FROM kvaps/iscsi
RUN apt-get update \
 && apt-get -y install sheepdog \
 && apt-get clean
ADD iscsi-sheepdog-publisher /
ENTRYPOINT [ "/iscsi-sheepdog-publisher" ]
