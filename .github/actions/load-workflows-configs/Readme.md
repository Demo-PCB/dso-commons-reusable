# ⚙️ Load Workflows Configs

Este composite action carga configuraciones de workflows y variables de entorno desde un repositorio centralizado. Utiliza autenticación mediante GitHub App y permite importar configuraciones específicas por aplicación, componente y entorno.

## 🚀 ¿Qué hace?

- Autentica con GitHub App usando `actions/create-github-app-token@v2`.
- Clona el repositorio de configuraciones con `sparse-checkout`.
- Carga variables desde archivos YAML comunes, por aplicación, por componente y por entorno.
- Clona el repositorio de despliegue si se especifica.

## 📦 Uso

```yaml
jobs:
  load-configs:
    runs-on: ubuntu-latest
    steps:
      - name: Load workflow configs
        uses: ./.github/actions/load-workflows-configs
        with:
          application: 'my-app'
          component-name: 'api'
          environment: 'prd'
          dso-ghe-app-id: ${{ secrets.GHE_APP_ID }}
          dso-ghe-private-key: ${{ secrets.GHE_PRIVATE_KEY }}
          dso-workflows-configs-repo: 'workflows-configs'
          dso-workflows-configs-repo-owner: 'my-org'
          dso-deployment-repo: 'deployment-repo'
          dso-deployment-repo-owner: 'my-org'
          dso-deployment-region: 'us-east'

```
## 🧾 Inputs

| Nombre                          | Descripción                                                                 | Requerido | Tipo     | Default   |
|----------------------------------|------------------------------------------------------------------------------|-----------|----------|-----------|
| `application`                   | Nombre de la aplicación para cargar configuraciones                         | ✅         | `string` | —         |
| `component-name`               | Nombre del componente para cargar flags específicos                         | ✅         | `string` | —         |
| `environment`                  | Entorno objetivo (`dev`, `uat`, `stg`, `prd`)                                | ❌         | `string` | `''`      |
| `dso-ghe-app-id`               | GitHub App ID para autenticación                                            | ✅         | `string` | —         |
| `dso-ghe-private-key`          | Llave privada del GitHub App                                                | ✅         | `string` | —         |
| `dso-workflows-configs-repo`   | Repositorio que contiene las configuraciones de workflows                   | ✅         | `string` | —         |
| `dso-workflows-configs-repo-owner` | Propietario del repositorio de configuraciones                          | ✅         | `string` | —         |
| `dso-deployment-repo`          | Repositorio de despliegue de la aplicación                                  | ✅         | `string` | —         |
| `dso-deployment-repo-owner`    | Propietario del repositorio de despliegue                                   | ✅         | `string` | —         |
| `dso-deployment-region`        | Región de despliegue                                                        | ❌         | `string` | `default` |

## 🛠️ Requisitos

- Los repositorios deben estar accesibles mediante GitHub App con permisos adecuados.
- Los archivos YAML deben estar estructurados por aplicación, entorno y componente.
- El action `load-env-from-yaml` debe estar disponible en el repositorio `dso-commons-reusable`.

## 📄 Referencias

- [GitHub App Authentication](https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app)
- [GitHub Actions Environment Variables](https://docs.github.com/en/actions/learn-github-actions/environment-variables)
- [Sparse Checkout](https://git-scm.com/docs/git-sparse-checkout)
