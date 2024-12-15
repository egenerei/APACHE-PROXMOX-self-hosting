# Grafana's datasources

- Add as many datasources as needed after datasources following the example starting from - name

```yaml
apiVersion: 1
#
datasources:
  - name: web1
    type: prometheus
    access: proxy
    url: http://localhost:9090
    isDefault: true
    jsonData:
      timeInterval: 5s
```
