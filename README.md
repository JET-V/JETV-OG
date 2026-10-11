# JetV Shop

Une boutique de jeu de rôle en PHP, faite en équipe de quatre au cégep (mars à mai 2025). On s'inscrit, on gagne des caps en répondant à des énigmes, on achète de l'équipement, on le range dans son sac et on l'utilise. Chaque objet a un poids : un sac trop lourd fait baisser la dextérité.

<!-- Captures d'écran : ajouter ici la boutique, la page d'un objet et une énigme (ex. docs/shop.png) -->

## Ce qu'on peut faire

- **Comptes** : inscription, connexion, modification du profil et de la photo de profil.
- **Boutique** : catalogue d'armes, d'armures, de médicaments, de nourriture et de munitions, avec recherche, filtres par type et par prix, et tri (prix, utilité, poids, quantité).
- **Panier et sac à dos** : ajout et retrait au panier, achat, revente et utilisation des objets (soins, nourriture).
- **Énigmes** : des questions à choix multiples par niveau de difficulté qui rapportent des caps.
- **Avis** : commentaires et évaluations sur cinq étoiles pour chaque objet.
- **Stats du joueur** : caps, points de vie, poids transporté et dextérité, affichés dans l'en-tête et mis à jour en direct.

## Technique

- **PHP 8**, architecture MVC faite à la main : un routeur (`src/configuration.php`), des contrôleurs, des modèles et des vues, sans framework.
- **MariaDB** : le schéma, les données de départ et la logique métier en **fonctions et procédures stockées** (`BD/dbMaria.sql`), appelées par **PDO** avec des requêtes préparées.
- **Sécurité** : mots de passe hachés avec `password_hash` / `password_verify`, sorties échappées contre le XSS, images de profil validées et renommées côté serveur.
- **Bootstrap 5** pour l'interface, et un petit module JS (`public/js/autoRefreshPanel.js`) qui rafraîchit les panneaux de la page sans la recharger.

```
controllers/   un contrôleur par page
models/        accès à la base (une classe par table ou concept)
views/         les pages et les partials (en-tête, pied de page)
src/           routeur, session, connexion PDO, classes (User, Item...)
public/        CSS, JS et images
BD/            le script SQL complet
```

## Lancer le projet

Il faut PHP 8 avec `pdo_mysql`, MariaDB et Apache avec `mod_rewrite` (le `.htaccess` envoie toutes les routes vers `index.php`).

1. Créer la base et l'importer :
   ```bash
   mysql -u root -e "CREATE DATABASE dbknapsak9"
   mysql -u root dbknapsak9 < BD/dbMaria.sql
   ```
2. Copier `configurations.ini.example` en `configurations.ini` et y mettre ses identifiants MariaDB.
3. Servir le dossier avec Apache, puis ouvrir le site.

Comptes de test : `joueur1` / `passjohn`, `joueur2` / `passjane`, `playerA` / `password`.

## L'équipe

Projet de [JET-V](https://github.com/JET-V), plus de 400 commits à quatre :

- **Jonathan** ([@Jonathan-333](https://github.com/Jonathan-333)) : l'en-tête et la navigation (stats du joueur, liens selon la connexion), la page de détails d'un objet (achat, revente, utilisation), le formulaire de profil avec l'envoi de la photo, l'affichage et le vidage du panier, la recherche dans la boutique, les formulaires d'inscription et de connexion, et les modèles `UserModel`, `ItemModel` et ceux des énigmes.
- **Emilien** ([@emil1326](https://github.com/emil1326))
- **Thomas** ([@ThomasAneakot](https://github.com/ThomasAneakot))
- **Victor** ([@OnlineAquaCow](https://github.com/OnlineAquaCow))
