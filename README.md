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


# Plugins

```
import eslint from '@eslint/js'
import importPlugin from 'eslint-plugin-import'
import a11yPlugin from 'eslint-plugin-jsx-a11y'
import reactPlugin from 'eslint-plugin-react'
import reactHooksPlugin from 'eslint-plugin-react-hooks'
// https://github.com/eslint-stylistic/eslint-stylistic
import stylistic from '@stylistic/eslint-plugin'
import tseslint from 'typescript-eslint'
// https://github.com/sindresorhus/eslint-plugin-unicorn
import eslintPluginUnicorn from 'eslint-plugin-unicorn'
// https://github.com/eslint-community/eslint-plugin-n
import nodePlugin from 'eslint-plugin-n'
// https://www.npmjs.com/package/eslint-plugin-security
import pluginSecurity from 'eslint-plugin-security'
// https://www.npmjs.com/package/eslint-plugin-sonarjs
import sonarjs from 'eslint-plugin-sonarjs'
// https://www.npmjs.com/package/eslint-plugin-promise
import pluginPromise from 'eslint-plugin-promise'
```

<br><br>

## eslint-plugin-prefer-arrow-functions
- Diese Regel ist nicht konform mit TypeScript, weil der Autofix dieser Regel normale Funktionen nach Error-Funktionen setzt. Wenn man die Named-Function-Option auf True setzt, hätte laut KI dieses ESLint-Plugin keinen Sinn mehr. Daher macht es keinen Sinn, es in einer TypeScript-Umgebung zu benutzen, nur in einer normalen Node.js-Umgebung. Macht laut KI auch keinen Sinn für ein reines Node.js-Projekt, da es dann mit Hosting im Enterprise-Grade-Umfeld konfliktiert.

<br><br>


## eslint-plugin-boundarie

<br><br>

## eslint-plugin-jsdoc
- Dieses Plug-In **MUSS** man nicht wirklich in einem TypeScript-Projekt verwenden, wo TS-Docs verwendet werden.
https://www.npmjs.com/package/eslint-plugin-jsdoc

<br><br>

## eslint-plugin-xss
- **not eslint 9 compatibel**
```

// ⚠️ INCOMPATIBLE WITH ESLINT 9 - DO NOT USE
// eslint-plugin-xss uses deprecated APIs (getComments) removed in ESLint 9
/*
 * Last updated: 2019 - NOT MAINTAINED
 * Alternative: Use eslint-plugin-security for XSS prevention
 * https://www.npmjs.com/package/eslint-plugin-xss
 * import eslintPluginXss from 'eslint-plugin-xss'
 */
```


<br><br>






## Module boundaries 
- https://sheriff.softarc.io/docs/introduction


## file formats

### markdown

#### eslint-markdown
- https://github.com/eslint/markdown
  - no support for eslint 9 yet

- eslint-plugin-markdownlint
  - no support for eslint 9 yet 


<br><br>

## Browser
- https://www.npmjs.com/package/eslint-plugin-compat


<br><br>

## Testing

### Jest
- https://www.npmjs.com/package/eslint-plugin-jest

### testing-library
eslint-plugin-testing-library

### Vitest
eslint-plugin-vitest

### Mocha
eslint-plugin-mocha




## Sorting

### eslint-plugin-typescript-sort-keys
- **Not needed because sorting enums and interfaces has to many not wanted side effects**

























<br><br>
<br><br>
____________________________________________________
____________________________________________________
<br><br>
<br><br>

# Typescript eslint
- https://github.com/CyberT33N/typescript-eslint-cheat-sheet/blob/main/README.md




























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
