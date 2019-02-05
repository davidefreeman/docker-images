# LICENSE CDDL 1.0 + GPL 2.0
#
# Copyright (c) 2014-2017 Oracle and/or its affiliates. All rights reserved.
#
# ORACLE GoldenGate DOCKERFILES PROJECT
# -----------------------------------------
# This is the DockerFile for Oracle GoldenGate for BigData 12.3.2.1.1
#
# IMPORTANT
# -------------------------------------------
# The resulting image of this Dockerfile would have Oracle Linux 7 and GoldenGate for BigData 12.3.2.1.1 installed in standalone mode.
#
# REQUIRED FILES TO BUILD THIS IMAGE
# ----------------------------------
# (1) OGG_BigData_Linux_x64_12.3.2.1.1.zip (Oracle GoldenGate 12c for BigData (12.3.2.1.1)
#     Download from http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html
#
ARG         BASE_IMAGE=oracle/instantclient:12.2.0.1
FROM      ${BASE_IMAGE}
MAINTAINER Bobby Curtis <bobby.curtis@oracle.com>
#Container Additional Environment Variables
ENV OGG_SHIPHOME=OGG_BigData_Linux_x64_12.3.2.1.1.zip \
    OGG_HOME=/u01/app/oracle/product/12.3.2.1.1/oggbd_1 \
    OGG_PORT=9500 \
    STAGE_SOFTWARE=/u01/software
ENV PATH=$OGG_HOME:$PATH \
    LD_LIBRARY_PATH=$OGG_HOME:$OGG_HOME/lib:$LD_LIBRARY_PATH
#Command during the build
RUN yum install -y util-linux zip unzip tar && yum clean all
#Create installation directories
RUN mkdir -p $OGG_HOME $STAGE_SOFTWARE
#Copy any artifacts to the image
ADD entrypoint.sh /
ADD $OGG_SHIPHOME $STAGE_SOFTWARE
EXPOSE $OGG_PORT
ENTRYPOINT ["/entrypoint.sh"]
