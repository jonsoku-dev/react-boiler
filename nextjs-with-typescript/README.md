## Getting started

```shell
yarn add --dev eslint prettier eslint-plugin-react eslint-plugin-react-hooks eslint-config-prettier eslint-plugin-prettier eslint-plugin-jsx-a11y
```

### .eslintrc.js .prettierrc

```shell
touch .eslintrc.js .prettierrc
```

### .eslintignore and .prettierignore

```shell
touch .eslintignore .prettierignore
```

Just add the follwing to both files

```shell
node_modules
```

### .prettierrc

```shell
{
    "semi": true,
    "tabWidth": 4,
    "printWidth": 100,
    "singleQuote": true,
    "trailingComma": "none",
    "jsxBracketSameLine": true
}
```

### .eslintrc.js

```js
module.exports = {
    root: true,                 // Make sure eslint picks up the config at the root of the directory
    parserOptions: {
        ecmaVersion: 2020,      // Use the latest ecmascript standard
        sourceType: 'module',   // Allows using import/export statements
        ecmaFeatures: {
            jsx: true           // Enable JSX since we're using React
        }
    },
    settings: {
        react: {
            version: 'detect'   // Automatically detect the react version
        }
    },
    env: {
        browser: true,          // Enables browser globals like window and document
        amd: true,              // Enables require() and define() as global variables as per the amd spec.
        node: true              // Enables Node.js global variables and Node.js scoping.
    },
    extends: [
        'eslint:recommended',
        'plugin:react/recommended',
        'plugin:jsx-a11y/recommended',
        'plugin:prettier/recommended' // Make this the last element so prettier config overrides other formatting rules
    ],
    rules: {
        'prettier/prettier': ['error', {}, {usePrettierrc: true}]  // Use our .prettierrc file as source
    }
};
```

## Running ESlint

You need to add the script to your `package.json` file.

```json
  "scripts": {
"lint": "eslint --fix .",
"format": "prettier --write './**/*.{js,jsx,ts,tsx,css,md,json}' --config ./.prettierrc"
},
```

## Targeting Next.js

### .eslint.js 에 규칙추가

```shell
{
    rules: {
        'react/react-in-jsx-scope': 'off',
        'jsx-a11y/anchor-is-valid': [
            'error',
            {
                components: ['Link'],
                specialLink: ['hrefLeft', 'hrefRight'],
                aspects: ['invalidHref', 'preferButton']
            }
        ]
    }
}
```

## Targeting TypeScript

```shell
yarn add --dev @typescript-eslint/eslint-plugin @typescript-eslint/parser
```

### Finally

```js
module.exports = {
    root: true,
    parser: '@typescript-eslint/parser',
    parserOptions: {
        ecmaVersion: 2020,
        sourceType: 'module',
        ecmaFeatures: {
            jsx: true
        }
    },
    settings: {
        react: {
            version: 'detect'
        }
    },
    env: {
        browser: true,
        amd: true,
        node: true
    },
    extends: [
        'eslint:recommended',
        'plugin:@typescript-eslint/eslint-recommended',
        'plugin:@typescript-eslint/recommended',
        'plugin:react/recommended',
        'plugin:jsx-a11y/recommended',
        'prettier/@typescript-eslint',
        'plugin:prettier/recommended'   // Make sure this is always the last element in the array.
    ],
    rules: {
        'prettier/prettier': ['error', {}, {usePrettierrc: true}],
        'react/react-in-jsx-scope': 'off',
        'react/prop-types': 'off',
        '@typescript-eslint/explicit-function-return-type': 'off',
        'simple-import-sort/sort': 'error',
        'jsx-a11y/anchor-is-valid': [
            'error',
            {
                components: ['Link'],
                specialLink: ['hrefLeft', 'hrefRight'],
                aspects: ['invalidHref', 'preferButton']
            }
        ]
    }
};
```

## import sort

```shell
yarn add --dev eslint-plugin-simple-import-sort
```

Update your .eslintrc.js file to make use of this plugin. Add a top level property plugins.

```js
module.exports = {
  plugins: [
    'simple-import-sort'
  ]
};
```

## husky + lint-staged
```shell
yarn add --dev husky@4 lint-staged
```
Now in your `package.json` add the following at the top level.
```json
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "./**/*.{js,jsx,ts,tsx}": [
      "eslint --fix",
    ]
  }
}
```

# ENV
https://github.com/vercel/next.js/tree/canary/examples/environment-variables
```shell
touch .env .env.development .env.production .env.local .env.development.local .env.production.local
```