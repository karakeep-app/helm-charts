# Karakeep Helm chart

Helm chart for deploying Karakeep along with:

- **[Meilisearch](https://github.com/meilisearch/meilisearch-kubernetes)**: for fast and lightweight full-text search
- **[Headless Chrome](https://github.com/jlandure/alpine-chrome)**: enables web page previews

This chart inherits from the [bjw-s/common](https://github.com/bjw-s/helm-charts/tree/main/charts/library/common) library.


### Usage

```bash
helm repo add karakeep-app https://karakeep-app.github.io/helm-charts
helm repo update
helm install karakeep karakeep-app/karakeep
```



### Configuration

| Key                    | Description                              | Default                  |
| ---------------------- | ---------------------------------------- | ------------------------ |
| `applicationHost`      | Hostname used in ingress/service         | `karakeep.domain`        |
| `applicationProtocol`  | Protocol for internal service references | `http`                   |
| `applicationSecretKey` | Secret used for app authentication       | Auto-generated if `null` |
| `meilisearchMasterKey` | Meilesearch master key                   | Auto-generated if `null` |

#### Adding Custom Environment Variables

To add custom environment variables without overriding the defaults, add them to the `secrets.karakeep.stringData` section:

```yaml
secrets:
  karakeep:
    stringData:
      CUSTOM_VAR: "custom-value"
      ANOTHER_VAR: "another-value"
```

These variables will be automatically merged with the default environment variables defined in the chart.

#### Example with OIDC Authentication

```yaml
secrets:
  karakeep:
    stringData:
      DISABLE_PASSWORD_AUTH: "true"
      OAUTH_ALLOW_DANGEROUS_EMAIL_ACCOUNT_LINKING: "true"
      OAUTH_PROVIDER_NAME: OIDC
      OAUTH_SCOPE: openid email profile
      OAUTH_WELLKNOWN_URL: https://auth.company/application/o/karakeep/.well-known/openid-configuration
      OAUTH_CLIENT_ID: your-client-id
      OAUTH_CLIENT_SECRET: your-client-secret
```
