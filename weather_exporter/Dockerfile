FROM registry.access.redhat.com/ubi8/python-27

ENV DESCRIPTION="Prometheus Weather Exporter that uses the Dark Sky API. \
Based on code from https://github.com/celliott/weather_exporter"

LABEL org.opencontainers.image.title="weather_exporter" \
      org.opencontainers.image.description="$DESCRIPTION" \
      org.opencontainers.image.authors="danhawker" \
      org.opencontainers.image.url="https://github.com/danhawker/horus"

# Add python deps
ADD ./requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

# Add config
ADD ./config/sample.json /etc/weather_exporter/config.json

# Add exporter
ADD ./src/weather_exporter /opt/weather_exporter
RUN chmod +x /opt/weather_exporter/*

EXPOSE 9265
USER 65534

ENTRYPOINT ["/opt/weather_exporter/exporter.py", "--config=/etc/weather_exporter/config.json"]