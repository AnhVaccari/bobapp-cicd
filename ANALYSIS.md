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
- **Actions :** Scan du code backend et frond end, détection des bugs, calcul des métriques

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

#### `.github/workflows/tests.yml` 
- **Rôle :** Exécution des tests backend et frontend
- **Jobs :** backend-tests, frontend-tests
- **Artéfacts :** Rapports de couverture de code

#### `.github/workflows/ci-build.yml`
- **Rôle :** Build et création des images Docker
- **Jobs :** backend, frontend, docker-backend, docker-frontend
- **Dépendances :** Déclenché après validation des tests

#### `.github/workflows/sonar.yml` 
- **Rôle :** Analyse qualité du code avec SonarCloud
- **Jobs :** backend, frontend
- **Déclenchement :** En parallèle des autres workflows

#### `back/pom.xml`
- **Modification :** Ajout de l'organisation SonarCloud
- **Plugins :** Jacoco pour la couverture de code
- 
#### `front/karma.conf.js`
- **Modification :** Ajout du reporter lcov dans coverageReporter
- **Objectif :** Génération automatique du fichier lcov.info pour SonarCloud


## 2. KPI proposés

### 1. Code Coverage (Obligatoire)
- **Seuil minimum :** 70%
- **Actuel Backend :** 38.8% 
- **Actuel Frontend :** 56.0% 
- **Justification :** Garantir qu'au moins 70% du code est testé pour réduire les risques de bugs

### 2. Reliability (Fiabilité)  
- **Seuil minimum :** Note B ou supérieure
- **Actuel Backend :** Note D (1 problème détecté)
- **Actuel Frontend :** Note A (exellent)
- **Justification :** Éviter les bugs qui peuvent affecter le fonctionnement de l'application


## 3. Analyse des métriques actuelles

### Métriques Backend (178 lignes)
- **Coverage :** 38.8% (insuffisant, objectif 70%)
- **Reliability :** Note D - 1 bug critique à corriger
- **Maintainability :** Note A - 8 code smells mineurs
- **Security :** Note A - Niveau excellent 
- **Duplications :** 0% - Aucun code dupliqué

### Métriques Frontend (161 lignes)
- **Coverage :** 56.0% (encore insuffisant, l'objectif 70%)
- **Reliability :** Note A - Aucun bug détecté
- **Maintainability :** Note A - 5 code smells mineurs
- **Security :** Note A - Niveau excellent 
- **Duplications :** 0% - Aucun code dupliqué


### Retours utilisateurs
**Avis négatifs identifiés :**
- **1 ⭐ :** "Impossible de poster une suggestion de blague, le bouton tourne et fait planter mon navigateur !"
- **2 ⭐⭐ :** "Bug sur le post de vidéo remonté depuis deux semaines, toujours présent"
- **1 ⭐ :** "Plus de réception depuis une semaine, email sans réponse depuis 5 jours"
- **2 ⭐⭐ :** "J'ai supprimé ce site de mes favoris, vraiment dommage"

**Problèmes identifiés :**
- Bugs fonctionnels (boutons, vidéos) - corélation avec le bug reliability backend
- Manque de réactivité sur les corrections
- Support client défaillant
- Perte d'utilisateurs


### Priorités d'amélioration
1. **URGENT - Corriger le bug de reliability bavkend** (Note D → B) - Impact direct sur l'expérience utilisateur
2. **Augmenter la couverture des tests backend** (38.8% → 70%)
3. **Légère amélioration frontend** (56.0% → 70%)
4. **Résoudre les code smells** (8 backend + 5 frontend) pour maintenir la maintenabilité