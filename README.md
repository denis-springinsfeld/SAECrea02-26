# Full Site Editing FSE et thèmes Gutenberg

Le **Full site editing** (L'édition complète du site), FSE en abrégé, désigne un ensemble de fonctionnalités WordPress qui permettent d'utiliser des **blocs Gutenberg** pour toutes les parties d'un site web, et pas seulement pour le contenu. Cela inclut les en-têtes, les pieds de page, les modèles de page, et plus encore. Cette fonctionnalité offre une manière plus intuitive et flexible de créer et de gérer les mises en page, les thèmes et le contenu d'un site web sans avoir besoin d'écrire de code.

On parlera de **thèmes Gutenberg** ou **Block Themes** pour désigner les thèmes WordPress qui sont conçus pour tirer parti du Full Site Editing. Ces thèmes sont construits à l'aide de blocs et de modèles de blocs, ce qui permet aux utilisateurs de personnaliser facilement leur site en utilisant l'éditeur de blocs de WordPress.

Exemple de thèmes compatible FSE : Twenty Twenty-Five

## A Plan

### A.1 Objectif

Créer un thème WordPress : Block Theme.

### A.2 Prérequis

- Avoir une installation de WordPress fonctionnelle sur WAMP ou sur le serveur Tpmmi

### A.3 Étapes

1. Créer un thème WordPress
2. Ajouter des styles globaux
3. Ajouter des variations de styles
4. Ajouter des modèles de page
5. Ajouter des parties de modèles
6. Ajouter des compositions
7. Ajouter des options
8. Exporter le thème
9. Importer le thème
10. Tester le thème

### A.4 Ressources

https://developer.wordpress.org/themes/

- [Création d'un thème WordPress](https://developer.wordpress.org/themes/basics/)
- [Styles globaux](https://developer.wordpress.org/themes/global-settings-and-styles/)
- [Variations de styles](https://developer.wordpress.org/themes/global-settings-and-styles/style-variations/)
- [Modèles de page (Templates)](https://developer.wordpress.org/themes/templates/)
- [Parties de modèles (Template Parts)](https://developer.wordpress.org/themes/templates/template-parts/)
- [Compositions (Patterns)](https://developer.wordpress.org/themes/features/block-patterns/)
- [Options et settings](https://developer.wordpress.org/themes/global-settings-and-styles/settings/)
- [Exporter le thème](https://developer.wordpress.org/themes/tools/create-block-theme/)
- [Tester le thème](https://developer.wordpress.org/themes/advanced-topics/theme-testing/)

---

## Installation sur Wamp en R04 uniquement

- télécharger wordpress v.6.9.1 (www.wordpress.org)
- Déposer le dossier dans `C:wamp64/www/`
- Cliquer sur StartWamp sur le bureau
- Ouvrir le navigateur et aller sur `http://localhost`
- Cliquer sur phpmyadmin
- Créer une base de données (phpmyadmin) - login: "root", mdp: ""
- Lancer l'installation de wordpress

---

## B. Réalisation d'un thème Block FSE

➡️ Dans le dossier `wp-content/themes/`, créez un nouveau dossier pour votre thème, par exemple `mon-theme`. Ce dossier contiendra tous les fichiers nécessaires pour votre thème.

📖 [Voir la documentation complète : A-Theme-Gutenberg](../../wiki/A-Theme-Gutenberg)

### B.1 Étape 1 : Créez le dossier du thème, les fichiers `style.css` et `index.html`

```bash
/mon-theme
    ├── style.css
    └── templates/
        └── index.html

```

Les fichiers minimum requis sont un fichier `style.css` et un `index.html`. Ce dernier doit être placé dans un dossier appelé `templates`.

#### B.1.1 style.css

➡️ Ajouter un fichier `style.css`. Celui-ci doit contenir un en-tête minimal et peut rester vide pour l'instant. L'en-tête doit inclure au moins le nom du thème pour que WordPress puisse le reconnaître.:

```css
/*
Theme Name: Mon Theme
Author: Votre Nom
Version: 1.0
*/
```

Remarque si vous allez dans l'administration de WordPress, puis dans `Apparence > Thèmes`, votre thème "Mon Theme" n'apparaît pas encore dans la liste. Pour l'instant il n'est pas encore fonctionnel, vous devriez voir un message "Broken Theme".

#### B.1.2 Ajoutez votre premier modèle de page (template)

Les **templates** (ou modèle de page) sont des fichiers HTML qui définissent la structure d'une page.

> [!TIP]
> [ref template-hierarchy](https://developer.wordpress.org/themes/basics/template-hierarchy/)

➡️ Ajouter un fichier `index.html` dans un dossier `templates`, pour rendre votre thème opérationnel. Ce fichier pour l'instant peut rester vide, mais il doit être présent pour que WordPress puisse reconnaître le thème.

➡️ Vous pouvez à présent activer votre thème dans l'interface d'administration de WordPress. Vous pouvez regarder votre site, il s'affiche, mais il est vide, car le modèle de page ne contient aucun bloc.

---

### B.2 Étape 2 : Ajouter des styles globaux - `theme.json`

Le `theme.json` est le fichier le plus important des thèmes modernes WordPress, car c’est via celui-ci que l’on va configurer notre design system dans l’éditeur, à savoir les couleurs, polices, espacements… Il va également nous permettre d’**activer ou désactiver des fonctionnalités de l’éditeur**, et définir les **styles par défaut du site**.

#### B.2.1 Créer le fichier theme.json

➡️ Ajouter un fichier `theme.json` à la racine de votre thème.
Voici une version minimale du fichier `theme.json` pour notre thème:

```json
{
  "$schema": "https://schemas.wp.org/wp/6.9/theme.json",
  "version": 3,
  "settings": {},
  "styles": {}
}
```

Anatomie du fichier `theme.json` :

- **$schema**: L'URL du schéma JSON pour l'autocomplétion (e.g. VS Code) et la validation.
  - _Recommandé_ : `https://schemas.wp.org/wp/6.7/theme.json` (ou votre version actuelle) pour cibler une version spécifique et stable de WordPress.
  - _Alternatif_ : `https://schemas.wp.org/trunk/theme.json` pour utiliser les dernières fonctionnalités expérimentales si l'extension Gutenberg (Beta) est active.
- **version**: La version du format theme.json utilisé.

- **settings**: Un objet contenant les paramètres globaux du thème, tels que les options de mise en page, les couleurs, les polices, etc. Configure ce qui est possible et disponible dans l'éditeur Gutenberg
- **styles**: Un objet définissant les styles globaux du thème, comme les couleurs, les polices, les espacements, etc.

Il existe d'autres propriétés optionnelles que vous découvrirez plus tard, comme `templates`, `templateParts`, `patterns` et `options`.

> [!TIP]
> [Theme Settings and Styles](https://developer.wordpress.org/themes/global-settings-and-styles/)

#### B.2.2 `settings` et paramètre globaux du thème

Les paramètres globaux du thème sont définis dans la propriété `settings` du fichier `theme.json`. Cela permet de configurer les options disponibles dans l'éditeur Gutenberg, comme les couleurs, les polices, les espacements, etc. Mais également les fonctionnalités à activer ou désactiver dans Gutenberg.

> [!TIP]
> [settings](https://developer.wordpress.org/themes/global-settings-and-styles/settings/)

➡️ Testez cette configuration dans votre fichier `theme.json` pour voir les changements dans l'éditeur Gutenberg uniquement pour l'instant, votre site ne change pas encore, car nous n'avons pas encore défini les styles globaux du thème.

```json
{
  "$schema": "https://schemas.wp.org/wp/6.9/theme.json",
  "version": 3,
  "settings": {
    // Fonctionnalités de l'éditeur
    "appearanceTools": false,
    "color": {
      // Fonctionnalités de l'éditeur
      "defaultPalette": false,
      "custom": false,

      // Palettes de couleurs
      "palette": [
        {
          "name": "Primary",
          "slug": "primary",
          "color": "#0073aa"
        },
        {
          "name": "Secondary",
          "slug": "secondary",
          "color": "#005177"
        },
        {
          "name": "Accent",
          "slug": "accent",
          "color": "#d54e21"
        }
      ]
    }
  },
  "styles": {
    "color": {
      "background": "var(--wp--preset--color--primary)",
      "text": "var(--wp--preset--color--secondary)"
    }
  }
}
```

- les instructions booléennes permettant d’activer ou de désactiver les options de couleur dans l’éditeur Gutenberg.

- on déclare ensuite la liste des couleurs de la palette que l’on va proposer sur le site.

Voici une vision des paramètre que `settings` peut contenir :

```json
{
  "$schema": "https://schemas.wp.org/wp/6.9/theme.json",
  "version": 3,
  "settings": {
    "appearanceTools": true,
    "color": {},
    "layout": {},
    "typography": {},
    "spacing": {},
    "border": {},
    "custom": {}
  }
}
```

#### B.2.3 `styles` et utilisation des variables de thème

Une fois les paramètres globaux définis dans `settings`, vous pouvez les utiliser pour appliquer des styles globaux à votre thème via la propriété `styles`.

> [!TIP]
> [styles](https://developer.wordpress.org/themes/global-settings-and-styles/styles/)

Par exemple, pour appliquer la couleur de la palette "primary" en tant que couleur de fond globale du site, vous pouvez faire ceci :

```json
{
  "styles": {
    "color": {
      "background": "var(--wp--preset--color--primary)"
      "text": "var(--wp--preset--color--secondary)"
    }
  }
}
```

##### Explication sur la création des variables et des classes CSS à partir des paramètres globaux du thème

Lorsque vous définissez des paramètres globaux dans la section `settings` de votre fichier `theme.json`, WordPress génère automatiquement des variables CSS personnalisées et des classes CSS basées sur ces paramètres. Cela permet d'utiliser facilement les valeurs définies dans `settings` pour styliser votre thème.

Par exemple, si vous définissez une palette de couleurs dans `settings.color.palette` comme ceci :

```json
"settings": {
  "color": {
    "palette": [
      {
        "name": "Primary",
        "slug": "primary",
        "color": "#0073aa"
      },
      {
        "name": "Secondary",
        "slug": "secondary",
        "color": "#005177"
      },
      {
        "name": "Accent",
        "slug": "accent",
        "color": "#d54e21"
      }
    ]
  }
```

WordPress va automatiquement créer des **variables CSS personnalisées** pour chaque couleur de la palette, avec le format suivant :

```css
--wp--preset--{preset-category}--{preset-slug}
```

Dans notre exemple, les variables CSS générées seraient :

```css
--wp--preset--color--primary: #0073aa;
--wp--preset--color--secondary: #005177;
--wp--preset--color--accent: #d54e21;
```

De plus, WordPress génère également des **classes utilitaires CSS** pour chaque couleur de la palette, avec le format suivant :

```css
.has-{preset-slug}-color
```

Dans notre exemple, les classes CSS générées seraient :

```css
.has-primary-color {
  color: var(--wp--preset--color--primary);
}
.has-secondary-color {
  color: var(--wp--preset--color--secondary);
}
.has-accent-color {
  color: var(--wp--preset--color--accent);
}
```

##### Exercice : paramétrer et utiliser les styles globaux typographiques

➡️ Testez cette méthode pour paraméter les styles globaux typographique en utilisant une police personnalisée, et utilisez les variables CSS générées pour appliquer cette police à votre thème.

> [!TIP]
> [Typography](https://developer.wordpress.org/themes/global-settings-and-styles/typography/#font-families)

Vous devrez surement créer un dossier `assets` pour y placer votre fichier de police, et ensuite le déclarer dans `theme.json` :

```json
{
  "settings": {
    "typography": {
      "fontFamilies": [
        {
          "name": "Custom Font",
          "slug": "custom-font",
          "fontFace": [
            {
              "fontFamily": "Custom Font",
              "src": "url(../assets/fonts/custom-font.woff2) format('woff2')"
            }
          ]
        }
      ]
    }
  },
  "styles": {
    "typography": {
      "fontFamily": "var(--wp--preset--typography--custom-font)"
    }
  }
}
```

##### Style et Paramétrage des éléments (elements)

La propriété `elements` dans `styles` permet de styliser des **éléments HTML globalement** sur tout le site. Par exemple, tous les liens `<a>` ou tous les boutons `<button>`.

> [!TIP]
> [Elements](https://developer.wordpress.org/themes/global-settings-and-styles/styles/#elements)

**Éléments disponibles :** `link`, `button`, `heading`, `h1` à `h6`, `caption`, `cite`

➡️ Exemple simple pour styliser les liens et boutons :

```json
{
  "styles": {
    "elements": {
      "link": {
        "color": {
          "text": "#d54e21"
        },
        ":hover": {
          "color": {
            "text": "#0073aa"
          }
        }
      },
      "button": {
        "color": {
          "background": "#0073aa",
          "text": "#ffffff"
        },
        ":hover": {
          "color": {
            "background": "#005177"
          }
        }
      }
    }
  }
}
```

> **Note** : `elements.button` cible l'élément HTML `<button>` de manière globale. Pour styliser le **bloc Bouton** de Gutenberg (`core/button`), utilisez `styles.blocks`.

##### Style et Paramétrage des blocs (blocks)

La propriété `blocks` permet de personnaliser des **blocs Gutenberg spécifiques**. Nous allons voir toutes les possibilités avec le bloc **Bouton** (`core/button`).

> [!TIP]
> [Blocks](https://developer.wordpress.org/themes/global-settings-and-styles/styles/#blocks)

###### Style par défaut du bloc Bouton

➡️ Définissez le style par défaut de tous les boutons :

```json
{
  "styles": {
    "blocks": {
      "core/button": {
        "color": {
          "background": "#0073aa",
          "text": "#ffffff"
        },
        "border": {
          "radius": "4px"
        },
        "typography": {
          "fontSize": "1rem",
          "fontWeight": "600"
        },
        "spacing": {
          "padding": {
            "top": "10px",
            "right": "20px",
            "bottom": "10px",
            "left": "20px"
          }
        }
      }
    }
  }
}
```

###### Restreindre les options du bloc dans l'éditeur

Dans `settings.blocks`, vous pouvez limiter les couleurs disponibles pour le bloc Bouton :

```json
{
  "settings": {
    "blocks": {
      "core/button": {
        "color": {
          "custom": false,
          "palette": [
            { "name": "Bleu", "slug": "bleu", "color": "#0073aa" },
            { "name": "Rouge", "slug": "rouge", "color": "#d54e21" },
            { "name": "Blanc", "slug": "blanc", "color": "#ffffff" }
          ]
        }
      }
    }
  }
}
```

Avec `"custom": false`, l'utilisateur ne pourra choisir que parmi ces 3 couleurs dans l'éditeur.

##### B.2.7.3 Variations de style du bloc Bouton

Le bloc Bouton supporte des **variations de style** (style variations) que vous pouvez personnaliser. Les deux variations natives sont :

- `fill` : bouton plein (par défaut)
- `outline` : bouton avec contour uniquement

➡️ Personnalisez chaque variation dans `styles.blocks` :

```json
{
  "styles": {
    "blocks": {
      "core/button": {
        "variations": {
          "fill": {
            "color": {
              "background": "#0073aa",
              "text": "#ffffff"
            },
            "border": {
              "radius": "4px",
              "width": "0"
            }
          },
          "outline": {
            "color": {
              "background": "transparent",
              "text": "#0073aa"
            },
            "border": {
              "color": "#0073aa",
              "width": "2px",
              "style": "solid",
              "radius": "4px"
            }
          }
        }
      }
    }
  }
}
```

##### B.2.7.4 Exemple complet pour le bloc Bouton

Voici un exemple complet combinant style par défaut, restrictions et variations :

```json
{
  "$schema": "https://schemas.wp.org/wp/6.9/theme.json",
  "version": 3,
  "settings": {
    "color": {
      "custom": false,
      "palette": [
        { "name": "Primary", "slug": "primary", "color": "#0073aa" },
        { "name": "Secondary", "slug": "secondary", "color": "#005177" },
        { "name": "Accent", "slug": "accent", "color": "#d54e21" },
        { "name": "White", "slug": "white", "color": "#ffffff" }
      ]
    }
  },
  "styles": {
    "blocks": {
      "core/button": {
        "border": {
          "radius": "8px"
        },
        "typography": {
          "fontWeight": "600",
          "textTransform": "uppercase",
          "letterSpacing": "0.05em"
        },
        "variations": {
          "fill": {
            "color": {
              "background": "var(--wp--preset--color--primary)",
              "text": "var(--wp--preset--color--white)"
            }
          },
          "outline": {
            "color": {
              "background": "transparent",
              "text": "var(--wp--preset--color--primary)"
            },
            "border": {
              "color": "var(--wp--preset--color--primary)",
              "width": "2px",
              "style": "solid"
            }
          },
          "danger": {
            "color": {
              "background": "var(--wp--preset--color--accent)",
              "text": "var(--wp--preset--color--white)"
            },
            "border": {
              "color": "var(--wp--preset--color--accent)",
              "width": "0"
            }
          }
        }
      }
    }
  }
}
```

➡️ Testez ce code dans votre `theme.json`. Dans l'éditeur Gutenberg, ajoutez un bloc Bouton et changez son style entre "Remplissage" (fill) et "Contour" (outline) dans le panneau de droite.

---

#### B.2.4 Variations de styles personnalisées

Les **variations de styles** permettent de proposer différentes déclinaisons visuelles de votre thème (mode sombre, couleurs alternatives, etc.) sans créer un nouveau thème.

##### Créer le dossier `styles`

➡️ Créez un dossier `styles` à la racine de votre thème :

```bash
/mon-theme
    ├── style.css
    ├── theme.json
    ├── styles/
    │   └── dark.json
    └── templates/
        └── index.html
```

##### Créer une variation de style globale

➡️ Créez un fichier `dark.json` dans le dossier `styles` pour proposer un mode sombre :

```json
{
  "$schema": "https://schemas.wp.org/wp/6.7/theme.json",
  "version": 3,
  "title": "Mode Sombre",
  "settings": {
    "color": {
      "palette": [
        {
          "name": "Primary",
          "slug": "primary",
          "color": "#1a1a2e"
        },
        {
          "name": "Secondary",
          "slug": "secondary",
          "color": "#e0e0e0"
        },
        {
          "name": "Accent",
          "slug": "accent",
          "color": "#ff6b6b"
        }
      ]
    }
  },
  "styles": {
    "color": {
      "background": "var(--wp--preset--color--primary)",
      "text": "var(--wp--preset--color--secondary)"
    }
  }
}
```

➡️ Dans l'administration WordPress, allez dans `Apparence > Éditeur > Styles` et vous verrez la variation "Mode Sombre" disponible.

##### Créer des variations de styles pour les blocs

Vous pouvez également créer des variations de styles spécifiques à certains blocs (ex: boutons).

➡️ Créez un fichier `button-danger.json` dans `styles/` :

```json
{
  "$schema": "https://schemas.wp.org/wp/6.9/theme.json",
  "version": 3,
  "title": "Bouton Danger",
  "slug": "danger",
  "blockTypes": ["core/button"],
  "styles": {
    "color": {
      "background": "var(--wp--preset--color--accent) ",
      "text": "var(--wp--preset--color--white)"
    },
    "border": {
      "color": "currentColor",
      "width": "2px",
      "style": "solid"
    }
  }
}
```

---

### B.3 Étape 3 : Grammaire des blocs et création de templates

Pour ajouter du contenu à vos fichiers de templates (`.html`), il faut comprendre la **grammaire des blocs** WordPress. Les blocs sont définis par des **commentaires HTML** avec une syntaxe spécifique.

ref : https://developer.wordpress.org/themes/templates/

#### B.3.1 Syntaxe de base

Un bloc WordPress utilise cette structure :

```html
<!-- wp:nom-du-bloc {"attributs":"valeurs"} -->
Contenu du bloc
<!-- /wp:nom-du-bloc -->
```

- `wp:` : préfixe obligatoire
- `nom-du-bloc` : identifiant du bloc (ex: `paragraph`, `heading`, `button`)
- `{"attributs"}` : objet JSON optionnel pour les paramètres
- Contenu : le HTML affiché
- `<!-- /wp:nom-du-bloc -->` : balise de fermeture

#### B.3.2 Blocs auto-fermants

Certains blocs n'ont pas de contenu et se ferment directement :

```html
<!-- wp:site-title /-->
<!-- wp:post-date /-->
<!-- wp:spacer {"height":"50px"} /-->
```

#### B.3.3 Exemples de blocs courants

**Paragraphe :**

```html
<!-- wp:paragraph -->
<p>Ceci est un paragraphe.</p>
<!-- /wp:paragraph -->
```

**Titre :**

```html
<!-- wp:heading {"level":2} -->
<h2 class="wp-block-heading">Mon titre</h2>
<!-- /wp:heading -->
```

**Bouton :**

```html
<!-- wp:button -->
<div class="wp-block-button">
  <a class="wp-block-button__link wp-element-button" href="#">Cliquez ici</a>
</div>
<!-- /wp:button -->
```

**Image :**

```html
<!-- wp:image {"id":123,"sizeSlug":"large"} -->
<figure class="wp-block-image size-large">
  <img src="image.jpg" alt="Description" class="wp-image-123" />
</figure>
<!-- /wp:image -->
```

Autres blocs utiles pour les templates :

```html
<!-- wp:query -->
correspond à un bloc boucle de requête.
<!-- wp:post-title /-->
correspond à un bloc titre.
<!-- wp:post-excerpt /-->
correspond à un bloc résumé.
<!-- wp:post-date /-->
correspond à un bloc date.
<!-- wp:spacer -->
correspond à un bloc saut de ligne.
<!-- wp:query-pagination -->
correspond à un bloc pagination.
```

#### B.3.4 Blocs imbriqués

Les blocs peuvent contenir d'autres blocs :

```html
<!-- wp:group {"layout":{"type":"constrained"}} -->
<div class="wp-block-group">
  <!-- wp:heading {"level":1} -->
  <h1 class="wp-block-heading">Titre principal</h1>
  <!-- /wp:heading -->

  <!-- wp:paragraph -->
  <p>Un paragraphe de texte.</p>
  <!-- /wp:paragraph -->
</div>
<!-- /wp:group -->
```

**Groupe de boutons :**

```html
<!-- wp:buttons {"layout":{"type":"flex","justifyContent":"center"}} -->
<div class="wp-block-buttons">
  <!-- wp:button -->
  <div class="wp-block-button">
    <a class="wp-block-button__link wp-element-button">Bouton 1</a>
  </div>
  <!-- /wp:button -->

  <!-- wp:button {"className":"is-style-outline"} -->
  <div class="wp-block-button is-style-outline">
    <a class="wp-block-button__link wp-element-button">Bouton 2</a>
  </div>
  <!-- /wp:button -->
</div>
<!-- /wp:buttons -->
```

#### B.3.5 Attributs courants

| Attribut          | Description                   | Exemple                                  |
| ----------------- | ----------------------------- | ---------------------------------------- |
| `className`       | Classes CSS personnalisées    | `{"className":"ma-classe"}`              |
| `style`           | Styles inline                 | `{"style":{"color":{"text":"#ff0000"}}}` |
| `backgroundColor` | Couleur de fond (preset)      | `{"backgroundColor":"primary"}`          |
| `textColor`       | Couleur de texte (preset)     | `{"textColor":"white"}`                  |
| `fontSize`        | Taille de police (preset)     | `{"fontSize":"large"}`                   |
| `align`           | Alignement                    | `{"align":"wide"}` ou `{"align":"full"}` |
| `layout`          | Configuration de mise en page | `{"layout":{"type":"flex"}}`             |

#### B.3.6 Utiliser les presets du theme.json

Les couleurs et tailles définies dans `theme.json` s'utilisent directement :

```html
<!-- wp:paragraph {"backgroundColor":"primary","textColor":"white"} -->
<p
  class="has-primary-background-color has-white-color has-text-color has-background"
>
  Texte avec couleurs du thème
</p>
<!-- /wp:paragraph -->
```

#### B.3.7 Astuce : Copier depuis l'éditeur

Pour obtenir le balisage correct d'un bloc :

1. Créez le bloc dans l'éditeur Gutenberg
2. Cliquez sur les 3 points du bloc → **Copier le bloc**
3. Collez dans un éditeur de texte pour voir le code

Ou utilisez l'**éditeur de code** (Ctrl+Shift+Alt+M) pour voir le balisage de tous les blocs.

---

### B.4 Étape 4 : Ajouter des parts de modèles (template parts)

Les **template parts** (parties de modèles) sont des sections réutilisables d'un template, comme un en-tête, un pied de page ou une barre latérale. Elles permettent de structurer votre thème de manière modulaire.

ref : https://developer.wordpress.org/themes/templates/template-parts/

#### B.4.1 Structure du dossier parts

➡️ Créez un dossier `parts` à la racine de votre thème :

```bash
/mon-theme
    ├── style.css
    ├── theme.json
    ├── parts/
    │   ├── header.html
    │   └── footer.html
    └── templates/
        └── index.html
```

#### B.4.2 Créer l'en-tête (header)

➡️ Créez le fichier `parts/header.html` :

```html
<!-- wp:paragraph -->
<p>C'est mon Header !</p>
<!-- /wp:paragraph -->
```

#### B.4.2b Méthode alternative : Créer le header via l'éditeur WordPress

Vous pouvez aussi créer votre header **visuellement** dans l'éditeur WordPress, puis copier le code généré dans votre thème.

➡️ **Étapes :**

1. **Ouvrir l'éditeur de site**
   - Allez dans `Apparence > Éditeur`
   - Cliquez sur `Modèles de blocs` (ou `Template Parts`)
   - Sélectionnez `En-tête` (Header)

2. **Construire le header visuellement**
   - Ajoutez un bloc **Groupe** (pour contenir le header)
   - Dans ce groupe, ajoutez un bloc **Rangée** (Row) pour aligner les éléments
   - Insérez le bloc **Titre du site** (`Site Title`)
   - Insérez le bloc **Navigation**
   - Configurez l'alignement via les options du bloc Rangée (espace entre les éléments)

3. **Passer en mode Code**
   - Cliquez sur les **3 points verticaux** (⋮) en haut à droite de l'éditeur
   - Sélectionnez **Éditeur de code** (ou utilisez le raccourci `Ctrl+Shift+Alt+M`)
   - Vous verrez le balisage des blocs généré automatiquement

4. **Copier le code**
   - Sélectionnez tout le code affiché (`Ctrl+A`)
   - Copiez-le (`Ctrl+C`)

5. **Coller dans votre thème**
   - Ouvrez le fichier `parts/header.html` de votre thème
   - Collez le code (`Ctrl+V`)
   - Sauvegardez le fichier

➡️ **Exemple de code obtenu :**

```html
<!-- wp:group {"layout":{"type":"constrained"}} -->
<div class="wp-block-group">
  <!-- wp:group {"layout":{"type":"flex","flexWrap":"nowrap","justifyContent":"space-between"}} -->
  <div class="wp-block-group">
    <!-- wp:site-title {"level":0} /-->
    <!-- wp:navigation {"ref":123,"layout":{"type":"flex","justifyContent":"right"}} /-->
  </div>
  <!-- /wp:group -->
</div>
<!-- /wp:group -->
```

> **Note** : Le bloc Navigation peut contenir un attribut `"ref":123` qui fait référence à un menu enregistré en base de données. Pour un thème portable, vous pouvez supprimer cet attribut et le menu sera créé automatiquement.

> **Astuce** : Cette méthode est idéale pour découvrir la syntaxe des blocs complexes. Construisez visuellement, puis récupérez le code !

#### B.4.3 Créer le pied de page (footer)

➡️ Créez le fichier `parts/footer.html` :

```html
<!-- wp:group {"tagName":"footer","backgroundColor":"secondary","layout":{"type":"constrained"}} -->
<footer class="wp-block-group has-secondary-background-color has-background">
  <!-- wp:paragraph {"align":"center"} -->
  <p class="has-text-align-center">© 2026 Mon Theme. Tous droits réservés.</p>
  <!-- /wp:paragraph -->
</footer>
<!-- /wp:group -->
```

#### B.4.4 Déclarer les template parts dans theme.json

Pour que WordPress reconnaisse vos template parts, déclarez-les dans `theme.json` :

```json
{
  "$schema": "https://schemas.wp.org/wp/6.7/theme.json",
  "version": 3,
  "templateParts": [
    {
      "name": "header",
      "title": "En-tête",
      "area": "header"
    },
    {
      "name": "footer",
      "title": "Pied de page",
      "area": "footer"
    }
  ]
}
```

**Propriétés :**

- `name` : nom du fichier (sans extension)
- `title` : nom affiché dans l'éditeur
- `area` : zone du template (`header`, `footer`, ou `uncategorized`)

#### B.4.5 Utiliser les template parts dans un template

➡️ Modifiez votre fichier `templates/index.html` pour inclure les template parts :

```html
<!-- wp:template-part {"slug":"header","tagName":"header"} /-->

<!-- wp:group {"tagName":"main","layout":{"type":"constrained"}} -->
<main class="wp-block-group">
  <!-- wp:post-title /-->
  <!-- wp:post-content /-->
</main>
<!-- /wp:group -->

<!-- wp:template-part {"slug":"footer","tagName":"footer"} /-->
```

**Attributs du bloc `template-part` :**

- `slug` : nom du fichier template part (sans extension)
- `tagName` : balise HTML à utiliser (`header`, `footer`, `aside`, `div`...)

#### B.4.6 Exemple complet de structure

```bash
/mon-theme
    ├── style.css
    ├── theme.json
    ├── parts/
    │   ├── header.html
    │   ├── footer.html
    │   └── sidebar.html
    └── templates/
        ├── index.html
        ├── single.html
        ├── page.html
        └── archive.html
```

Tous vos templates peuvent maintenant réutiliser le même header et footer en les incluant avec `<!-- wp:template-part {"slug":"header"} /-->`.

---

### B.5 Étape 5 : Créer des compositions (patterns)

Les **patterns** (compositions) sont des assemblages de blocs prêts à l'emploi que l'utilisateur peut insérer facilement dans ses pages. Ils permettent de proposer des mises en page prédéfinies (hero, call-to-action, galerie, etc.).

ref : https://developer.wordpress.org/themes/features/block-patterns/

#### B.5.1 Structure du dossier patterns

➡️ Créez un dossier `patterns` à la racine de votre thème :

```bash
/mon-theme
    ├── style.css
    ├── theme.json
    ├── patterns/
    │   ├── hero.php
    │   └── call-to-action.php
    ├── parts/
    └── templates/
```

#### B.5.2 Méthode 1 : Créer un pattern via l'éditeur WordPress

Vous pouvez créer visuellement un pattern dans l'éditeur, puis récupérer le code pour l'intégrer à votre thème.

➡️ **Étapes :**

1. **Créer une nouvelle page ou article**
   - Allez dans `Pages > Ajouter` ou `Articles > Ajouter`

2. **Construire votre composition visuellement**
   - Exemple : créez une section "Hero" avec :
     - Un bloc **Couverture** (Cover) avec une image de fond
     - Un bloc **Titre** (Heading) centré
     - Un bloc **Paragraphe** pour le sous-titre
     - Un bloc **Boutons** avec un ou plusieurs boutons

3. **Sélectionner tous les blocs**
   - Cliquez sur le premier bloc
   - Maintenez `Shift` et cliquez sur le dernier bloc
   - Ou utilisez la vue **Liste des blocs** (icône 3 barres) pour sélectionner

4. **Copier les blocs**
   - Cliquez sur les **3 points** (⋮) de la barre d'outils
   - Sélectionnez **Copier les blocs**
   - Ou passez en **Éditeur de code** (`Ctrl+Shift+Alt+M`) et copiez tout le code

5. **Récupérer le code**
   - Collez dans un éditeur de texte pour voir le balisage des blocs

➡️ **Exemple de code obtenu pour un Hero :**

```html
<!-- wp:cover {"dimRatio":50,"minHeight":500,"align":"full"} -->
<div class="wp-block-cover alignfull" style="min-height:500px">
  <span
    aria-hidden="true"
    class="wp-block-cover__background has-background-dim"
  ></span>
  <div class="wp-block-cover__inner-container">
    <!-- wp:heading {"textAlign":"center","level":1} -->
    <h1 class="wp-block-heading has-text-align-center">
      Bienvenue sur notre site
    </h1>
    <!-- /wp:heading -->

    <!-- wp:paragraph {"align":"center"} -->
    <p class="has-text-align-center">
      Découvrez nos services et notre expertise.
    </p>
    <!-- /wp:paragraph -->

    <!-- wp:buttons {"layout":{"type":"flex","justifyContent":"center"}} -->
    <div class="wp-block-buttons">
      <!-- wp:button -->
      <div class="wp-block-button">
        <a class="wp-block-button__link wp-element-button">En savoir plus</a>
      </div>
      <!-- /wp:button -->
    </div>
    <!-- /wp:buttons -->
  </div>
</div>
<!-- /wp:cover -->
```

#### B.5.3 Méthode 2 : Créer un pattern en dur dans le thème

Pour intégrer le pattern à votre thème, créez un fichier PHP dans le dossier `patterns/`.

➡️ **Créez le fichier `patterns/hero.php` :**

```php
<?php
/**
 * Title: Hero Section
 * Slug: mon-theme/hero
 * Categories: featured
 * Keywords: hero, banner, accueil
 * Description: Une section hero avec titre, sous-titre et bouton d'action.
 */
?>
<!-- wp:cover {"dimRatio":50,"minHeight":500,"align":"full"} -->
<div class="wp-block-cover alignfull" style="min-height:500px"><span aria-hidden="true" class="wp-block-cover__background has-background-dim"></span><div class="wp-block-cover__inner-container"><!-- wp:heading {"textAlign":"center","level":1} -->
<h1 class="wp-block-heading has-text-align-center">Bienvenue sur notre site</h1>
<!-- /wp:heading -->

<!-- wp:paragraph {"align":"center"} -->
<p class="has-text-align-center">
      Découvrez nos services et notre expertise.
    </p>
<!-- /wp:paragraph -->

<!-- wp:buttons {"layout":{"type":"flex","justifyContent":"center"}} -->
<div class="wp-block-buttons"><!-- wp:button -->
<div class="wp-block-button"><a class="wp-block-button__link wp-element-button">En savoir plus</a></div>
<!-- /wp:button --></div>
<!-- /wp:buttons --></div></div>
<!-- /wp:cover -->
```

**En-tête PHP obligatoire :**

| Propriété     | Description                                  | Exemple                                         |
| ------------- | -------------------------------------------- | ----------------------------------------------- |
| `Title`       | Nom affiché dans l'éditeur                   | `Hero Section`                                  |
| `Slug`        | Identifiant unique (préfixé du nom du thème) | `mon-theme/hero`                                |
| `Categories`  | Catégorie(s) du pattern                      | `featured`, `text`, `gallery`, `call-to-action` |
| `Keywords`    | Mots-clés pour la recherche                  | `hero, banner, accueil`                         |
| `Description` | Description optionnelle                      | `Une section hero...`                           |
| `Block Types` | Blocs associés (optionnel)                   | `core/post-content`                             |

#### B.5.4 Exemple : Pattern Call-to-Action

➡️ **Créez le fichier `patterns/call-to-action.php` :**

```php
<?php
/**
 * Title: Call to Action
 * Slug: mon-theme/cta
 * Categories: call-to-action
 * Keywords: cta, action, contact
 */
?>
<!-- wp:group {"backgroundColor":"accent","layout":{"type":"constrained"}} -->
<div class="wp-block-group has-accent-background-color has-background">
    <!-- wp:heading {"textAlign":"center"} -->
    <h2 class="has-text-align-center">Prêt à commencer ?</h2>
    <!-- /wp:heading -->

    <!-- wp:paragraph {"align":"center"} -->
    <p class="has-text-align-center">Contactez-nous dès aujourd'hui pour démarrer votre projet.</p>
    <!-- /wp:paragraph -->

    <!-- wp:buttons {"layout":{"type":"flex","justifyContent":"center"}} -->
    <div class="wp-block-buttons">
        <!-- wp:button {"backgroundColor":"primary"} -->
        <div class="wp-block-button"><a class="wp-block-button__link has-primary-background-color has-background wp-element-button">Nous contacter</a></div>
        <!-- /wp:button -->
    </div>
    <!-- /wp:buttons -->
</div>
<!-- /wp:group -->
```

#### B.5.5 Utiliser les variables du thème dans les patterns

Vous pouvez utiliser les couleurs et presets définis dans `theme.json` :

```php
<?php
/**
 * Title: Section colorée
 * Slug: mon-theme/section-coloree
 * Categories: featured
 */
?>
<!-- wp:group {"backgroundColor":"primary","textColor":"white","layout":{"type":"constrained"}} -->
<div class="wp-block-group has-primary-background-color has-white-color has-text-color has-background">
    <!-- wp:paragraph -->
    <p>Ce texte utilise les couleurs du thème.</p>
    <!-- /wp:paragraph -->
</div>
<!-- /wp:group -->
```

#### B.5.6 Tester vos patterns

➡️ Pour voir vos patterns dans l'éditeur :

1. Allez dans une page ou un article
2. Cliquez sur le **+** pour ajouter un bloc
3. Cliquez sur l'onglet **Compositions** (ou Patterns)
4. Recherchez votre pattern par nom ou parcourez les catégories
5. Cliquez sur le pattern pour l'insérer

> **Astuce** : Vos patterns personnalisés apparaissent automatiquement dès qu'ils sont placés dans le dossier `patterns/` avec l'en-tête PHP correct. Aucune déclaration supplémentaire n'est nécessaire !

---

## B.6 Structure finale du thème

```bash
/mon-theme
    ├── style.css              # Métadonnées du thème
    ├── theme.json             # Configuration et styles globaux
    ├── functions.php          # Fonctionnalités PHP
    ├── screenshot.png         # Capture d'écran (1200x900px)
    ├── templates/             # Modèles de page
    │   ├── index.html
    │   ├── front-page.html
    │   ├── single.html
    │   ├── page.html
    │   ├── archive.html
    │   └── 404.html
    ├── parts/                 # Parties de modèles
    │   ├── header.html
    │   └── footer.html
    ├── patterns/              # Compositions
    │   ├── hero.php
    │   └── call-to-action.php
    └── styles/                # Variations de styles
        └── dark.json
```

---

### B.7 Étape 7 : Exporter le thème

Pour exporter votre thème avec les modifications faites dans l'éditeur :

- exporter en zip directement depuis l'éditeur de wordpress
- ou utilisez l'extension **Create Block Theme**.

#### B.7.1 Installation de Create Block Theme

➡️ Dans l'administration WordPress :

1. Allez dans `Extensions > Ajouter`
2. Recherchez "Create Block Theme"
3. Installez et activez l'extension

#### B.7.2 Exporter le thème

➡️ Allez dans `Apparence > Create Block Theme` et choisissez une option :

- **Export** : Télécharge un ZIP du thème actuel
- **Create Child Theme** : Crée un thème enfant
- **Clone Theme** : Crée une copie du thème
- **Overwrite Theme** : Sauvegarde les modifications dans les fichiers du thème

---
