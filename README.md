# eslint-cheat-sheet

<br><br>
<br><br>

## Install

## Typescript
```
npm i --save-dev eslint
npm init @eslint/config@latest

# Go through guide and select typescript
```

<br><br>
<br><br>

### eslint-config-google
```bash
npm install --save-dev eslint eslint-config-google
```

<br><br>
<br><br>

### eslint-config-google with babel
```bash
npm install --save-dev eslint eslint-config-google @babel/eslint-parser @babel/plugin-proposal-decorators @babel/plugin-proposal-class-properties @babel/plugin-transform-flow-strip-types
```






















<br><br>
<br><br>
____________________________________________________
____________________________________________________
<br><br>
<br><br>

# Typescript eslint
- https://typescript-eslint.io/getting-started

## Install
```shell
npm install --save-dev eslint @eslint/js @types/eslint__js typescript typescript-eslint
```

eslint.config.mjs:
```typescript

import eslint from '@eslint/js'
import tseslint from 'typescript-eslint'

export default tseslint.config(
    // ===== ESLINT RULES =====
    {
        ...eslint.configs.recommended,
        rules: {
            ...eslint.configs.recommended.rules,

            // Hier fügst du deine neue Regel hinzu
            'arrow-parens': ['error', 'as-needed'],
            'no-var': 1,
            'no-eval': 'error',
            indent: ['error', 4],
            quotes: ['error', 'single'],
            'no-console': 'off',
            'space-before-function-paren': ['error', 'never'],
            'padded-blocks': ['error', 'never'],

            'prefer-arrow-callback': [0, {
                allowNamedFunctions: true
            }],

            'func-names': ['error', 'never'],

            'no-use-before-define': ['error', {
                functions: true,
                classes: true
            }],

            'max-len': ['error', 120],
            'object-curly-spacing': 0,
            'comma-dangle': ['error', 'never'],
            semi: [2, 'never'],
            'new-cap': 0,
            'one-var': 0,
            'guard-for-in': 0,
        }
    },

    // ===== TSESLINT RULES =====
    ...tseslint.configs.stylisticTypeChecked,
    ...tseslint.configs.recommendedTypeChecked,
    {
        languageOptions: {
            parserOptions: {
                projectService: true,
                tsconfigRootDir: import.meta.dirname,
            }
        }
    },
    // ...tseslint.configs.recommended,
    // ...tseslint.configs.strictTypeChecked,
    //...tseslint.configs.stylisticTypeChecked

    {
        rules: {
            // '@typescript-eslint/no-explicit-any': 'off',
            // '@typescript-eslint/no-unused-vars': 'off',
            // '@typescript-eslint/no-var-requires': 'off',
            // '@typescript-eslint/explicit-module-boundary-types': 'off',
            // '@typescript-eslint/no-empty-function   ': 'off',
        }
    }
)
```


## Configs
- https://typescript-eslint.io/users/configs/
Recommended Configurations

We recommend that most projects should extend from one of:
    recommended: Recommended rules for code correctness that you can drop in without additional configuration.
    - `export default tseslint.config(...tseslint.configs.recommended);`
    recommended-type-checked: Contains recommended + additional recommended rules that require type information.
    - `export default tseslint.config(...tseslint.configs.recommendedTypeChecked);`
    strict: Contains recommended + additional strict rules that can also catch bugs but are more opinionated than recommended rules.
    - `export default tseslint.config(...tseslint.configs.strict);`
    strict-type-checked: Contains strict + additional strict rules require type information.
    - `export default tseslint.config(...tseslint.configs.strictTypeChecked);`


Additionally, we provide a stylistic config that enforces concise and consistent code. We recommend that most projects should extend from either:
    stylistic: Stylistic rules you can drop in without additional configuration.
     - `export default tseslint.config(...tseslint.configs.stylistic);`
    stylistic-type-checked: Contains stylistic + additional stylistic rules that require type information.
    - `export default tseslint.config(...tseslint.configs.stylisticTypeChecked);`


Notice that type-checked rules need additional settings:
- https://typescript-eslint.io/getting-started/typed-linting/
```typescript
import eslint from '@eslint/js';
import tseslint from 'typescript-eslint';

export default tseslint.config(
  eslint.configs.recommended,

  ...tseslint.configs.recommendedTypeChecked,
  {
    languageOptions: {
      parserOptions: {
        projectService: true,
        tsconfigRootDir: import.meta.dirname,
      },
    },
  },
);
```
- import.meta.dirname is only present for ESM files in Node.js >=20.11.0 / >= 21.2.0.
For CommonJS modules and/or older versions of Node.js, use __dirname or an alternative.
- **If your eslint.config.mjs getting a parsing error then add to your tsconfig.json at the include array `"**/*.mjs",`**








<br><br>
<br><br>

## Rules
- https://typescript-eslint.io/rules/

<br><br>

### no-explicit-any

Comment:
```javascript
/* eslint-disable  @typescript-eslint/no-explicit-any */
```




<br><br>

### unbound-method
- https://typescript-eslint.io/rules/unbound-method/
  
Comment:
```javascript
/* eslint-disable  @typescript-eslint/no-explicit-any */
```

#### Usage with statics
- There are cases e.g. when you create a singleton class with the getInstance method concept when eslint will trigger an error for unbound-method… There you can disable it with this riles
```javascript
// static getInstance() method using this
'@typescript-eslint/unbound-method': [
    'error',
    {
        'ignoreStatic': true
    }
]
```
```typescript
export default class ModelManager {
    // eslint-disable-next-line no-use-before-define
    private static instance: ModelManager | null = null

    /**
     * Private constructor to prevent direct instantiation.
     * Access is provided via the `getInstance` method.
     */
    private constructor() {}

    /**
     * Returns the singleton instance of the ModelManager.
     * Initializes the instance upon the first call.
     * @returns {Promise<ModelManager>} - The singleton instance of the ModelManager.
     */
    public static async getInstance(): Promise<ModelManager> {
        if (!this.instance) {
            this.instance = new ModelManager()
            await this.instance.init()
        }
        
        return this.instance
    }
}
```






























<br><br>
<br><br>
____________________________________________________
____________________________________________________
<br><br>
<br><br>

## Fix all files in project
```shell
eslint --fix .
```


















<br><br>
<br><br>
____________________________________________________
____________________________________________________
<br><br>
<br><br>


# eslint
- https://eslint.org/docs/latest/rules/

## .eslintrc

<br><br>

### Google
```javascript
{
    "extends": "google",
    "env": {
        "browser": false,
        "node": true,
        "es8": true,
        "mocha": false
    },
    "parserOptions": {
        "sourceType": "module",
        "requireConfigFile": false
    },
    "ecmaFeatures": {
        "arrowFunctions": true,
        "blockBindings": true,
        "classes": true,
        "defaultParams": true,
        "modules": true,
        "spread": true,
        "globalReturn": true
    },
    "rules": {
        "arrow-parens": ["error", "as-needed"],
        "valid-jsdoc": ["error", {
            "requireReturn": true,
            "requireReturnType": true,
            "requireParamDescription": true,
            "requireReturnDescription": true,
            "preferType": {
                "String": "string",
                "object": "Object"
            }
        }],
        "require-jsdoc": ["error", {
            "require": {
                "FunctionDeclaration": true,
                "MethodDefinition": true,
                "ClassDeclaration": true
            }
        }],
        "no-var": 1,
        "no-eval": "error",
        "indent": ["error", 4],
        "quotes": ["error", "single"],
        "no-console": "off",
        "space-before-function-paren": ["error", "never"],
        "padded-blocks": ["error", "never"],
        "prefer-arrow-callback": [0, { "allowNamedFunctions": true }],
        "func-names": ["error", "never"],
        "no-use-before-define": [
            "error", {
                "functions": true,
                "classes": true
            }
        ],
        "max-nested-callbacks": [
            "error",
            5
        ],
        "max-len": ["error", 120],
        "object-curly-spacing": 0,
        "comma-dangle": ["error", "never"],
        "semi": [2, "never"],
        "new-cap": 0,
        "one-var": 0,
        "guard-for-in": 0
    }
}
```

<br><br>


### Google and Babel
```javascript
{
    "extends": "google",
    "parser": "@babel/eslint-parser",
    "plugins": [
        ["@babel/plugin-transform-flow-strip-types"],
        ["@babel/plugin-proposal-decorators", { "legacy": true}],
        ["@babel/plugin-proposal-class-properties", { "loose": true}]
    ],
    "env": {
        "browser": false,
        "node": true,
        "es6": true,
        "mocha": false
    },
    "parserOptions": {
        "sourceType": "module",
        "requireConfigFile": false
    },
    "ecmaFeatures": {
        "arrowFunctions": true,
        "blockBindings": true,
        "classes": true,
        "defaultParams": true,
        "modules": true,
        "spread": true,
        "globalReturn": true
    },
    "rules": {
        "arrow-parens": ["error", "as-needed"],
        "valid-jsdoc": ["error", {
            "requireReturn": true,
            "requireReturnType": true,
            "requireParamDescription": true,
            "requireReturnDescription": true,
            "preferType": {
                "String": "string",
                "object": "Object"
            }
        }],
        "require-jsdoc": ["error", {
            "require": {
                "FunctionDeclaration": true,
                "MethodDefinition": true,
                "ClassDeclaration": true
            }
        }],
        "no-var": 1,
        "no-eval": "error",
        "indent": ["error", 4],
        "quotes": ["error", "single"],
        "no-console": "off",
        "space-before-function-paren": ["error", "never"],
        "padded-blocks": ["error", "never"],
        "prefer-arrow-callback": [0, { "allowNamedFunctions": true }],
        "func-names": ["error", "never"],
        "no-use-before-define": [
            "error", {
                "functions": true,
                "classes": true
            }
        ],
        "max-nested-callbacks": [
            "error",
            5
        ],
        "max-len": ["error", 120],
        "object-curly-spacing": 0,
        "comma-dangle": ["error", "never"],
        "semi": [2, "never"],
        "new-cap": 0,
        "one-var": 0,
        "guard-for-in": 0
    }
}
```
