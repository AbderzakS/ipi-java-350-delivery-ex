# ipi-java350-delivery-ex
TP pour le cours de livraison Web 350. L'objectif de ce TP est de livrer l'appli web statique du TP MDD050 sur AWS S3, et l'appli REST sur le service Beanstalk d'AWS (avec BDD MySQL via AWS RDS).

Il faut vous répartir en 4 groupes maximum pour effectuer ce TP, qui est à commencer en ELearning (allez le plus loin possible) et qui sera déroulé en un peu plus détaillé l'après-midi. **NE TOUCHEZ QU'AUX SERVICES QUI CONCERNENT VOTRE GROUPE**.

- Aller sur la console AWS via l'URL https://pjvilloud.signin.aws.amazon.com/console et se connecter avec les identifiants envoyés par mail.

## Application web statique 

- Sur la console AWS, chercher le service S3 parmi tous les services. 

- Regarder la vidéo de présentation de S3 : https://www.youtube.com/watch?v=_I14_sXHO8U

- Ouvrir le bucket *aws-website-mdd050-gX* correspondant au numéro de votre groupe et vous familiariser avec l'interface et les options (ne rien modifier pour l'instant). Ce bucket accueillera notre application web HTML/JS statique.

- Récupérer la dernière version de l'application web sur https://github.com/pjvilloud/ipi-mdd-050-web/releases

- Envoyer sur le bucket le contenu de l'archive 

- Paramétrer le bucket pour qu'il se transforme en hébergement statique de site web en le faisait pointer vers `index.html`

- Trouver l'URL et vérifier que le site web s'affiche correctement (nombre d'employés : 2500). Le site statique est pour l'instant connecté à une API qui existe déjà mais ce n'est pas la vôtre...

## API REST

- Sur la console AWS, chercher le service Elastic Beanstalk parmi tous les services.

- Regarder la vidéo de présentation de AWS Beanstalk : https://www.youtube.com/watch?v=SrwxAScdyT0

- Ouvrir l'application *Mdd050Api-X* correspondant à votre groupe et vous familiariser avec l'interface et les options.

- Sur la console AWS, chercher le service RDS parmi tous les services.

- Regarder la vidéo de présentation de AWS RDS : https://www.youtube.com/watch?v=yjH10T3Miag

- Cloner/Télécharger/Forker le repository https://github.com/pjvilloud/ipi-mdd-050-ex et basculer sur la branche deploy

- Se documenter sur le concept des profils Spring (https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-profiles.html) et isoler dans un profil `qlf` les propriétés qui devront être modifiées (valeurs pour l'instant inconnues) pour faire fonctionner l'application sur un autre environnement que l'environnement local. Ajouter la propriété `server.port=5000` ainsi que `spring.jpa.hibernate.ddl-auto=update` dans le profil `qlf`.

- Dans l'application Beanstalk, trouver les informations sur l'URL de l'appli web et sur la base de données à utiliser, sachant que le mot de passe est identique au nom d'utilisateur et mettre à jour le profil spring `qlf` avec les infos de la base de données (mot de passe identique au nom d'utilisateur).

- Ajouter une variable d'environnement (Configuration => Logiciels) dans l'application Beanstalk en spécifiant la clé `SPRING_PROFILES_ACTIVE` et la valeur `qlf` afin que l'API REST livrée sur Beanstalk utilise le profil `qlf` nouvellement créé.

- Exécuter un `mvn package` dans le répertoire du projet *ipi-mdd-050-ex* et vérifier qu'un jar a bien été créé dans le dossier `target`. Depuis le tableau de bord Beanstalk, charger ce jar dans l'application. Accéder à l'URL `.../employes/count` pour vérifier que cela renvoie bien un nombre correct.

## Communication entre l'appli web statique et l'appli REST.

- Modifier le fichier `index.html` de l'appli Web statique en remplaçant toutes les occurences de `mdd050api-qlf.eu-west-2.elasticbeanstalk.com` par l'URL de votre application.

- Ecraser le fichier `index.html` modifié sur S3.

- Vérifier que l'application web communique correctement avec l'API (2502 employés).

## Bonus (partie présentée l'après-midi si on a le temps)

- Intégrer la livraison dans votre processus de développement pour l'appli EmberJS et pour l'appli Java.

# BONUS : Essayer de livrer votre API REST sur votre VPS OVH en mettant en place un autre environnement
