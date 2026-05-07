# 🧮 GitVersion Semantic Version GitHub Action

Este composite action genera una versión semántica (`semVer`) utilizando [GitVersion](https://gitversion.net/) en modo `ContinuousDeployment`. Es útil para automatizar el versionado en flujos CI/CD según el tipo de rama.

## 📦 ¿Qué hace?

- Detecta el sistema operativo del runner (`Linux` o `macOS`).
- Descarga e instala GitVersion desde GitHub Releases.
- Genera un archivo `GitVersion.yml` con configuración personalizada.
- Ejecuta GitVersion y exporta el resultado como output (`semVer`).

## 🚀 Uso

```yaml
jobs:
  versioning:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Generate semantic version
        uses: ./.github/actions/gitversion

      - name: Use version
        run: echo "Versión generada: ${{ steps.get-version.outputs.semVer }}"
```
## 📤 Outputs

| Nombre   | Descripción                                      |
|----------|--------------------------------------------------|
| `semVer` | Versión semántica generada por GitVersion        |

## ⚙️ Configuración de GitVersion

El archivo `GitVersion.yml` se genera automáticamente con la siguiente lógica:

- **Modo:** `ContinuousDeployment`
- **Incrementos por rama:**
  - `main`, `master`: `Patch`
  - `develop`: `Minor`
  - `feature`, `release`, `hotfix`: `Patch`
- Control de versiones fusionadas y seguimiento de ramas fuente

## 🛠️ Requisitos

- El runner debe ser **Linux** o **macOS**.
- Se requiere `jq` para extraer el valor `SemVer` del JSON generado.
- No se necesita instalación previa de GitVersion; se descarga automáticamente.

## 📄 Referencias

- [GitVersion Documentation](https://gitversion.net/docs/)
- [GitVersion GitHub Releases](https://github.com/GitTools/GitVersion/releases)
- [Semantic Versioning](https://semver.org/)
