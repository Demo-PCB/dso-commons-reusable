# 📦 Publish Artifacts Decision GitHub Action

Este composite action determina si los artefactos deben publicarse en función del tipo de rama y evento del workflow. Es útil para controlar la publicación condicional en flujos CI/CD.

## ⚙️ ¿Qué hace?

- Detecta el tipo de rama (`main`, `develop`, `feature`, `release`, `hotfix`, `tag`, `pull request`).
- Detecta el tipo de evento (`push`, `release`, `pull_request`, `workflow_dispatch`).
- Establece la variable `publish-artifacts` como `true` o `false` según la lógica definida.

## 🚀 Uso

```yaml
jobs:
  decide-publish:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Decide if artifacts should be published
        uses: ./.github/actions/publish-artifacts

      - name: Use decision
        run: echo "Publish artifacts: ${{ steps.set-vars.outputs.publish-artifacts }}"
```
## 📤 Outputs

| Nombre              | Descripción                                                                 |
|---------------------|------------------------------------------------------------------------------|
| `publish-artifacts` | Indica si los artefactos deben publicarse según el tipo de rama y evento.   |

## 🧠 Lógica de decisión

Se publican artefactos si la rama es:

- `main`, `master`
- `release/*`
- `develop`
- `hotfix/*`
- `refs/tags/*`

No se publican si es:

- `feature/*`
- `pull request`
- Desconocida

## 🛠️ Requisitos

- Este action no requiere dependencias externas.
- Se ejecuta en shell `bash` y utiliza variables de entorno de GitHub (`GITHUB_REF`, `GITHUB_EVENT_NAME`).

## 📄 Referencias

- [GitHub Actions Contexts](https://docs.github.com/en/actions/learn-github-actions/contexts)
- [GitHub Events](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)
