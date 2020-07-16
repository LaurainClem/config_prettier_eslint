# Configuration (ESLint / Prettier)

Ci-dessous la liste des étapes pour installer ESLint et Prettier correctement avec l'intégration sur l'IDE VS Code.

Sources :
https://dev.to/chgldev/getting-prettier-eslint-and-vscode-to-work-together-3678
https://prettier.io/docs/en/index.html
https://eslint.org/docs/user-guide/getting-started

## Installation des extensions VS Code

Installer les extensions **EsLint** et **Prettier - Code formatter** et vérifier qu'il soit bien activés.

## Installation des dépendances

Les dépendances peuvent être installer sous forme de dépendances du projet avec la commande :
`npm i --save-dev eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-prettier eslint-plugin-prettier prettier`

**eslint-plugin-prettier**: Permet l'intégration de Prettier dans ESLint en tant que plugin de celui-ci.
**eslint-config-prettier**: Permet de désactiver dans ESLint les règles pouvant entrer en conflit avec Prettier.

## Intégrer Prettier à ESLint

Afin que **Pettier** ne rentre pas en conflit avec **ESLint** sur les règles de styles d'écriture du code (tabulation, virgule flottante, espacements, ... ) , il faudra configurer **ESLint** pour pas qu'il rentre en collision avec les règles défini dans **Prettier**, et rendre visible les erreurs de **Prettier**.

Créer un fichier nommé `.eslintrc` à la racine de votre projet avec le contenu ci-dessous.

```
{
	"root": true,
	"parser": "@typescript-eslint/parser",
	"extends": [
		"plugin:prettier/recommended",
		"plugin:@typescript-eslint/recommended",
		"prettier/@typescript-eslint",
		"plugin:prettier/recommended"
	],
	"plugins": ["@typescript-eslint", "prettier"],
	"rules": {
		"prettier/prettier": "error"
	}
}
```

La liste des règles n'est pas exhaustives, il est nécessaire de compléter celui-ci à votre convenance.
Cf: https://eslint.org/docs/user-guide/getting-started

Créer ensuite un fichier `.prettierrc` à la racine de votre projet avec le contenu ci-dessous.

```
{
	"semi": true,
	"singleQuote": true,
	"tabwidth": 4,
	"useTabs": true,
	"trailingComma": "all",
	"printWidth": 120
}
```

(Il s'agit ici de quelques règles basiques, à titre d'exemple. Elles sont évidement personnalisables et doivent être personnalisées à votre convenance.
Cf: https://prettier.io/docs/en/index.html

## Déclencher le formatage à la sauvegarde

Configurer la propriété `code Actions OnSave` de VS Code à vrai depuis l'interfaces des préférences, ou en ajoutant la ligne ci-dessous dans le fichier `settings.json`.
```
"editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
}
```
