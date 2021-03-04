# EVALUATION Conception / SQL / PHP

Le but ici est de créer un blog en PHP.
On s'intéressera surtout aux données, aussi ne perdez pas de temps en mise en forme (vous pouvez utiliser Bootstrap si vous voulez).
Vous coderez en PHP pur, en utilisant de préférence la structure d'application fournie.

## Créer le modèle ( 2h )

Un blog comprend :
- des articles
- des commentaires sur les articles
- des catégories d'articles
- des utilisateurs enregistrés qui peuvent commenter les articles

### Créer le MCD

Une catégorie comportera :
- un nom

Un utilisateur comportera :
- un pseudo
- un email
- un mot de passe
- un rôle (qui sera égal à "user" ou "admin")

Un article comportera :
- un titre
- un contenu texte
- une image (le nom d'une image)
- une date de publication
- un statut (publié ou non)

Un commentaire comportera :
- un titre
- un contenu
- une date

Relations :
> - Un article appartient à une catégorie.
> 
> - Un commentaire concerne un article.
> 
> - Un commentaire est posté par un utilisateur.

Créez le MCD.
Générez la base de données (MySql).
Créez directement dans la base de données des catégories, des articles (reliés à une catégorie), des utilisateurs, des commentaires (reliés à un article et à un utilisateur).
Voir l'aide en bas de page pour l'encodage des mots de passe.
## Création de l'interface ( 2h )

La structure de l'application est fournie.

1 - Créez une page d'affichage des articles (accueil) avec :

- une bannière (dans un fichier header.php) avec :
    - le nom du site
    - un bouton de connexion (vous créerez le formulaire par la suite) si l'utilisateur n'est pas connecté
    - le nom de l'utilisateur s'il est connecté, avec un bouton de déconnexion
- tous les articles avec le titre, le date, le image, le contenu. Si possible par ordre anti-chronologique.

2 - Pour chaque article, créer un lien vers une page d'affichage de cet article.

3 - Créez la page d'affichage d'un article (avec les commentaires associés).

## Connexion ( 1h )

Créez une page avec un *formulaire de connexion* avec un champ *email* et un champ *mot de passe*.
Si les identifiants saisis ne sont pas corrects, on ré-affichera le formulaire avec un message d'erreur.
Si les identifiants sont corrects, on mettra l'utilisateur en session et on redirigera vers la page d'affichage des articles (accueil).
Dans la bannière, on affichera "Bonjour " suivi du pseudo de l'utilisateur.
On affichera un bouton de *déconnexion* à la place du bouton de *connexion*.

## Zone admin ( 2h )

### Authentification
Créez une page d'administration accessible via l'url /admin.

*Si vous ne savez pas faire cette partie (authentification), passez à la suivante.*

Protégez cette page (dans le controller) en testant si l'utilisateur est connecté et qu'il possède les bons droits (admin).

### Création de nouveaux articles
Dans la page que vous venez de créer, afficher un bouton (lien) pour ajouter un article et créez le formulaire associé. Attention, le champ image contient le chemin de l'image (sous forme de texte). Il n'y a pas d'upload à faire ici.
Afficher la liste des articles sous forme de table.

### BONUS :
Lorsqu'on clique sur une ligne, on souhaite afficher un formulaire pour éditer l'article selectionné.
On pourrait également avoir un lien de suppression pour chaque article.

---

AIDE :

La bonne pratique consiste à encrypter les mots de passe.

En Php, on dispose de 2 fonctions pour cela : *passwordHash* pour l'encodage et *passwordVerify* pour la vérification.

Vous pouvez utiliser *passwordVerify* lors de la soumission du formulaire de connexion.

Voici le mot de passe *toto* encodé : $2y$10$1QfBjKEqMVbTW0x/1SUzb.gUvU6uwkE2KI8VA.GQaT5UXTMQLw/jW

Vous pouvez l'utiliser comme mot de passe de vos utilisateurs.

Fonctionnement de *passwordHash* et *passwordVerify* :
```
<?php

$hash = password_hash("toto", PASSWORD_BCRYPT);

var_dump($hash);

var_dump(password_verify($hash, "toto"));

<?php

$hash = password_hash("toto", PASSWORD_BCRYPT);

var_dump($hash);

$passOk = password_verify("toto", $hash);

var_dump($passOk);
```
