Système de Recommandation d’Animés basé sur la Qualité

 - Contexte du projet

Dans un contexte de forte croissance des plateformes de streaming, la **recommandation de contenus de qualité** est un enjeu stratégique majeur.
Ce projet vise à fournir à une plateforme de streaming un **système de recommandation d’animés** orienté **qualité et accessibilité**, en particulier pour les **nouveaux utilisateurs**.

Contrairement aux systèmes classiques basés sur les genres ou la popularité, l’approche proposée repose sur un **Score Qualité** intégrant à la fois :

* la note globale de l’animé,
* la régularité de sa qualité au fil des épisodes,
* la durée de l’œuvre (nombre d’épisodes).


-  Objectifs

* Nettoyer et enrichir un jeu de données d’animés
* Construire un **indicateur de qualité robuste**
* Analyser les relations statistiques entre qualité, régularité et durée
* Mettre en place un **système de recommandation pondéré**
* Visualiser les résultats pour faciliter l’aide à la décision



- 1. Collecte des données

Le jeu de données initial 'animes.csv' contient notamment :

* Nom de l’animé
* Notes globale, meilleure et pire note par épisode
* Nombre d’épisodes
* Date de publication
* Studio de production
* Statut


* Mini audit des données

L'audit initial est réalisé afin de :

* Identifier les **valeurs manquantes**
* Détecter les **doublons**
* Vérifier les **types de colonnes**

Cette étape permet d’évaluer la qualité des données avant transformation.


- 2. Nettoyage des données

Pour procéder au nettoyage j'ai :

* Convertit des dates en format datetime
* Supprimé les lignes contenant des valeurs manquantes
* Supprimé les doublons
* Supprimé les colonnes non pertinentes ("Studio", "Status")
* Exporté le dataset nettoyé ("anime_nettoye.csv")


- 3. Enrichissement des données

J'ai créer de nouveau indicateurs :

* Régularité

C'est la différence entre la meilleur et la pire note d'un épisode de chaque animé
"Régularité = 10 − (Note meilleure épisode − Note pire épisode)"


* Score Qualité
Il représente la note globale de chaque animé ajusté grâce à la régularité
"Score Qualité = (Note Globale × 0.6) + (Régularité × 0.4)"

Ce score permet d’évaluer non seulement la qualité perçue, mais aussi la constance de l’animé dans le temps.



- 4. Analyse statistique

J'ai déterminé dans un premier temps :

* minimum
* maximum
* moyenne
* médiane

J'ai ensuite réalisé une "heatmap de corrélation" qui met en évidence les relations entre :

* Score Qualité
* Note globale
* Régularité
* Nombre d’épisodes

### Résultats :

* Corrélation positive forte entre **note globale**, **régularité** et **score qualité**
* Corrélation négative entre **nombre d’épisodes** et les autres indicateurs


- 5. Système de recommandation

### Principe

La recommandation repose principalement sur le **Score Qualité**, multiplié par un coefficient en fonction du nombre d'épisode

### Coefficients

| Nombre d’épisodes | Coefficient |
| ----------------- | ----------- |
| ≤ 150             | 1.00        |
| 150 – 300         | 0.85        |
| > 300             | 0.75        |

### Score final

Le score final devient le pourcentage de recommandation et est obtenue par la formule suivante :
Recommandation (%) = Score Qualité × Coefficient × 10



- 6. Visualisations

J'ai réalisé trois graphes à savoir :

* Score Qualité par animé (bar chart)
* Évolution de la qualité en fonction du nombre d’épisodes (échelle logarithmique)
* Top 10 des animés les plus recommandés (graphique interactif Plotly)

Ces ont démontrés d'une part que le score qualité se montre assez efficace dans le choix d'animé de haute qualite et d'autre part que le nombre d'épisode d'un animé influ grandement sur son pourcentage de recommandation car il existe des animés plus long que d'autre mais qui ont un meilleurs score qualité que beaucoup d'animé plus cours

- 7. Storytelling & interprétation

Le projet montre que :

* Un animé long n’est pas nécessairement mauvais
* Cependant, plus une œuvre est longue, plus le risque de baisse de qualité augmente
* Pour un nouveau fan d’animé, des œuvres plus courtes et régulières sont généralement plus adaptées

Le système proposé permet donc de guider intelligemment les utilisateurs, sans se limiter aux genres ou à la popularité brute.



Conclusion

Ce projet démontre qu’un système de recommandation simple, explicable et orienté qualité peut offrir une réelle valeur ajoutée à une plateforme de streaming, en améliorant l’expérience utilisateur et la découverte de contenus premium.


