# Colorer l'aperçu Markdown dans VS Code

## Le principe

Une ligne dans les réglages de VS Code et un fichier `markdown.css` dans chaque projet suffisent pour colorer l'aperçu Markdown : titres, texte et blocs de code.

## Étape 1 : déclarer la feuille de style, une seule fois

Ouvrez les réglages utilisateur depuis la palette (⇧⌘P) avec la commande « Preferences: Open User Settings (JSON) ». Sur Mac, ce fichier se trouve dans `~/Library/Application Support/Code/User/settings.json`.

Ajoutez cette ligne à l'intérieur des accolades existantes, sans créer de second bloc `{ }` :

```jsonc
"markdown.styles": [".vscode/markdown.css"]
```

Les entrées sont séparées par des virgules : la ligne qui précède doit donc se terminer par une virgule. Placez la vôtre au premier niveau, pas dans un bloc imbriqué comme `"[markdown]": { … }`.


## Étape 2 : ajouter le fichier CSS dans chaque projet

À la racine du projet, à côté du `.code-workspace`, créez un dossier `.vscode` contenant un fichier `markdown.css`.

Contenu du fichier :

```css
/* Couleurs des titres : changez directement les codes */
.vscode-body h1 { color: #6529cb; }
.vscode-body h2 { color: #135bae; }
.vscode-body h3 { color: #217b31; }
.vscode-body h4 { color: #ba5b1f; }
.vscode-body h5, .vscode-body h6 { color: #c92f2f; }
/* Le trait sous h1 et h2 prend la couleur du titre */
.vscode-body h1, .vscode-body h2 { border-bottom-color: currentColor; }

/* Texte */
.vscode-body :not(pre) > code { color: #79c0ff; }                        /* code en ligne */
.vscode-body strong, .vscode-body em { color: #c9d1d9; }                 /* gras, italique */
.vscode-body a { color: #a5d6ff; }                                       /* liens */
.vscode-body blockquote { color: #7ee787; border-left-color: #7ee787; }  /* citations */
.vscode-body li::marker { color: #ffa657; }                              /* puces et numéros */

/* Blocs de code : correspondance approximative avec l'éditeur */
.vscode-body .hljs-comment { color: #8b949e; }                           /* commentaires */
.vscode-body .hljs-keyword { color: #ff7b72; }                           /* mots-clés (if, then…) */
.vscode-body .hljs-string { color: #a5d6ff; }                            /* chaînes */
.vscode-body .hljs-number,
.vscode-body .hljs-literal,
.vscode-body .hljs-built_in { color: #79c0ff; }                          /* nombres, true/false, commandes intégrées */
.vscode-body .hljs-title { color: #d2a8ff; }                             /* noms de fonctions */
.vscode-body .hljs-variable { color: #c9d1d9; }                          /* variables ($HOME…) */
.vscode-body .hljs-attr { color: #7ee787; }                              /* clés JSON et YAML */
.vscode-body .hljs-type { color: #ffa657; }                              /* types */
```

Le fichier a trois parties. Les titres ont des couleurs choisies librement ; le texte et les blocs de code reprennent celles de l'éditeur (thème Dark 2026).

Pour changer une couleur, remplacez son code sur la ligne concernée.

## Étape 3 : vérifier dans l'aperçu

Ouvrez un fichier `.md` du projet, puis son aperçu : ⇧⌘V, ou ⌘K puis V pour l'afficher à côté de l'éditeur. Les titres doivent apparaître en couleur.

Si une modification n'apparaît pas, lancez « Markdown: Refresh Preview » depuis la palette.
