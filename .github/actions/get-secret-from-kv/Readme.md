# 🔐 Extract Secrets from Azure Key Vault

Este composite action permite extraer secretos desde Azure Key Vault y exportarlos como variables de entorno en GitHub Actions. Es útil para configurar credenciales sensibles en tiempo de ejecución sin exponerlas en el código.

## 📦 ¿Qué hace?

- Utiliza la CLI de Azure para obtener secretos desde un Azure Key Vault.
- Oculta los valores en los logs (`::add-mask::`).
- Exporta cada secreto como variable de entorno (`$GITHUB_ENV`).

## 🚀 Uso

```yaml
jobs:
  load-secrets:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Login to Azure
        uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}

      - name: Extract secrets from Azure Key Vault
        uses: ./.github/actions/extractSecretFromAzKv
        with:
          secrets: "DB_PASSWORD API_KEY STORAGE_TOKEN"
          keyvault_name: "my-keyvault-name"
          subscription_id: "00000000-0000-0000-0000-000000000000"

      - name: Use secrets
        run: |
          echo "La contraseña es: $DB_PASSWORD"
          echo "La API Key es: $API_KEY"
```

## ⚙️ Inputs

| Nombre            | Descripción                                                                 | Requerido | Tipo     |
|-------------------|------------------------------------------------------------------------------|-----------|----------|
| `secrets`         | Lista de secretos a obtener del Azure Key Vault (separados por espacio)     | ✅         | `string` |
| `keyvault_name`   | Nombre del Azure Key Vault                                                   | ✅         | `string` |
| `subscription_id` | ID de suscripción de Azure donde se encuentra el Key Vault                  | ✅         | `string` |

## 🛠️ Requisitos

- Debes autenticarte previamente en Azure usando [`azure/login@v1`](https://github.com/Azure/login).
- La CLI de Azure (`az`) debe estar disponible en el runner (ya lo está en `ubuntu-latest`).
- Los secretos deben existir en el Key Vault especificado.

## 📄 Referencias

- [Azure Key Vault CLI](https://learn.microsoft.com/en-us/cli/azure/keyvault/secret)
- [GitHub Actions Environment Variables](https://docs.github.com/en/actions/learn-github-actions/environment-variables)
- [GitHub Masking Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#masking-secrets)
