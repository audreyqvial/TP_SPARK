# TP_SPARK
## Classification d'exoplanètes
OBJECTIF : Réaliser un classifieur d’exoplanètes labellisées “confirmée” ou “faux-positif”.  
Les données peuvent être récupérées sur ce site :http://exoplanetarchive.ipac.caltech.edu/index.html  
Pour ce faire, on utilise spark et scala.  
Dans un premier temps, on utilise un premier job qui permet de récupérer les data brutes et de les nettoyer (ajouter 0 lorsque les valeurs sont manquantes, enlever les colonnes inutiles, etc...). Les data sont enregistrées dans un fichier .csv ou .parquet  
Dans un deuxième temps, un autre job va appliquer un modèle de logistic regression selon différents paramètres et les données prédites sont enregistrées dans un fichier .csv  
La ligne de commande pour lancer le premier job est:

./spark-submit --conf spark.eventLog.enabled=true --conf spark.eventLog.dir="/tmp"  --driver-memory 3G --executor-memory 4G --class com.sparkProject.Job ~/Bureau/tp_spark/target/scala-2.11/tp_spark-assembly-1.0.jar  
  
La ligne de commande pour lancer le deuxième job est :  
./spark-submit --conf spark.eventLog.enabled=true --conf spark.eventLog.dir="/tmp"  --driver-memory 3G --executor-memory 4G --class com.sparkProject.JobML ~/Bureau/tp_spark/target/scala-2.11/tp_spark-assembly-1.0.jar
  
Pour exécuter le code, il faut changer le path d'enregistrement et de récupération des fichiers.  
  
La métrique du modèle de régression est donnée par le tableau suivant:  
      
|           paramgrid|             model|  
|--------------------|:------------------:|  
|              1.0E-6|0.9856638268288074|  
|3.162277660168379E-6| 0.988309235953996|  
|              1.0E-5|0.9902417397247346|  
|3.162277660168379...|0.9901872407616876|  
|              1.0E-4|0.9896820206447947|  
|3.162277660168379...|0.9891974217571619|  
|               0.001| 0.987970458616139|  
|0.003162277660168...|0.9848021540346792|  
|                0.01|0.9826693297511142|  
| 0.03162277660168379| 0.975644855297887|  
|                 0.1|0.9386547888386055|  
| 0.31622776601683794|               0.5|  
|                 1.0|               0.5|  
  
  
  Le meilleur paramètre pour la régression logistique est  1.0E-5.  
  
