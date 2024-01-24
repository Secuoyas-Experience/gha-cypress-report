# gha-cypress-report

Esta accion permite generar el informe final de los tests que se han ejecutado anteriormente con Cypress.

## Inputs

- **cache-path**: (opcional) path donde se encuentra la cache de Cypress (.cache/Cypress)
- **retention**: (opcional) cuantos dias se debe guardar el informe generado

## Usage

En el siguiente ejemplo se muestra como utilizar el action `gha-cypress-report` despues de ejecutar los tests de cypress.

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
    runs-on: toolbox-griddo-qa
    needs:
      - cypress-tests
    steps:
      - uses: Secuoyas-Experience/gha-cypress-report@v1
```

Tambien se puede cambiar los parametros de cache de Cypress y de retencion de los informes

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
    runs-on: toolbox-griddo-qa
    needs:
      - cypress-tests
    steps:
      - uses: Secuoyas-Experience/gha-cypress-report@v1
        with:
          retention: 4
          cypress-cache: /path/to/cache
```