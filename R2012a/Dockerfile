# syntax=docker/dockerfile:1.3

###
# installation stage
###
#FROM registry.access.redhat.com/rhel6/rhel:6.10-548 AS install
#FROM i386/centos:centos6 AS install
FROM centos:centos6.10 AS install

# can we make this a cache instad?
COPY iso/ /iso

# prep
ARG MATLAB_INSTALL_KEY
COPY installer_input.txt /
RUN sed -i s/fileInstallationKey=.*/fileInstallationKey=$MATLAB_INSTALL_KEY/ /installer_input.txt
COPY network.lic /

# take in the fileInstallationKey from ARG
RUN cat /installer_input.txt

# install
RUN cd iso/ \
  && ./install -mode silent -agreeToLicense yes -inputFile /installer_input.txt 

# spit out log
RUN cat /tmp/matlab-install.log

###
# final image stage
###
#FROM registry.access.redhat.com/rhel6/rhel:6.10-548
#FROM i386/centos:centos6
FROM centos:centos6.10

COPY CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo
RUN  yum clean all && yum makecache \
  && yum groupinstall -y "X Window System" \ 
  && yum install -y re2c glibc.i686 libX11.i686 zlib.i686 ncurses-libs.i686 libXext.i686 libXt.i686 libXmu.i686 \
  && yum clean all -y && rm -rf /var/cache 

COPY --from=install /usr/local/MATLAB/R2012a /usr/local/MATLAB/R2012a

