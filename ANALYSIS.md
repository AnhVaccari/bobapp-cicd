# Pipeline CI/CD - Analyse et Documentation

## 1. Documentation technique du workflow

### Vue d'ensemble

Le workflow CI/CD automatise l'intégration et le déploiement continue de BobApp. Chaque modification du code déclenche automatiquement une 
série de vérifications et de déploiements pour garantir la qualité et la fiabilité de l'application.

### Détail des étapes

#### 1. Tests Backend (Java/Spring Boot)
- **Objectif :** Vérifier que le code Java fonctionne
- **Actions :** Installation des dépendances Maven, exécution des tests, génération du rapport Jacoco

#### 2. Tests Frontend (Angular) 
- **Objectif :** Vérifier que le code Angular fonctionne
- **Actions :** Installation npm, tests avec coverage, build de production 

#### 3. Analyse Qualité (SonarCloud)
- **Objectif :** Analyser la qualité du code et détecter les problèmes
- **Actions :** Scan du code backend, détection des bugs, calcul des métriques

#### 4. Build Docker Backend
- **Objectif :** Créer l'image Docker du backend
- **Actions :** Construction de l'image, push vers Docker Hub

#### 5. Build Docker Frontend  
- **Objectif :** Créer l'image Docker du frontend
- **Actions :** Construction de l'image, push vers Docker Hub

#### 6. Déclenchement
- **Automatique :** Sur chaque push vers main
- **Validation :** Sur chaque Pull Request


### Fichiers de configuration

#### `.github/workflows/ci-build.yml`
- **Rôle :** Pipeline principale avec tests, builds et Docker
- **Jobs :** backend, frontend, docker-backend, docker-frontend

#### `.github/workflows/sonar.yml` 
- **Rôle :** Analyse qualité du code avec SonarCloud
- **Déclenchement :** En parallèle du workflow principal

#### `back/pom.xml`
- **Modification :** Ajout de l'organisation SonarCloud
- **Plugins :** Jacoco pour la couverture de code


## 2. KPI proposés

### 1. Code Coverage (Obligatoire)
- **Seuil minimum :** 60%
- **Actuel :** 38.8% 
- **Justification :** Garantir qu'au moins 60% du code est testé pour réduire les risques de bugs

### 2. Reliability (Fiabilité)  
- **Seuil minimum :** Note B ou supérieure
- **Actuel :** Note D (1 problème détecté)
- **Justification :** Éviter les bugs qui peuvent affecter le fonctionnement de l'application


## 3. Analyse des métriques actuelles

### Métriques techniques
- **Coverage :** 38.8% (insuffisant, objectif 60%)
- **Reliability :** Note D - 1 bug détecté à corriger
- **Maintainability :** Note A - 8 code smells mineurs
- **Security :** Note A - Niveau excellent maintenu
- **Duplications :** 0% - Aucun code dupliqué


### Retours utilisateurs
**Avis négatifs identifiés :**
- **1 ⭐ :** "Impossible de poster une suggestion de blague, le bouton tourne et fait planter mon navigateur !"
- **2 ⭐⭐ :** "Bug sur le post de vidéo remonté depuis deux semaines, toujours présent"
- **1 ⭐ :** "Plus de réception depuis une semaine, email sans réponse depuis 5 jours"
- **2 ⭐⭐ :** "J'ai supprimé ce site de mes favoris, vraiment dommage"

**Problèmes identifiés :**
- Bugs fonctionnels (boutons, vidéos)
- Manque de réactivité sur les corrections
- Support client défaillant
- Perte d'utilisateurs


### Priorités d'amélioration
1. **Corriger le bug de reliability** (Note D → B)
2. **Augmenter la couverture des tests** (38.8% → 60%)
3. **Résoudre les 8 code smells** pour maintenir la maintenabilité