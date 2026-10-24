# Le Triage — ICQ, cours 1

Jeu de tri de vocabulaire, à placer après l'exposé et le quiz, avant l'activité « Autopsie d'une défaillance ». Environ 10 à 15 minutes.

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `index.html` | Le jeu (mise en page et logique) |
| `contenu-source.json` | Les manches, les bacs, les tickets et leurs explications |
| `fond.jpg` | Image de fond |

## Mise en ligne sur GitHub Pages

1. Déposer les trois fichiers à la racine d'un dépôt (ou dans un dossier, par exemple `triage/`).
2. Dans le dépôt : Settings → Pages → choisir la branche, puis enregistrer.
3. Le jeu est accessible à l'adresse indiquée par GitHub Pages.

## Tester sur son poste

Le jeu charge `contenu-source.json` : un double-clic sur `index.html` ne fonctionne pas, le navigateur bloque la lecture du fichier. Lancer un petit serveur dans le dossier, par exemple :

```
python -m http.server 8000
```

puis ouvrir http://localhost:8000. L'extension Live Server de VS Code fonctionne aussi.

## Modifier le contenu

Tout se fait dans `contenu-source.json`, sans toucher au code :

- `attente` : durée en secondes avant qu'un ticket passe « en retard » (20 par défaut). Le bonus de rapidité s'applique pendant ce délai.
- Pour chaque manche :
  - `court` : nom affiché dans le parcours des manches ;
  - `titre` et `description` : écran de présentation de la manche ;
  - `cadence` : secondes entre l'arrivée de deux tickets (20 par défaut) ;
  - `bacs` : 2 à 4 bacs, chacun avec un `id`, un `nom` et une `aide` ;
  - `tickets` : chaque ticket a un `texte`, le `bac` attendu (son `id`) et une `explication`.

On peut ajouter ou retirer des tickets et des manches librement. Vérifier que chaque `bac` d'un ticket correspond bien à l'`id` d'un bac de sa manche.

## Règles du jeu

- Cliquer un bac, ou appuyer sur 1, 2, 3, 4 au clavier.
- Bonne réponse : 100 points, plus 20 par bonne réponse consécutive (jusqu'à +100), plus 50 si le ticket est trié avant de passer en retard.
- Mauvaise réponse : la série retombe à zéro, le bon bac est montré et le ticket y est déplacé, hachuré en rouge.
- Ticket en retard : il reste à trier, seul le bonus de rapidité est perdu.
- Option « Sans chrono » à l'accueil : un nouveau ticket arrive seulement quand le précédent est trié.
- Écran de fin : points, taux de réussite, meilleure série et liste des tickets à revoir en plénière.
