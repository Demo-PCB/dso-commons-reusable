# 📄 Load Env Vars from YAML

Este composite action carga variables de entorno desde uno o más archivos YAML y las exporta al entorno de GitHub Actions (`GITHUB_ENV`). Es útil para centralizar configuraciones sensibles o reutilizables en archivos YAML.

## 🚀 ¿Qué hace?

- Instala la librería `PyYAML` usando `pip`, `pip --user` o `apt-get` como fallback.
- Lee uno o más archivos YAML especificados.
- Exporta las claves y valores como variables de entorno.
- Falla opcionalmente si algún archivo YAML no existe.

## ⚙️ Inputs

| Nombre           | Descripción                                                       | Requerido | Tipo     | Default |
|------------------|--------------------------------------------------------------------|-----------|----------|---------|
| `yaml-path`      | Ruta(s) de archivo(s) YAML (una línea o múltiples líneas)         | ✅         | `string` | —       |
| `fail-if-missing`| Falla si algún archivo YAML no existe (`true` o `false`)          | ❌         | `boolean`| `false` |

## 🛠️ Requisitos

- El runner debe tener Python y `pip` disponibles (ya incluidos en `ubuntu-latest`).
- Los archivos YAML deben tener formato plano de clave-valor (`key: value`).
- Si se usa `fail-if-missing: true`, el workflow fallará si algún archivo no se encuentra.

## 📤 Outputs

Este action no define outputs explícitos, pero todas las variables del YAML se exportan al entorno y pueden usarse en pasos posteriores.

## 📄 Referencias

- [GitHub Actions Environment Variables](https://docs.github.com/en/actions/learn-github-actions/environment-variables)
- [PyYAML Documentation](https://pyyaml.org/wiki/PyYAMLDocumentation)
- [GitHub Masking Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#masking-secrets)
