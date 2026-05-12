# ${{ github.event.repository.name }}

Repositorio caller de ejemplo para actualizar Azure Key Vault usando workflows reutilizables.

## Archivos principales

- `.github/workflows/ci.yml`: valida, empaqueta y publica en JFrog.
- `.github/workflows/cd-dev.yml`: despliega DEV manual o automáticamente después de CI exitoso en `main`.
- `.github/workflows/cd-uat.yml`: despliega UAT con aprobación del GitHub Environment `uat`.
- `.github/workflows/cd-prd.yml`: despliega PRD con aprobación del GitHub Environment `prd`.
- `.github/workflows/rollback.yml`: rollback manual para `dev` o `uat`.
- `.github/workflows/rollback-prd.yml`: rollback manual para producción con Environment `prd-rollback`.
- `keyvault/config.yml`: define el Key Vault por ambiente.
- `keyvault/data.json`: define los nombres de secretos que deben existir.

## Política aplicada

El pipeline no administra valores reales. Solo crea secretos faltantes con valor inicial `DEMO`.

- Si el secreto no existe: lo crea con `DEMO`.
- Si existe y vale `DEMO`: no lo modifica.
- Si existe y tiene otro valor: no lo sobrescribe.

## Secrets/variables esperadas

Secrets:

- `AZURE_CLIENT_ID`
- `AZURE_TENANT_ID`
- `AZURE_SUBSCRIPTION_ID`
- `DSO_ARTIFACTORY_TOKEN`

Variables:

- `IBK_ARTIFACTORY_URL`
