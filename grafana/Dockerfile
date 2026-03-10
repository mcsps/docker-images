FROM grafana/grafana:12.3.5

USER root

RUN grafana cli plugins install grafana-advisor-app
RUN grafana cli plugins update-all
RUN cp -R /var/lib/grafana/plugins /opt && chown -R grafana:grafana /opt/plugins

USER grafana
