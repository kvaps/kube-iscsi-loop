FROM alpine
RUN apk add --no-cache curl jq e2fsprogs xfsprogs \
 && curl -Lo /usr/local/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl \
 && chmod +x /usr/local/bin/kubectl
ADD iscsi-sharedfs-deleter iscsi-sharedfs-provisioner /
