FROM registry.access.redhat.com/ubi8

ENV OC_VERSION=4.5.10 \
    ODO_VERSION=v1.2.6 \
    ANSIBLE_VERSION=2.9 \
    JQ_VERSION=1.6 \
    HELM_VERSION=v3.2.3 \
    TEKTON_VERSION=0.12.1 \
    HOME=/home/tool-box \
    INSTALL_PKGS="git vim unzip python36 iputils"

RUN yum -y update && \
    yum -y install $INSTALL_PKGS && \
    yum clean all

RUN curl -o jq --fail -sL https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64 && \
    chmod +x jq && \
    mv jq /usr/local/bin

RUN mkdir -m 775 $HOME && \
    chmod 775 /etc/passwd && \
    pip3 install git+https://github.com/ansible/ansible.git@stable-${ANSIBLE_VERSION}

RUN curl --fail -s https://get.helm.sh/helm-${HELM_VERSION}-linux-amd64.tar.gz | tar -xvz && \
    chmod u+x linux-amd64/helm && mv linux-amd64/helm /usr/local/bin/ && rm -rf linux-amd64

RUN curl --fail -sL https://github.com/tektoncd/cli/releases/download/v${TEKTON_VERSION}/tkn_${TEKTON_VERSION}_Linux_x86_64.tar.gz | tar --no-same-owner -xvz -C /usr/local/bin/ tkn

RUN curl --fail -sL https://mirror.openshift.com/pub/openshift-v4/clients/ocp/${OC_VERSION}/openshift-client-linux-${OC_VERSION}.tar.gz | tar -C /usr/local/bin/ -xzf -

RUN curl --fail -sL https://mirror.openshift.com/pub/openshift-v4/clients/odo/${ODO_VERSION}/odo-linux-amd64 -o /usr/local/bin/odo && \
    chmod +x /usr/local/bin/odo
    
RUN printf '[mongodb-enterprise-4.2] \nname=MongoDB Repository \nbaseurl=https://repo.mongodb.com/yum/redhat/$releasever/mongodb-enterprise/4.2/$basearch/ \ngpgcheck=1 \nenabled=1 \ngpgkey=https://www.mongodb.org/static/pgp/server-4.2.asc' > /etc/yum.repos.d/mongodb-enterprise-4.2.repo

RUN yum install -y mongocli

RUN yum install -y https://downloads.mongodb.com/compass/mongosh-0.5.0-x86_64.rpm

RUN yum install -y https://repo.mongodb.com/yum/redhat/8/mongodb-enterprise/4.4/x86_64/RPMS/mongodb-enterprise-shell-4.4.1-1.el8.x86_64.rpm

RUN yum install -y https://fastdl.mongodb.org/tools/db/mongodb-database-tools-rhel80-x86_64-100.2.0.rpm

WORKDIR $HOME

ADD ./root /

RUN chmod u+x /usr/local/bin/run && \
    rm -rf $HOME/.cache

USER 1001

ENTRYPOINT ["/usr/local/bin/run"]
CMD ["sleep", "infinity"]
