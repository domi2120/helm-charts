# A Helm chart for Tube Archivist
This chart bundles Tube Archivist along with a bitnami Redis (for now).
The Elasticsearch must be provided externally.

## Installation
```bash
helm repo add tubearchivist https://domi2120.github.io/helm-charts/
helm upgrade --install tubearchivist tubearchivist/tube-archvist
```

## Values
Most commonly the following values will need to be configured. For further configurations, refer to the [values.yaml](values.yaml)
```
persistence:
  cache:
    size: 5Gi
  youtube: 
    size: 20Gi

ingress:
  enabled: true
  className: ""
  hosts:
    - host: test.chart.local
      paths:
        - path: /
          pathType: ImplementationSpecific
  tls: []

env:
  - name: "TA_HOST"
    value: "https://test.chart.local" # make sure to include the protocl here, otherwise you'll get 403 and a redirect to login page when trying to add something to download
  - name: "TA_PASSWORD"
    value: "changeme"
  - name: "TA_USERNAME"
    value: "admin"
  - name: "ELASTIC_USER"
    value: "elastic"
  - name: "ES_URL"
    value: "http://elastic:9200"
  - name: "REDIS_CON"
    value: "redis://redis-master:6379"
  - name: "ELASTIC_PASSWORD"
    value: "changeme"
```

### Notes
* This chart also bundles the [bgutil-ytdlp-pot-provider](https://github.com/Brainicism/bgutil-ytdlp-pot-provider), which can be integrated with tube-archivist according to the official [docs](https://docs.tubearchivist.com/settings/application/#po-token-provider-url). The Url to enter is http://<release-name>-pot-provider:4416