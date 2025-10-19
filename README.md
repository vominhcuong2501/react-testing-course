# React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type-aware lint rules:

```js
export default tseslint.config({
  extends: [
    // Remove ...tseslint.configs.recommended and replace with this
    ...tseslint.configs.recommendedTypeChecked,
    // Alternatively, use this for stricter rules
    ...tseslint.configs.strictTypeChecked,
    // Optionally, add this for stylistic rules
    ...tseslint.configs.stylisticTypeChecked,
  ],
  languageOptions: {
    // other options...
    parserOptions: {
      project: ["./tsconfig.node.json", "./tsconfig.app.json"],
      tsconfigRootDir: import.meta.dirname,
    },
  },
});
```

You can also install [eslint-plugin-react-x](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-x) and [eslint-plugin-react-dom](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-dom) for React-specific lint rules:

```js
// eslint.config.js
import reactX from "eslint-plugin-react-x";
import reactDom from "eslint-plugin-react-dom";

export default tseslint.config({
  plugins: {
    // Add the react-x and react-dom plugins
    "react-x": reactX,
    "react-dom": reactDom,
  },
  rules: {
    // other rules...
    // Enable its recommended typescript rules
    ...reactX.configs["recommended-typescript"].rules,
    ...reactDom.configs.recommended.rules,
  },
});
```

# install vitest

npm i -D vitest jsdom @testing-library/react @testing-library/user-event @testing-library/jest-dom

1. create file setup.ts in src (config global)
   afterEach(()=>{
    cleanup();
    vi.clearAllMocks()
   })

2. create vitest.config.ts
    import { defineConfig } from 'vitest/config'

    export default defineConfig({
      test: {
        globals: true,
        environment: 'jsdom',
        setupFiles: './test/setup'
      }
    })


3. add config in tsconfig.app.json
   "types": [
    "vitest/globals",
    "@testing-library/jest-dom"
   ]

4. add config in tsconfig.json
   "compilerOptions": {
    "types": [
      "vitest/globals",
      "@testing-library/jest-dom",
      "node"
    ]
   }

5. add package.json in script
   "test": "vitest"

# install jest
npm i -D jest ts-jest @types/jest @testing-library/react @testing-library/jest-dom jest-environment-jsdom ts-node
1. create file src/test/jest.setup.ts (config global)
   import "@testing-library/jest-dom";

2. create jest.config.ts
  import type { Config } from "jest";

  const config: Config = {
    rootDir: "./",
    testEnvironment: "jsdom",
    setupFilesAfterEnv: ["<rootDir>/test/jest.setup.ts"],
    moduleNameMapper: {
      "\\.(gif|jpg|jpeg|png|svg|ttf|eot)$": "<rootDir>/test/mocks/fileMock.js",
      "\\.(css|less)$": "<rootDir>/test/mocks/styleMock.js",
    },
    transform: {
      "^.+\\.(ts|tsx)$": "ts-jest",
      "^.+\\.(js|jsx)$": "babel-jest",
    },
  };

  export default config;


3. create file src/test/mocks/fileMock.js
   module.exports = {
    __esModule: true,
    default: 'test-file-stub',
}

4. add config in tsconfig.app.json
   "include": ["src", "test"]

5. add config in tsconfig.json
    "types": ["@testing-library/jest-dom"]


6. add package.json in script
   "test": "jest"

# link Youtube Typescript: https://www.youtube.com/watch?v=KmuJOm09e98