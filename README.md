# Cafe
Analyse de données à partir d'une extraction de Coffe-Review.com et de données de production FAO
Les amateurs de café à  la recherche de données sur leur breuvage préféré trouveront sur Kaggle différents jeux de données : Coffee_Data_CoffeeReview | Kaggle avec des données issues de dégustations de café , Coffee dataset | Kaggle qui concerne la production et la consommation de café dans le monde , entre autres.

Nous avons décidé de reprendre à la base avec 
une extraction d’ un jeu de données de dégustation/cotation de différents cafés , par  webscraping du site www.coffeereview.com 
un croisement  avec des  données de la FAO (Organisation des Nations Unies pour l'alimentation et l'agriculture )  pour la production de café vert  www.fao.org/faostat/fr/#data/QCL

Ce projet comporte 3 étapes :

-  webscraping et préparation des données [notebook cafe_1_webscrapping]
On obtient un jeu de données de 1700   cafés de cotation >= 94 sur 100 sélectionnés  sur une période de 21 ans  par le site “coffereview” .Il s’agit de leur liste des "highest-rated-coffees" (base “sélection_café”)

-  analyse de données  [notebook cafe_2_analyse]
Nous regardons la distribution des différentes  variables , particulièrement le pays d’origine du café , et les relations entre ces variables .
Puis nous mettons en relation cette base des cafés les plus côtés avec les données de production du café vert dans le monde

-  analyse de texte [notebook cafe_3_analyse-texte]
Il s’agit ici d’extraire la liste des qualificatifs utilisés dans la conclusion de chaque dégustation et de mettre en évidence les qualificatifs ou familles de qualificatifs les plus utilisés . Nous tentons ensuite d’établir une relation entre les qualificatifs les plus fréquents et la cotation des cafés ( ramenée à 2 classes >94 et =94)
      
Résultats de l'analyse de données de la base “sélection_café”
------------------------------------------------------------
1- Distribution des variables

a- variables quantitatives [café_2_graphe1]

Les principales variables sont la cotation (échelle de 0 à 100) , la note d’arôme , la note de saveur et la note de corps ( échelle de 0 à 10 pour les trois)  Les distributions de ces variables sont très resserrées du fait qu’il s’ agit d’une sélection des meilleurs cafés .

La distribution de la cotation , bien que tronquée à 94 par construction , est la plus étalée avec 934 cafés sur 1570 cafés pur origine à la valeur 94 , soit  59% .On pourra dans la suite s’intéresser à la portion de café de cotation > 94.
Les 3 autres variables ont pour mode la valeur 9 avec selon le cas de 83% à 91% de fréquence.Les valeurs minimales sont 7 ou 8 .Il n’y aura pas beaucoup d’informations à tirer de ces 3 variables.

b- variables catégorielles 

pays d’origine [café_2_graphe2] : 23  pays d’origine pour les 1570 cafés pur origine.
L’origine la plus représentée dans cette sélection des meilleurs cafés est l'Ethiopie avec 30% des cafés .

 pays de torréfaction [café _2_ graphe4] : 23% des cafés sont torréfiés à Taiwan et 18% en Californie . Au total 68% des cafés de la sélection sont torréfiés aux Etats-Unis , ce qui se comprend puisque les sélectionneurs sont américains .
Les cafés doivent , dans l’idéal, être consommés quelques semaines après la torréfaction et ce n’est possible que si lieu de torréfaction et lieu de consommation sont proches.
Il y a au total 56 pays de torréfaction ( en comptant individuellement les états américains) 

niveau de torréfaction [ café _2_ graphe3] : 64% des cafés ont suivi une torréfaction de type Medium-Light .
On note que le taux de torréfaction de niveau Médium-Light a tendance à augmenter au cours des années [café_2_graphe7]
Il y a 6 niveaux de torréfaction Very-Dark ,Dark, Medium-Dark ,Medium, Medium-Light, Light , mais avec seulement 4 cafés dans les deux premiers niveaux


2- Relations entre variables

a- entre  variables quantitatives:

Comme expliqué plus haut ,il n’ y a rien de particulier à dire.


b- entre variables catégorielles :

L’étude des contingences entre les variables catégorielles ,les trois variables du paragraphe précédent auxquelles a été  ajouté l’année de test , montre que toutes les variables sont liées [café_2_tabl1]

Par exemple [café_2_graphe5] : 355 café d’ origine Ethiopie dont 167 torréfiés à Taiwan et 59 en Californie ,191 cafés d’origine Kenya dont 74 torréfiés à Taiwan ,94 cafés d’ origine Hawaii dont 66 torréfiés à Hawaii.

Ou bien [café_2_graphe6]:sur 361 cafés torréfiés à Taiwan  216 sont de torréfaction Medium-Light , sur 248 cafés torréfiés en Californie 159 sont en Medium-Light .


c- entre variables quantitatives et catégorielles 

L’analyse porte , suite aux conclusions des statistiques descriptives sur les variables quantitatives , sur le lien entre la variable cotation > 94 et les variables catégorielles .Plus précisément on s’intéresse aux variations de la proportion de café de cotation >94 en fonction des modalités des variables catégorielles.
Les intervalles de confiance à 95% sur les proportions sont calculés selon une loi de distribution binomiale et les tests de comparaison entre proportions font intervenir une loi hypergéométrique (hypothèse H0 : les proportions sont égales)

en fonction des années [café_2_graphe9]:
  3 années ont une proportion nulle 
  3 années , 2009,2007 et 2017 présentent une proportion>94 significativement supérieure à la moyenne de 40.5% [café_2_tabl2]

en fonction des pays d’origine [café_2_graphe10] : 
  3 pays ont une proportion nulle 
  3 pays sont significativement  au-dessus  : Tanzanie,Panama , Kenya .[café_2_tabl3]

en fonction des pays de torréfaction [café_2_graphe11]: 
  16 pays ont une proportion nulle
  3 pays sont significativement  au-dessus de la moyenne : Kansas, Massachusetts, Hawaii [café_2_tabl4] 

en fonction des niveaux de torréfaction [café_2_graphe12] : 
  2 modalités Very Dark et Dark avec  proportion nulle
  1 modalité est  significativement  au-dessus de la moyenne : Medium [café_2_tabl5]


Croisement avec les données de productions 
------------------------------------------

1- description des  données de production

Quelques retraitements de la base de données de la FAO ont été faits:
-  cas de la Chine : de manière étonnante la base contient 3 lignes :"China" , "China,mainland" et "China, Taiwan Province of" , la ligne “China “ étant la somme des deux autres .On a supprimé la ligne “China” originale , changé "China,mainland" en “China” et rebaptisé la troisième ligne “Taiwan”

-  cas des Etats-Unis : Hawaii est le seul état des Etats-Unis producteur significatif de café et on a donc assimilé les Etats-Unis à Hawaii.


Le taux de croissance de la production mondiale de café vert est de 25% sur 20 ans , pour atteindre en 2021 environ 10 millions de tonnes., le nombre de pays producteurs variant de 83 à 80 sur la même période.[café_2_graphe13]

En 2021 les plus gros producteurs sont le Brésil avec 3 millions de tonnes et le Viet Nam avec 1.8 millions de tonnes [café_2_graphe14]

Les producteurs significatifs (> 50 milliers de tonnes en 2021 ) avec la plus forte croissance sur 20 ans sont : 
      Chine :+ 468%  ,106 milliers de tonnes en 2021
      Laos : + 403%  ,161 milliers de tonnes en 2021
      Ethiopie : + 185%  ,456 milliers de tonnes en 2021
      Nicaragua : + 180%  ,168 milliers de tonnes en 2021
      Viet Nam : + 164%  ,1845 milliers de tonnes en 2021

2-croisement avec la sélection de café

Un indicateur défini par 1000* nombre de cafés dans la sélection/production sur 20 ans est introduit à l’échelle de chaque pays d’origine [café2_graphe16][café2_graphe17]
La médiane de cet indicateur est 9 , la valeur du 1er quartile est 3 , la valeur du 3ème quartile est 46.

Principaux enseignements:
-  57 pays d’origine n’ont aucun café dans la sélection (Ouganda , Rwanda ,Venezuela,Côte d’ Ivoire ,Chine , Viet Nam)
-  Le  Vietnam est absent de la sélection alors qu’il s’agit du deuxième producteur mondial.
-  Le Brésil , premier producteur mondial , a un indicateur de 1 (7 cafés présents dans la sélection)
-  4 pays sont surreprésentés , c’est à dire avec une valeur d’ indicateur hors de la distribution dans une hypothèse normale : le Kenya avec 264 , Taiwan avec 775 , Panama avec 875 et Hawaii avec 1147

L’absence d’un pays d’origine de la sélection peut s’expliquer par une moindre qualité , au sens des critères de dégustation , des cafés issus de ce pays .Cependant on ne sait  pas combien de cafés ont été testés sur les 20 ans pour chaque origine.. 
Le cas de Hawaii interroge : sur 20 ans , 70 cafés intègrent la Top-review alors que la production cumulée n’est que de 61 milliers de tonnes (En comparaison l’Ethiopie a 378 cafés dans la sélection pour 6883 milliers de tonnes).Sachant que Hawaii est pratiquement le seul territoire des Etats Unis à même de produire du café et que la revue “coffeereview” est américaine , on peut sans doute parler d’ un biais domestique.

Analyse de texte
----------------

1- principe de l’analyse

Le texte analysé est le texte de la conclusion de chacune des dégustations.
Le processus est itératif avec un enrichissement des mots filtrés pour retirer  le plus possible de mots sans sens pour la qualification du café , par exemple des mots généraux comme “coffee” ,”cup”, “bean” ,”expresso” , certains adverbes comme “very” ,”almost” .., les mots en relation avec l’origine ou la torréfaction du café ( informations connues par ailleurs) , la ponctuation, les mots de liaison.

Après cette première opération, il reste au total 12500 mots répartis sur  1965 valeurs distinctes.

Le processus est à compléter , en effet certains des mots distincts de la liste finale recouvrent des sens très proches ou sont de même racine.Par exemple : floral , florals , flowers  ou fruit , fruit-toned  etc

On les regroupe pour obtenir une liste de qualificatifs , aux sens disjoints.A la fin il reste 1805 qualificatifs uniques pour un ensemble de 12493 valeurs (A noter : les techniques automatiques de racinisation ou lemnisation n'ont pas permis d'obtenir le résultat souhaité)


2-résultats de l’analyse

a-distribution des fréquences des qualificatifs 

Les 20 premiers qualificatifs ont une fréquence cumulée de 5175 [café_3_graphe1]
Les autres qualificatifs , au nombre de 1785 , ont une fréquence cumulée de 7318

Le qualificatif le plus fréquent est “fruity” dont la fréquence est 876 [café_3_graphe2]


b-lien entre les qualificatifs

Il y a bien des corrélations significatives (test de pearsonr ) entre certains qualificatifs mais les coefficients de corrélation ne dépassent pas 0.30 [café_3_tabl1]


3-liens avec la classe de cotation

On se propose de regarder si on peut faire une prédiction de la classe de cotation ( 1 = cotation >94 , 0 = cotation =94) à partir des 20 qualificatifs les plus fréquents .

Dans une phase intermédiaire ,il est procédé à une tentative de réduction de dimensions à partir d’une analyse ACP. Le résultat est plutôt décevant parce qu'il faut conserver 14 composantes pour cumuler 80% de variance expliquée [café_3_graphe4]

Néanmoins la modélisation par classification est faite à partir des 14 composantes principales conservées.

4 classifieurs sont testés : SVC , KNeighbors ,XGBClassifier ,RandomForestClkassifier avec dans chaque cas un processus de type GridSearchCV pour optimiser les hyperparamètres.
Les principales métriques d’évaluation des modèles sont regroupés en quatre graphiques [café_3_graphe6].
-Les 4 modèles ont des score test ( = accuracy ) similaires , SVC étant légèrement au dessus des autres
-Les 2 modèles XGBClassifier et RandomForestClassifier ( basés sur des arbres de décision) présentent un fort sur-appentissage

-Le paramètre précision prend la même valeur pour les 4 modèles sur chacune des 2 classes.Il est putôt mauvais pour la classe 1

-Le paramètre recall montre par contre une grosse disparité pour les 2 classes 
Le recall de la classe 1 reste très mauvais , il y a peu de vrais positifs et beaucoup de faux négatifs.XGB fait un peu mieux que les autres sur la classe 1 , mais inversement XGB est moins bon sur le recall de la classe 0.

En conclusion, les modèles de classifications testés ici ne sont pas très bons.

Nous proposons deux graphes d'illustration des matrices de confusion , modèles SVC et XGBClassifier. [café_3_graphe7][café_3_graphe8]


