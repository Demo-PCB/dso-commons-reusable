# 🖼️ Cosign Image GitHub Action

Este composite action permite firmar y verificar imágenes de contenedor utilizando [Cosign](https://docs.sigstore.dev/cosign/overview) en modo sin clave (keyless). Es útil para garantizar la integridad y autenticidad de imágenes en flujos CI/CD.

## 📦 ¿Qué hace?

- Instala Cosign.
- Firma una imagen con una attestation personalizada (`attest`).
- Verifica la attestation de una imagen (`verify-attestation`).

## 🚀 Uso

```yaml
jobs:
  sign-image:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Sign image
        uses: ./.github/actions/cosign
        with:
          workflow_name: 'ci'
          mode: 'sign'
          reference_image: 'ghcr.io/org/image:tag'
          predicate_path: './metadata/predicate.json'

  verify-image:
    runs-on: ubuntu-latest
    steps:
      - name: Verify image
        uses: ./.github/actions/cosign
        with:
          workflow_name: 'ci'
          mode: 'verify'
          reference_image: 'ghcr.io/org/image:tag'
          predicate_path: './metadata/predicate.json'
          output_result_path: './output/verify-result.json'
```

## ⚙️ Inputs

| Nombre              | Descripción                                               | Requerido | Por defecto |
|---------------------|-----------------------------------------------------------|-----------|-------------|
| `workflow_name`     | Nombre del workflow que firmó la imagen                   | ✅         | `ci`        |
| `mode`              | Modo de operación: `sign` o `verify`                      | ✅         | `verify`    |
| `reference_image`   | Referencia de la imagen a firmar o verificar              | ✅         | `''`        |
| `predicate_path`    | Ruta del archivo de metadatos (predicate)                 | ✅         | `''`        |
| `output_result_path`| Ruta de salida para el resultado de verificación          | ❌         | `''`        |

## 🛠️ Requisitos

- El entorno debe tener acceso a GitHub OIDC para firmar en modo keyless.
- Cosign se instala automáticamente mediante [`sigstore/cosign-installer@v3.7.0`](https://github.com/sigstore/cosign-installer).

## 📄 Referencias

- [Cosign Documentation](https://docs.sigstore.dev/cosign/overview)
- [Sigstore Keyless Signing](https://docs.sigstore.dev/cosign/keyless)
