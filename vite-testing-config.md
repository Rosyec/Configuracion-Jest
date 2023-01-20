# Instalación y configuracion de Jest + React Testing Library
## En proyectos de React + Vite

1. Instalaciones:
```
npm i --dev jest babel-jest @babel/preset-env @babel/preset-react 
npm i --dev @testing-library/react @types/jest jest-environment-jsdom
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
        [ '@babel/preset-env', { targets: { esmodules: true } } ],
        [ '@babel/preset-react', { runtime: 'automatic' } ],
    ],
};
```

5. Opcional, pero eventualmente necesario, crear Jest config y setup:

__jest.config.js__
```
module.exports = {
    testEnvironment: 'jest-environment-jsdom',
    setupFiles: ['./jest.setup.js']
}
```

__jest.setup.js__
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