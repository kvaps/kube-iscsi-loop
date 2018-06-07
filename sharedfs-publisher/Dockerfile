FROM alpine
RUN apk add --no-cache open-iscsi
ADD sharedfs-publisher /
ENTRYPOINT [ "/sharedfs-publisher" ]
