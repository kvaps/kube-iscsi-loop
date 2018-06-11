FROM kvaps/sheepdog
RUN apt-get update \
 && apt-get -y install curl jq \
 && apt-get clean \
 && curl -Lo /usr/local/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl \
 && chmod +x /usr/local/bin/kubectl
ADD iscsi-sheepdog-deleter iscsi-sheepdog-provisioner /
