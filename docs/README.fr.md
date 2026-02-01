# Plugin de Style de Code Python

🌍 **Langue**: [English](../README.md) | [中文简体](README.zh-cn.md) | [繁體中文](README.zh-tw.md) | [Deutsch](README.de.md) | [Français](README.fr.md) | [Italiano](README.it.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Español](README.es.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code Plugin](https://img.shields.io/badge/Claude%20Code-Plugin-blue.svg)](https://code.claude.com/docs/en/plugins)

Un plugin Claude Code qui applique des directives de style Python professionnelles pour toute génération de code Python.

## Fonctionnalités

- **Activation Automatique** : Claude suit automatiquement les directives de style Python lors de la génération ou de la révision du code
- **Support de Revue de Code** : Révisez le code Python existant avec des retours détaillés et une notation
- **Couverture Complète** : Inclut les meilleures pratiques de l'industrie
  - Conventions de nommage (modules, classes, fonctions, variables, constantes)
  - Format de docstring avec les sections Args, Returns, Raises, Yields
  - Règles d'importation et ordre
  - Standards de formatage (indentation, longueur de ligne, espaces)
  - Règles de langage (exceptions, annotations de type, compréhensions)
- **Références Détaillées** : Documentation de support pour les cas particuliers

## Installation

### Méthode 1 : Via Marketplace (Recommandé)

Dans Claude Code, exécutez :

```bash
# Étape 1 : Ajouter le marketplace
/plugin marketplace add pillarliang/python-code-style

# Étape 2 : Installer le plugin
/plugin install python-code-style
```

### Méthode 2 : Via settings.json

Ajoutez à votre `~/.claude/settings.json` :

```json
{
  "extraKnownMarketplaces": {
    "python-code-style": {
      "source": {
        "source": "github",
        "repo": "pillarliang/python-code-style"
      }
    }
  },
  "enabledPlugins": {
    "python-code-style@python-code-style": true
  }
}
```

### Méthode 3 : Installation Manuelle

```bash
# Cloner le dépôt
git clone https://github.com/pillarliang/python-code-style.git

# Copier dans le répertoire des plugins Claude
cp -r python-code-style ~/.claude/plugins/python-code-style
```

### Vérifier l'Installation

Exécutez `/plugin` ou `/plugin list` dans Claude Code pour confirmer l'installation.

### Mettre à jour le Plugin

**Mise à jour manuelle :**

1. Mettez à jour la liste des plugins du marketplace, puis réinstallez :
   ```bash
   /plugin marketplace update pillarliang/python-code-style
   ```

2. Ou via l'interface interactive : Exécutez `/plugin`, passez à l'onglet **Marketplaces**, sélectionnez le marketplace, puis choisissez **Update**.

**Mise à jour automatique :**

Claude Code prend en charge les mises à jour automatiques des marketplaces et des plugins installés au démarrage :

1. Exécutez `/plugin` pour ouvrir le gestionnaire de plugins
2. Sélectionnez l'onglet **Marketplaces**
3. Sélectionnez le marketplace cible
4. Choisissez **Enable auto-update**

> **Note :** Le marketplace officiel Anthropic a les mises à jour automatiques activées par défaut. Les marketplaces tiers et développés localement les ont désactivées par défaut.

## Utilisation

Une fois installé, le plugin s'active automatiquement lorsque vous demandez à Claude de :

- Écrire du code Python
- Créer des scripts ou modules Python
- Refactoriser du code Python
- Générer des fonctions ou classes Python
- **Réviser du code Python existant**

### Exemples de Prompts

**Génération de Code :**
```
"Écris une fonction Python pour analyser des fichiers JSON"

"Crée une classe Python pour les connexions à la base de données"

"Refactorise ce code Python pour le rendre plus propre"
```

**Revue de Code :**
```
"Révise ce fichier Python : /path/to/file.py"

"Vérifie ce code Python pour les problèmes de style"
```

Claude appliquera automatiquement les règles de style Python, incluant :

- Conventions de nommage appropriées (`snake_case` pour les fonctions, `CapWords` pour les classes)
- Docstrings avec les sections Args, Returns, Raises
- Ordre d'importation correct (stdlib → tiers → local)
- Indentation de 4 espaces et limite de 80 caractères par ligne
- Annotations de type pour les signatures de fonctions

### Exemple de Sortie de Revue de Code

Lors de la révision du code, Claude fournit un retour structuré :

```markdown
## Résumé de la Revue de Code

### ✅ Points Positifs
- Nommage de fonction clair utilisant snake_case
- Bonne utilisation des annotations de type

### ⚠️ Problèmes Trouvés

#### Problème 1 : Documentation - Docstring manquant
- **Emplacement** : Ligne 5
- **Problème** : La fonction `process_data` n'a pas de docstring
- **Suggestion** : Ajouter un docstring avec les sections Args/Returns/Raises

#### Problème 2 : Style - Argument par défaut mutable
- **Emplacement** : Ligne 10
- **Problème** : `def func(items=[])` utilise une valeur par défaut mutable
- **Suggestion** : Utiliser `items=None` et initialiser à l'intérieur de la fonction

### 📊 Évaluation Globale
- Conformité au Style : 7/10
- Documentation : 5/10
- Qualité du Code : 8/10
```

## Compatibilité

- **Claude Code** : v1.0.0+
- **Mode Cowork** : Entièrement supporté
- **Versions Python** : Les règles s'appliquent à Python 3.8+

## Sources des Directives de Style

Ce plugin est basé sur des conventions de style Python largement adoptées, incluant :

- [PEP 8 – Guide de Style pour le Code Python](https://peps.python.org/pep-0008/)
- [PEP 257 – Conventions de Docstring](https://peps.python.org/pep-0257/)
- [PEP 484 – Annotations de Type](https://peps.python.org/pep-0484/)
- [Guide de Style Python de Google](https://google.github.io/styleguide/pyguide.html)

## Licence

Ce plugin est sous licence [MIT](https://opensource.org/licenses/MIT).
