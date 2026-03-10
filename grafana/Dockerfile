FROM grafana/grafana:12.3

USER root

RUN grafana cli plugins install grafana-advisor-app
RUN grafana cli plugins update-all

USER grafana
