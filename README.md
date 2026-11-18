# TP2_Retail_Intelligence_Platform_UC3_UC4_ELKOURA

## UC-04 — Gestion des erreurs et contrôle des doublons

### Objectif

Vérifier que le pipeline Apache NiFi détecte les fichiers déjà présents dans HDFS et empêche leur écrasement accidentel.

### Méthode

Le processeur `PutHDFS` a été configuré avec la stratégie `Conflict Resolution Strategy = fail`.

Un fichier nommé `store_sales_test_20.dat`, contenant 20 enregistrements de ventes, avait préalablement été ingéré dans le répertoire HDFS `/retail-lake/raw/nifi/`.

Une nouvelle ingestion du même fichier a ensuite été déclenchée.

### Résultat

Le processeur PutHDFS a détecté un fichier portant le même nom dans le répertoire de destination.

Le FlowFile a été redirigé vers la relation `failure`, où un élément était visible en attente (`Queued 1`).

Le journal NiFi a confirmé le motif du rejet :

`routing to failure because file with same name already exists`

La présence du fichier initial dans HDFS a également été vérifiée après le test.

### Conclusion

Ce test démontre le fonctionnement du mécanisme de détection des conflits de noms dans le pipeline d'ingestion. La stratégie `fail` permet d'éviter l'écrasement d'un fichier déjà présent et de conserver le FlowFile rejeté pour analyse.

### Export du pipeline

Le groupe de processus `UC04_Retail_Ingestion` a été exporté au format JSON sous le nom `UC04_Retail_Ingestion.json`.

La validité syntaxique du fichier a été vérifiée avec Python avant sa publication dans le dépôt GitHub du projet.
