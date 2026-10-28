# SportIA — prototype mobile

Prototype web responsive d'analyse sportive pour football et basketball.

## Fonctionnalités
- Interface sombre adaptée au téléphone.
- Deux sports avec matchs d'exemple clairement fictifs.
- Calcul pédagogique à partir de deux notes de forme saisies.
- Module basketball : moyennes illustratives des joueurs (points, rebonds, passes décisives, interceptions, contres) et fourchettes pédagogiques.
- Module football : comparaison descriptive des moyennes de corners, cartons jaunes et touches par équipe.
- Les statistiques affichées en mode démo sont fictives ; les touches peuvent être indisponibles selon le fournisseur.
- Chargement facultatif d'un endpoint API qui renvoie un tableau JSON.
- Manifest et service worker pour une installation web progressive lorsqu'il est hébergé en HTTPS.

## Limites
Ce prototype n'intègre pas de vraie IA entraînée ni de flux de données sportives par défaut. Les matchs affichés au démarrage sont fictifs. Le calcul de forme n'est pas un modèle prédictif validé. Ne l'utilisez pas comme garantie de résultat.

## Format attendu pour une API
L'URL configurée dans l'application doit être accessible en HTTPS et autoriser les requêtes du navigateur (CORS). Exemple de réponse :

```json
{
  "matches": [
    {
      "home": "Équipe A",
      "away": "Équipe B",
      "league": "Championnat",
      "date": "2026-10-28 18:00",
      "home_probability": 48,
      "draw_probability": 27,
      "away_probability": 25,
      "desc": "Données mises à jour à 10:00 UTC"
    }
  ]
}
```

Pour le basketball, fournir `home_probability` et `away_probability` dont la somme est 100, sans `draw_probability`.

Pour les statistiques avancées, les objets de match peuvent aussi contenir :
- `players`: tableau d'objets joueurs avec `name`, `team`, `points`, `rebounds`, `assists`, `steals`, `blocks`.
- `team_stats`: tableau d'objets équipes avec `name`, `corners`, `yellow` et `throwins` (moyennes historiques par match).

Les fourchettes de performance affichées dans ce prototype sont de simples marges illustratives, pas des prédictions validées. Utilisez des données réelles et documentées pour toute analyse sérieuse ; ne remplacez jamais une statistique manquante par une valeur inventée.

**Sécurité :** ne mettez jamais de clé API privée dans `index.html`. Utilisez un serveur intermédiaire (backend) pour protéger les clés.

## Lancer
- Local : ouvrez `index.html` dans un navigateur. Le chargement d'API peut être bloqué si l'API ou le navigateur interdit CORS.
- Hébergement : importez les fichiers dans un dépôt GitHub puis activez Settings → Pages → Deploy from a branch → `main` → `/ (root)`. L'adresse HTTPS sera affichée par GitHub Pages.
- Pour l'installation comme application web, ouvrez l'adresse HTTPS dans Chrome et utilisez le menu ⋮ → Ajouter à l'écran d'accueil, si proposé.

## Prochaines étapes
1. Choisir un fournisseur de données sportives pour les compétitions ciblées.
2. Créer un backend pour appeler l'API et cacher les clés.
3. Enregistrer les prédictions et résultats afin d'évaluer la calibration du modèle.
4. Remplacer le calcul pédagogique par un modèle évalué sur des données historiques.
