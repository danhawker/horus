FROM registry.access.redhat.com/ubi8/ubi as go_builder

ENV DESCRIPTION="Prometheus Cisco Exporter for iOS and NXOS. \
Based on code from https://github.com/lwlcom/cisco_exporter"

LABEL org.opencontainers.image.title="cisco_exporter" \
      org.opencontainers.image.description="$DESCRIPTION" \
      org.opencontainers.image.authors="danhawker" \
      org.opencontainers.image.url="https://github.com/danhawker/horus"

RUN mkdir "/root/gopath"

WORKDIR /root/gopath

RUN yum -y install --disableplugin=subscription-manager golang git; \
	yum  --disableplugin=subscription-manager clean all; \
	rm -rf /var/cache/yum

RUN go get -u github.com/lwlcom/cisco_exporter


FROM registry.access.redhat.com/ubi8/ubi-minimal
RUN mkdir -p /bin
WORKDIR /bin

COPY --from=go_builder /root/go/bin/cisco_exporter /bin/
RUN chmod +x /bin/cisco_exporter
EXPOSE 9362 

#CMD [ "/bin/cisco_exporter" ]
ENTRYPOINT ["/bin/cisco_exporter"]

# EOF
