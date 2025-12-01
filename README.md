TP Cloud 1 – OpenTofu & MinIO
README
1. Présentation

Dans ce TP, j’ai utilisé OpenTofu pour gérer une petite infrastructure IaC et MinIO comme serveur de stockage objet local. L’objectif était de créer un bucket, d’y déployer un site web statique et de valider le cycle complet (déploiement, suppression, reconstruction).

2. Mise en place de MinIO

J’ai installé MinIO, créé un dossier de stockage local puis lancé le serveur. Ensuite, j’ai accédé à la console via localhost:9001 avec les identifiants par défaut.

3. Infrastructure OpenTofu

J’ai créé un dossier de projet tp1-minio contenant les fichiers nécessaires (main.tf, variables.tf, outputs.tf).
Dans un premier temps, j’ai défini un provider MinIO avec les identifiants administrateur et j’ai créé un bucket privé pour valider le fonctionnement. Après un tofu init, tofu plan et tofu apply, j’ai pu vérifier que le bucket apparaissait bien dans la console MinIO.

La capture d’écran correspondante est incluse dans le dépôt.

4. Site web statique

J’ai ensuite fait évoluer la configuration pour héberger un petit site web statique.
J’ai créé deux fichiers (index.html et style.css) et j’ai modifié main.tf pour :

créer un bucket public,

uploader automatiquement les deux fichiers sous forme d’objets MinIO.

5. Variables et secrets

Pour éviter d’écrire les identifiants directement dans main.tf, j’ai ajouté un fichier variables.tf définissant :

l’utilisateur MinIO,

le mot de passe (déclaré en secret),

le nom du bucket.

J’ai ensuite créé un fichier terraform.tfvars (non inclus dans le dépôt) pour stocker les valeurs sensibles.

6. Validation

J’ai terminé en testant le cycle complet :

destruction de l’infrastructure avec tofu destroy,

nouvelle application avec tofu apply.

La reconstruction a fonctionné correctement, validant l’approche IaC.
