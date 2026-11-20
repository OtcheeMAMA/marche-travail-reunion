## Données et périmètre

Source indiquée dans le dossier initial : Insee, *Flash Réunion* n° 308 (avril 2026), figure 2, enquêtes Emploi, taux de chômage BIT en moyennes annuelles 2014–2025. Le CSV contient 48 lignes : 12 années × 3 catégories de sexe à La Réunion et une série « Ensemble » pour l'Hexagone. Les valeurs sont reproduites telles qu'indiquées dans le dossier source ; elles ne doivent pas être extrapolées.

Limites : données annuelles arrondies, marge d'erreur signalée de ±2 points pour La Réunion, possible rupture de série en 2021 ; pas de ventilation par âge, diplôme ou commune ; pas de ventilation par sexe pour l'Hexagone.

## Construction dans Power BI Desktop

1. Décompresser ce dossier dans un emplacement simple, par exemple `C:\Portfolio\PROJET3_POWERBI_KIT_FINAL`.
2. Ouvrir Power BI Desktop. Choisir **Accueil → Obtenir des données → Texte/CSV**. Importer `data/chomage_reunion_insee_2014_2025.csv`.
3. Dans Power Query, vérifier les types : `Annee` entier, `Taux_chomage_pct` nombre décimal, les autres colonnes texte. Renommer la table `Chomage`. Si tu préfères le script M fourni, ouvrir l'Éditeur avancé et remplacer le chemin de fichier par le chemin réel sur ton ordinateur.
4. Dans **Modélisation → Nouvelle mesure**, copier les mesures de `powerbi/mesures_dax.dax` une par une. Formater les taux en pourcentage sans multiplier les valeurs par 100 : les données sont déjà exprimées en points de pourcentage (ex. 16 signifie 16 %). Formater les variations en points avec un format du type `+0;-0;0`.
5. Créer une page au format 16:9, fond clair. Titre : « Marché du travail à La Réunion – Taux de chômage BIT, 2014–2025 ». Ajouter deux segments : `Annee` et `Sexe` (sélection initiale « Ensemble »).
6. Ajouter les cartes : `Taux Réunion`, `Variation annuelle (pts)`, `Variation vs 2019 (pts)`, `Écart Réunion – Hexagone (pts)`, `Taux maximum sur la période`.
7. Ajouter les visuels : (a) courbes `Taux Réunion` et `Taux Hexagone` par année ; (b) courbes femmes/hommes avec `Taux Réunion`, légende `Sexe`, en excluant « Ensemble » ; (c) histogramme de `Variation annuelle (pts)` par année ; (d) tableau des années, taux Réunion, taux Hexagone, écart et variation annuelle.
8. Vérifier les interactions des segments et comparer les valeurs aux résultats ci-dessous.
9. Enregistrer sous `Dashboard_Chomage_Reunion.pbix`. Exporter éventuellement en PDF et prendre une capture d'écran du rapport réellement ouvert dans Power BI Desktop.

## Valeurs de contrôle attendues

- Réunion, Ensemble, 2025 : **16 %**
- Variation 2025 vs 2024 : **−1 point**
- Variation 2025 vs 2019 : **−5 points**
- Hexagone, Ensemble, 2025 : **7,5 %**
- Écart Réunion–Hexagone en 2025 : **+8,5 points**
- Maximum Réunion sur 2014–2025 : **26 % en 2014**

Lancer la vérification indépendante depuis ce dossier :

```bash
python powerbi/verification_indicateurs.py
```

## Organisation

- `data/` : données CSV
- `powerbi/` : requête M, mesures DAX et script de vérification
- `docs/` : rapport, fiche portfolio et maquette de référence

**Important :** ne présenter la maquette comme une capture Power BI réelle qu'après l'avoir remplacée par une capture issue de Power BI Desktop.
