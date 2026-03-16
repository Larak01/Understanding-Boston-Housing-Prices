# 🏠 Analyse des Déterminants du Prix du Logement à Boston

Ce projet explore les facteurs économiques, environnementaux et structurels qui influencent les prix de l'immobilier dans les quartiers de Boston. En s'appuyant sur le cadre théorique des **prix hédoniques**, nous comparons l'efficacité de l'économétrie classique face aux méthodes modernes de Machine Learning.

## 📌 Problématique
Identifier quels facteurs expliquent la variation des prix immobiliers et déterminer avec quelle précision ces prix peuvent être prédits en combinant modèles économétriques et apprentissage automatique.

## 📊 Données et Prétraitement
Le jeu de données contient 506 observations et 14 variables.
* **Audit initial** : Détection de 20 valeurs manquantes dans les variables clés (taux de criminalité, statut socio-économique, etc.).
* **Imputation robuste** : Utilisation de la **médiane** pour les variables continues afin d'éviter les biais liés aux quartiers atypiques, et du **mode** pour la variable binaire CHAS.
* **Analyse des valeurs aberrantes** : Identification de segments urbains spécifiques (zones industrielles ou enclaves d'élite) via la méthode de l'écart interquartile (IQR).
* **Pipeline** : Utilisation des `Pipelines` scikit-learn pour garantir la reproductibilité et éviter les fuites de données (*data leakage*).

## 🛠️ Stratégie de Modélisation
Nous avons confronté quatre approches pour naviguer entre interprétabilité et performance :
1. **OLS (MCO)** : Modèle de référence pour quantifier les associations linéaires.
2. **Elastic Net** : Régularisation (L1 + L2) pour stabiliser les estimations face à la forte **multicolinéarité** (ex: corrélation de 0,91 entre l'accessibilité RAD et la taxe TAX).
3. **Random Forest** : Méthode non-linéaire par agrégation (bagging) pour réduire la variance.
4. **XGBoost** : Algorithme de boosting séquentiel pour capturer les interactions complexes.

## 📈 Résultats de Performance
Les méthodes basées sur les arbres de décision surpassent largement les modèles linéaires, prouvant que le marché immobilier de Boston suit des logiques non-linéaires.

| Modèle | RMSE (Test) | R² (Test) |
| :--- | :---: | :---: |
| **XGBoost (Optimisé)** | **2.806** | **0.893** |
| Random Forest (Optimisé) | 3.252 | 0.856 |
| OLS (Baseline) | 5.000 | 0.659 |
| Elastic Net (Optimisé) | 5.005 | 0.658 |

*Note : XGBoost explique près de 89% de la variation des prix hors échantillon.*

## 💡 Enseignements Économiques
* **Piliers de la valeur** : Le nombre moyen de pièces (**RM**) et le statut socio-économique du quartier (**LSTAT**) sont les déterminants les plus critiques.
* **Externalités** : La qualité de l'air (NOX) et l'accessibilité (DIS) jouent un rôle significatif mais plus nuancé et souvent non-linéaire.
* **Censure des données** : Les modèles de Machine Learning gèrent mieux le phénomène de **top-coding** (prix plafonnés à 50 000 $) qui biaise les estimations OLS.

---
*Projet réalisé dans le cadre du module Machine Learning and Reduction Method (Année Académique 2025-2026).
