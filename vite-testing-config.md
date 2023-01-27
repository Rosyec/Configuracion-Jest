# Instalación y configuracion de Jest + React Testing Library
## En proyectos de React + Vite

1. Instalaciones (Typescript):
```
npm i --dev jest babel-jest @babel/preset-env @babel/preset-react 
npm i --dev @testing-library/react @types/jest jest-environment-jsdom
npm i --save-dev @babel/preset-typescript
npm i --save-dev jest typescript ts-jest @types/jest
```

2. Opcional: Si usamos Fetch API en el proyecto:
```
npm i --dev whatwg-fetch
```

3. Actualizar los scripts del __package.json__
```
"scripts: {
  ...
  "test": "jest --watchAll"
```

4. Crear la configuración de babel __babel.config.js__
```
module.exports = {
    presets: [
      [ '@babel/preset-env', {targets: {node: 'current'}} ],
      [ '@babel/preset-typescript' ],
      [ '@babel/preset-react', { runtime: 'automatic' } ]
    ],
  };
```

5. Opcional, pero eventualmente necesario, crear Jest config y setup:

__jest.config.cjs__

```
npx ts-jest config:init
```

```
/** @type {import('ts-jest').JestConfigWithTsJest} */
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'jsdom',
  setupFiles: ['./jest.setup.ts'],
  moduleNameMapper: {
    "\\.(css|sass)$": "identity-obj-proxy",
  }

};
```

__jest.setup.ts__
```
// En caso de necesitar la implementación del FetchAPI
import 'whatwg-fetch'; // <-- yarn add whatwg-fetch
```
6. Opcional: Configuración para que Jest detecte archivos .css
__jest.config.cjs__
```
module.exports = {
    moduleNameMapper: {
        "\\.(css|sass)$": "identity-obj-proxy",
      }
}
```
Luego instalamos la siguiente dependencia:
```
npm i --dev identity-obj-proxy
```
7. Opcional: Configuración de Jest Extend que proporciona nuevos matchers.
```
npm install --save-dev jest-extended
```
__testSetup.cjs__
```
// add all jest-extended matchers
import * as matchers from 'jest-extended';
expect.extend(matchers);

// or just add specific matchers
import { toBeArray, toBeSealed } from 'jest-extended';
expect.extend({ toBeArray, toBeSealed });
```
__jest.config.cjs__
```
setupFilesAfterEnv: ["jest-extended/all"]
```
Luego en cualquier archivo de pruebas, importamos Jest Extend:
```
import 'jest-extended';
```
8. Opcional: Tener autocompletado de Jest:
```
npm install -D @types/jest
```