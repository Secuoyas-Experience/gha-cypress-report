# gha-cypress-report

![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/Secuoyas-Experience/gha-cypress-report)

Esta acción genera el informe final (Mochawesome) de los tests de Cypress ejecutados antes con [Secuoyas-Experience/gha-cypress-run](https://github.com/Secuoyas-Experience/gha-cypress-run): baja todos los artefactos `cypress-*`, junta los resultados y las capturas y sube el informe como artefacto `report-merged`.

## Requisitos

Desde la `v10` usa `actions/checkout@v7`, `actions/cache@v6`, `actions/download-artifact@v8` y `actions/upload-artifact@v7`, que se ejecutan con Node.js 24: el runner tiene que ser la versión 2.327.1 o posterior. Con `download-artifact@v8`, un artefacto cuyo hash no cuadre hace fallar el job (antes solo avisaba).

El proyecto tiene que definir los scripts `report:generate` y `report:merge` en su `package.json`.

## Entradas

- **cache-path**: (opcional) ruta de la caché de Cypress (por defecto `.cache/Cypress`).
- **retention**: (opcional) días que se guarda el informe (por defecto 2).

## Uso

En el siguiente ejemplo se usa `gha-cypress-report` después de ejecutar los tests de Cypress:

```yaml
name: cypress-job

on:
  workflow_dispatch:

jobs:
  cypress-cache:
    ...

  cypress-tests:
    ...

  cypress-report:
    runs-on: griddo-qa
    if: ${{ !cancelled() }}
    needs:
      - cypress-tests
    steps:
      - uses: Secuoyas-Experience/gha-cypress-report@v10
```

También se pueden cambiar la ruta de la caché de Cypress y los días que se guarda el informe:

```yaml
      - uses: Secuoyas-Experience/gha-cypress-report@v10
        with:
          retention: 4
          cache-path: /path/to/cache
```
