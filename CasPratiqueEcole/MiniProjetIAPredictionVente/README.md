# Backlog complète du projet "Analyse et Prévision des Ventes"

---

## 1. Objectif général

Développer une application d’analyse des ventes pour une boutique en ligne permettant :

* Le chargement, nettoyage et analyse des données de ventes (CSV)
* Visualisation des indicateurs clés (CA mensuel, CA par produit)
* Analyse de tendance (croissance / décroissance)
* Prévision simple des ventes futures (sur 3 mois)
* Export de rapports (CSV + graphiques)
* Optionnel : interface web interactive avec Flask pour upload, analyse, prévisions et visualisation

---

## 2. User Stories (Backlog)

| ID  | En tant que... | Je veux...                                | Afin de...                           | Critères d’acceptation                                    | Priorité |
| --- | -------------- | ----------------------------------------- | ------------------------------------ | --------------------------------------------------------- | -------- |
| US1 | Analyste       | Charger un fichier CSV de ventes          | Analyser mes données facilement      | Script charge CSV, gère erreurs fichier                   | Haute    |
| US2 | Analyste       | Nettoyer les données                      | Supprimer lignes incomplètes         | Suppression NA sur colonnes clés                          | Haute    |
| US3 | Analyste       | Visualiser le chiffre d’affaires mensuel  | Comprendre l’évolution dans le temps | Graphique barre CA mensuel                                | Haute    |
| US4 | Analyste       | Visualiser le CA par produit              | Identifier produits les plus vendus  | Graphique barre CA produit                                | Haute    |
| US5 | Analyste       | Obtenir une tendance des ventes           | Savoir si le CA croît ou décroît     | Affichage message tendance croissance/décroissance/stable | Moyenne  |
| US6 | Analyste       | Exporter un rapport CA par produit        | Partager les résultats               | Fichier CSV exporté correctement                          | Moyenne  |
| US7 | Analyste       | Prévoir les ventes pour 3 mois à venir    | Planifier stock et marketing         | Graphique + données prévision 3 mois                      | Haute    |
| US8 | Utilisateur    | Accéder à l’analyse via une interface web | Simplifier l’usage et partager       | Page web upload + affichage graphiques                    | Basse    |
| US9 | Utilisateur    | Télécharger rapports et graphiques        | Garder traces                        | Boutons téléchargement fonctionnels                       | Basse    |

---

## 3. Jeux de données exemples

### `ventes.csv` (exemple simplifié)

```csv
commande_id,produit,prix_unitaire,quantite,date_commande
1,Stylo,1.20,10,2025-01-05
2,Cahier,2.50,5,2025-01-06
3,Stylo,1.20,3,2025-02-10
4,Crayon,0.80,15,2025-02-15
5,Cahier,2.50,7,2025-03-01
6,Stylo,1.20,20,2025-03-10
7,Agenda,5.00,2,2025-03-15
8,Stylo,1.20,8,2025-04-05
9,Cahier,2.50,10,2025-04-10
10,Crayon,0.80,10,2025-04-15
```

---

## 4. Sorties attendues

* Console/logs avec statistiques (total CA, nombre commandes, tendance)
* Graphiques sauvegardés (`.png`) :

  * CA mensuel
  * CA par produit
  * Prévision CA 3 mois (barres ou courbe)
* Fichier CSV rapport CA par produit (`rapport_ventes.csv`)
* (Pour Flask) interface web avec :

  * Upload fichier CSV
  * Affichage graphiques dynamiques
  * Boutons export rapport et graphiques

---

## 5. Script de prévision (extrait clé)

Exemple simple utilisant `statsmodels` pour une prévision ARIMA :

```python
from statsmodels.tsa.arima.model import ARIMA

def prevoir_ventes(ca_mensuel, mois_a_prevoir=3):
    # Convertir en série temporelle (index en datetime)
    ts = ca_mensuel.to_timestamp()
    model = ARIMA(ts, order=(1,1,1))
    model_fit = model.fit()
    forecast = model_fit.forecast(steps=mois_a_prevoir)
    return forecast
```

---

## 6. Proposition de structure Flask (optionnelle)

```
/app
  /static
    /css
    /js
  /templates
    index.html
    resultats.html
  app.py
requirements.txt
```

* `index.html` : formulaire upload CSV
* `app.py` : route pour upload, analyse, affichage
* `resultats.html` : affichage graphiques + liens téléchargement

---

## 7. Planning estimé (en jours)

| Tâche                        | Durée | Commentaire                    |
| ---------------------------- | ----- | ------------------------------ |
| Chargement et nettoyage CSV  | 1     | Gérer erreurs, formats date    |
| Analyse CA et visualisations | 1,5   | Graphiques matplotlib          |
| Analyse tendance             | 0,5   | Moyenne différences mensuelles |
| Prévision ARIMA              | 1,5   | Modèle, test, visualisation    |
| Export CSV rapport           | 0,5   |                                |
| Flask interface simple       | 2,5   | Upload + affichage résultats   |
| Tests & documentation        | 1     | README, commentaires           |

---

Veux-tu que je commence par te générer le **script Python complet** avec la partie prévision + jeu de données ?
Ou préfères-tu que je te fasse une **application Flask interactive** complète ?
Ou encore les deux, étape par étape ?
