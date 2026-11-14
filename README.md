Segmentation des clients d'un site e-commerce
Projet réalisé dans le cadre de la formation Data Scientist d'OpenClassrooms (titre RNCP niveau 7).
Contexte
Olist, place de marché en ligne brésilienne, souhaite une segmentation de ses clients utilisable par son équipe marketing pour ses campagnes de communication. Deux questions sont posées :
quels groupes de clients peut-on distinguer, et comment les décrire ?
à quelle fréquence faut-il mettre à jour la segmentation pour qu'elle reste pertinente ?
Données
Données publiques Brazilian E-Commerce Public Dataset by Olist :
environ 100 000 commandes passées entre septembre 2016 et octobre 2018 ;
plusieurs tables à relier : clients, commandes, paiements, avis, produits, vendeurs ;
95 379 clients uniques après nettoyage.
Démarche
Préparation : jointure des tables, nettoyage, puis calcul de quatre indicateurs par client, inspirés de la méthode RFM :
récence : nombre de jours depuis le dernier achat ;
fréquence : nombre de commandes ;
montant : total dépensé ;
satisfaction : note moyenne laissée dans les avis.
Clustering K-Means sur les données standardisées. Le nombre de groupes est choisi avec la méthode du coude et le score de Calinski-Harabasz, qui désignent tous deux 4 groupes.
Vérification : coefficient de silhouette, visualisation par ACP et t-SNE, distances entre groupes. DBSCAN et la classification hiérarchique ont aussi été testés.
Stabilité dans le temps : le modèle est réentraîné sur des données arrêtées 1 à 12 mois plus tôt, puis ses segments sont comparés à la segmentation actuelle avec l'indice de Rand ajusté (ARI).
Résultats
Quatre segments de clients :
Segment
Clients
Part
Note moyenne
Dépense moyenne
Commandes
Jours depuis le dernier achat
Satisfaits récents
42 926
45 %
4,7
153 R$
1,0
171
Satisfaits anciens
32 362
34 %
4,6
157 R$
1,0
442
Insatisfaits
17 126
18 %
1,6
187 R$
1,0
292
Fidèles à fort panier
2 965
3 %
4,1
361 R$
2,1
311
Ce que l'équipe marketing peut en tirer :
Satisfaits anciens : clients contents mais inactifs depuis plus d'un an, à relancer en priorité.
Insatisfaits : près d'un client sur cinq, avec un panier plutôt élevé ; à traiter par le service client avant toute relance commerciale.
Fidèles à fort panier : petit groupe, mais qui dépense plus du double des autres ; à fidéliser.
Stabilité : l'ARI reste compris entre 0,90 et 0,99 sur les douze mois testés. La segmentation est donc stable, et une mise à jour une à deux fois par an suffit.
Contenu du dépôt
Fichier
Rôle
1_notebook_exploration_062022.ipynb
Jointure des tables, nettoyage, calcul des indicateurs
2_notebook_essais_062022.ipynb
Essais de clustering et analyse des segments
3_notebook_simulation_062022.ipynb
Simulation de la stabilité dans le temps
Outils
Python, pandas, scikit-learn, Yellowbrick, Plotly, seaborn.
Limites
97 % des clients n'ont passé qu'une seule commande : la fréquence d'achat distingue donc peu les clients, sauf pour le segment des fidèles.
La segmentation repose sur quatre indicateurs ; la catégorie des produits achetés ou la localisation pourraient l'enrichir.
