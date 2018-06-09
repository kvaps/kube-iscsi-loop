FROM kvaps/iscsi
RUN apt-get update \
 && apt-get -y install sheepdog \
 && apt-get clean
ADD sheepdog-publisher /
ENTRYPOINT [ "/seepdog-publisher" ]
