# TP FINAL HADOOP: Recommandation d'amis/de relations sur les réseaux sociaux
## Introduction

Dans ce TP, nous allons explorer et mettre en œuvre une fonctionnalité emblématique des réseaux sociaux modernes : le système de recommandation d'amis/de relations. Cette fonctionnalité, omniprésente sur des plateformes comme Facebook, LinkedIn ou Twitter, suggère aux utilisateurs des profils avec lesquels ils pourraient avoir des affinités ou des connexions potentielles. Notre objectif est de reproduire ce mécanisme sophistiqué en utilisant les principes du traitement de données massives et du filtrage collaboratif.

## Installation

1. Cloner le repos
2. Build l'image docker présente dans le fichier deploy : `docker build -t hadoop-tp3-img .`
3. Lancer le container docker : `docker compose up -d`

### Job 1

1. Se placer dans le dossier `colfil1`
2. `mvn clean install` vous permet de générer le jar correspondant
3. `hdfs dfs -mkdir -p user/hvanheerden` pour créer le dossier de travail
4. `hdfs dfs -mkdir -p user/hvanheerden/input` pour créer le dossier d'input
5. `hadoop jar /home/takima/Travail/hadoop-tp3/p-collaborative-filtering-job-1/target/original-hadoop-tp3-collaborativeFiltering-job1-1.0.jar org.epf.hadoop.colfil1.ColFilJob1 user/hvanheerden/input user/hvanheerden/output`
6. `hdfs dfs -cat user/hvanheerden/output/part-r-00001` pour afficher le résultat

Dans l'output, vous devriez voir les utilisateurs et leurs relations.

### Job 2

1.  Se placer dans le dossier `colfil2`
2. `mvn clean install` vous permet de générer le jar correspondant
3. `hadoop jar /home/takima/Travail/hadoop-tp3/p-collaborative-filtering-job-2/target/original-hadoop-tp3-collaborativeFiltering-job2-1.0.jar org.epf.hadoop.colfil2.ColFilJob2 user/hvanheerden/output/part-r-00001 user/hvanheerden/output2`
4. `hdfs dfs -cat user/hvanheerden/output2/part-r-00001` pour afficher le résultat

Dans l'output, vous devriez voir les pairs d'utilisateurs et le nombre de relations communes.

### Job 3

1. Se placer dans le dossier `colfil3`
2. `mvn clean install` vous permet de générer le jar correspondant
3. `hadoop jar /home/takima/Travail/hadoop-tp3/p-collaborative-filtering-job-3/target/original-hadoop-tp3-collaborativeFiltering-job3-1.0.jar org.epf.hadoop.colfil3.ColFilJob3 user/hvanheerden/output2/part-r-00001 user/hvanheerden/output3`
4. `hdfs dfs -cat user/hvanheerden/output3/part-r-00000` pour afficher le résultat

Dans l'output, vous devriez voir les recommendations pour chaque utilisateur (ici le nombre de recommendations n'est pas limité à 5).