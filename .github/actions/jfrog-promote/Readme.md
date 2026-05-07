# 📦 JFrog Promote iOS Library (HTTP)

Este composite action copia un archivo ZIP de una librería iOS (XCFramework) desde un repositorio snapshot a uno release candidate (RC) en JFrog Artifactory, utilizando únicamente HTTP (sin CLI ni APIs del sistema).

## 🚀 ¿Qué hace?

- Normaliza la URL base de Artifactory.
- Realiza una copia del artefacto vía HTTP: `GET` desde el repositorio origen y `PUT` al destino.
- Verifica la promoción mediante la API de almacenamiento (`api/storage`).
- Exporta outputs útiles como estado y nombre de build.

## ⚙️ Inputs

| Nombre              | Descripción                                                                 | Requerido | Default                                  |
|---------------------|------------------------------------------------------------------------------|-----------|------------------------------------------|
| `application`       | Nombre de la aplicación                                                      | ✅         | —                                        |
| `component-name`    | Nombre del componente                                                        | ✅         | —                                        |
| `version`           | Versión del componente                                                       | ✅         | —                                        |
| `source-repository` | Repositorio origen (ej. `dso-swift-snapshot`)                                | ✅         | —                                        |
| `target-repository` | Repositorio destino (ej. `dso-swift-rc`)                                     | ✅         | —                                        |
| `artifactory-url`   | URL base de Artifactory (`https://<org>.jfrog.io` o `https://host[/artifactory]`) | ✅         | —                                        |
| `artifactory-token` | Token de autenticación para Artifactory                                      | ✅         | —                                        |
| `library-type`      | Tipo de librería (`ios`, `framework`, `package`, `library`)                  | ❌         | `ios`                                    |
| `artifact-filename` | Nombre exacto del ZIP (ej. `CipherFramework.xcframework.zip`)                | ❌         | `CipherFramework.xcframework.zip`        |

## 📤 Outputs

| Nombre              | Descripción                                                                 |
|---------------------|------------------------------------------------------------------------------|
| `promotion-status`  | Estado de la promoción (`success` si fue exitosa)                            |
| `build-name`        | Nombre del build normalizado (lowercase del componente)                     |
| `target-repository` | Repositorio destino usado en la promoción                                   |

## 🛠️ Requisitos

- El ZIP debe existir en el repositorio origen con la ruta esperada.
- El token debe tener permisos de lectura y escritura en ambos repositorios.
- No se realiza discovery automático: el nombre del artefacto debe ser proporcionado.

## 📄 Referencias

- [JFrog Artifactory REST API](https://jfrog.com/help/r/jfrog-rest-apis/artifactory-rest-apis)
- [GitHub Actions Environment Variables](https://docs.github.com/en/actions/learn-github-actions/environment-variables)
