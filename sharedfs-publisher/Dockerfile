FROM alpine
RUN apk add --no-cache openiscsi
ADD sharedfs-publisher /
ENTRYPOINT [ "/sharedfs-publisher" ]
