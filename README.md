# mysql_client_configeditor
To build docker image of mysql57 when we need to run mysql_config_editor

In Dockerfile, we have to change the original content downloaded via https://hub.docker.com/r/widdpim/mysql-client/dockerfile

=========================================================

FROM centos:7

#COPY mysql57-community.repo /etc/yum.repos.d/

RUN yum-config-manager --enable mysql57-community && \
    yum makecache fast && \
    yum install -y mysql-community-client curl && \
    yum clean all && \
    rm -rf /var/cache/yum/*

CMD ["bash"]

=========================================================

the reason why we comment out the COPY action of repo file into docker but use yum insteaded.
yum-config-manager is to allow you config and enable the repository of mysql57-community the download and install through it.

By running the command build.sh, you can get the docker image build-up as required.
As the docker image name specified in no matter Dockerfile or command parameter of "docker build", you could have image created in your local repository as need.

As the practice of Dockerfile, you had better to run all of the commands castcaded rather than separately thus && is essentially in RUN action.
