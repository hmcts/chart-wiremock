# chart-wiremock
This chart is intended to be used for mocking components which are not available in the relevant environments

## Example configuration


in chart.yaml
```yaml
  - name: wiremock
    version: 0.0.3
    repository: 'https://hmctspublic.azurecr.io/helm/v1/repo/'
    condition: wiremock.enabled
```
in preview.yaml
```yaml
wiremock:
  enabled: true
  image: "wiremock/wiremock"
  applicationPort: 8080
  imagePullPolicy: Always
  releaseNameOverride : ${SERVICE_NAME}-wiremock
  ingressHost: wiremock-${SERVICE_NAME}.preview.platform.hmcts.net
  volumes:
    - name: wiremock-mocks
      configMap:
        name: ${SERVICE_NAME}-wiremock-mocks
  volumeMounts:
    - name: wiremock-mocks
      mountPath: /home/wiremock/mappings
      subPath: mappings
```
