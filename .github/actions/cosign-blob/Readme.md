# 🔐 Cosign Artifacts GitHub Action

Este composite action permite firmar y verificar artefactos utilizando [Cosign](https://docs.sigstore.dev/cosign/overview) en modo sin clave (keyless). Es ideal para flujos CI/CD que requieren integridad y trazabilidad de artefactos.

## 📦 ¿Qué hace?

- Instala Cosign.
- Firma artefactos con una attestation personalizada (`attest-blob`).
- Verifica firmas y attestations (`verify-blob-attestation`).

## 🚀 Uso

```yaml
jobs:
  sign-artifact:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Sign artifact
        uses: ./.github/actions/cosign
        with:
          workflow_name: 'ci'
          mode: 'sign'
          artifact_path: './build/my-artifact.tar.gz'
          predicate_path: './metadata/predicate.json'
          output_attestation_path: './output/attestation.json'
          output_bundle_path: './output/bundle.json'

  verify-artifact:
    runs-on: ubuntu-latest
    steps:
      - name: Verify artifact
        uses: ./.github/actions/cosign
        with:
          workflow_name: 'ci'
          mode: 'verify'
          artifact_path: './build/my-artifact.tar.gz'
          predicate_path: './metadata/predicate.json'
          output_result_path: './output/verify-result.json'
```
## ⚙️ Inputs

| Nombre                    | Descripción                                               | Requerido | Por defecto |
|---------------------------|-----------------------------------------------------------|-----------|-------------|
| `workflow_name`           | Nombre del workflow que firmó el artefacto                | ✅         | `ci`        |
| `mode`                    | Modo de operación: `sign` o `verify`                      | ✅         | `verify`    |
| `artifact_path`           | Ruta del archivo a firmar o verificar                     | ✅         | `''`        |
| `predicate_path`          | Ruta del archivo de metadatos (predicate)                 | ✅         | `''`        |
| `output_result_path`      | Ruta de salida para el resultado de verificación          | ❌         | `''`        |
| `output_bundle_path`      | Ruta de salida para el bundle generado al firmar          | ❌         | `''`        |
| `output_attestation_path` | Ruta de salida para la attestation generada               | ❌         | `''`        |

## 🛠️ Requisitos

- El entorno debe tener acceso a GitHub OIDC para firmar en modo keyless.
- Cosign se instala automáticamente mediante [`sigstore/cosign-installer@v3.7.0`](https://github.com/sigstore/cosign-installer).

## 📄 Referencias

- [Cosign Documentation](https://docs.sigstore.dev/cosign/overview)
- [Sigstore Keyless Signing](https://docs.sigstore.dev/cosign/keyless)
