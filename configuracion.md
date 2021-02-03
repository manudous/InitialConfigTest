# Testing Con Jest

>## Librerías

Vamos a instalar las librerías de Jest y sus typing.

``npm install jest @types/jest ts-jest --save-dev```

>## Configuración

- Jest test comandos:
  - `npm test`: para un solo test
  - `npm run test:watch`: mirar todos los cambios

### ./package.json

```diff
{
  ...
  "scripts": {
    ...
-   "clean": "rimraf dist"
+   "clean": "rimraf dist",
+   "test": "jest --verbose",
+   "test:watch": "npm run test -- --watchAll -i"
  },
  ...
}
```

> NOTE:

> [Jest CLI options](https://facebook.github.io/jest/docs/en/cli.html#options)

> --watchAll To rerun all tests.

> --watch To rerun tests related to changed files.

> --verbose Display individual test results with the test suite hierarchy.

> -i or --runInBand Run all tests serially in the current process, rather than creating a worker pool of child processes that run tests. This can be useful for debugging

### ./package.json

```diff
{
  ...
  "scripts": {
    ...
-   "clean": "rimraf dist"
+   "clean": "rimraf dist",
+   "test": "jest --verbose",
+   "test:watch": "npm run test -- --watchAll -i"
  },
  ...
}
```

- [ts-jest basic configuration](https://kulshekhar.github.io/ts-jest/user/config/#basic-usage):

### ./package.json

```diff
{
    ...
- }
+ },
+ "jest": {
+   "preset": "ts-jest"
+ }
```

- Finalmente vamos a restaurar automáticamente el estado del mock para cada test:

### ./package.json

```diff
{
  ...
  "jest": {
-   "preset": "ts-jest"
+   "preset": "ts-jest",
+   "restoreMocks": true
  }
}
```

> [Opciones configuración de Jest](https://facebook.github.io/jest/docs/en/configuration.html#options)

# Dummy spec

- Vamos a arrancar los test en watch mode:

```bash
npm run test:watch
```

+ Añadiendo un archivo para los test 

### ./src/dummy.spec.ts

```javascript
describe('dummy specs', () => {
  it('should pass spec', () => {
    // Arrange
    Definimos todo lo previo para ejecutar el test
    variables, mocks, etc...
    // Act
    Ejecución del test
    // Assert
    Comprobamos que los resultados son los esperados
    expect(true).toBeTruthy();
  });
});
```

Para para el proceso pulsamos q, o pulsamos w y luego q en la consola.

### ./config/test/jest.js

```diff
module.exports = {
  rootDir: '../../',
  preset: 'ts-jest',
  restoreMocks: true,
};

```

- Sacamos el jest del package.json a un archivo y usamos ese archivo en el package.json

### ./package.json

```diff
{
  ...
  "scripts": {
    ...
-   "test": "jest --verbose",
+   "test": "jest -c ./config/test/jest.js --verbose",
    "test:watch": "npm run test -- --watchAll -i"
  },
  ...
}
```

- Con el -c le decimos al webpack la ruta donde está nuestro archivo de configuración de jest.