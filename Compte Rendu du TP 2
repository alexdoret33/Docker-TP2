Conteneurisation:

------------------------------------------------------------------------------------------------

Pour la désactivation de SELinux:

Édition du fichier "config" avec vi présent dans le répertoire: /etc/selinux/
Remplacer SELINUX=enforcing par SELINUX=disabled pour désactiver la politique de sécurité Linux.

------------------------------------------------------------------------------------------------

Le FireWall est activé et aucune configuration n'est nécessaire.

------------------------------------------------------------------------------------------------

Nous allons à présent installer puis configurer Docker.

L'installation se fait grâce à cette commande: sudo yum install docker 
À présent, Docker est installé. Il faut maintenant le lancer grâce à la commande de la doc:
sudo systemctl start docker 
Pour vérifier que cela marche:
sudo docker run hello-world 
Nous voyons ainsi le message suivant: "Hello from Docker".

De plus, il faut créer un groupe Docker dans le but de pouvoir l'utiliser sans être root. 
-groupadd docker est la commande pour créer le groupe Docker qu'on utilisera plus tard. 
-usermod -aG docker centos est la commande pour ajouter un utilisateur dans ce groupe. 
Ici, le nom de notre utilisateur sera centos. 
Nous n'avions pas crée d'utilisateur, donc pour en créer un nous avons utilisés les commandes suivantes: 
-useradd centos -passwd centos, pour l'ajout d'un mot de passe. 
Puis nous avons retapé la commande "usermod -aG docker centos" pour l'ajouter au groupe précédemment créé.

Maintenant, Docker est bien installé et correctement configuré.

------------------------------------------------------------------------------------------------

Ajout d'un disque de 30gb à la machine virtuelle CentOS: 

Sur VMWare, j'ai rajouté un disque de 15Go pour la partie DATA.
1. pvcreate /dev/sdb
2. vgcreate
3. lvcreate vgdata -L +15G --name lvl
4. mkfs.ext4 /dev/vgdata/lvl
5. mkdir /data
6. mount /dev/vgdata/lvl /toto

------------------------------------------------------------------------------------------------

Installer Docker et l'utiliser comme répertoire de données 

1. /data/docker
2. sudo vi /etc/docker/daemon.json
3. "data-root": "/data/docker/"
4. systemctl restart docker
5. ls /data/docker/

------------------------------------------------------------------------------------------------

Installer GitLab CE 

1. sudo yum install -y curl policycoreutils-python openssh-server openssh-clients
2. sudo systemctl enable sshd
3. sudo systemctl start sshd
4. sudo firewall-cmd --permanent --add-service=http
5. sudo systemctl reload firewalld
6. sudo yum install postfix
7. sudo systemctl enable postfix
8. sudo systemctl start postfix
9. curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash


Il faut modifier le fichier /etc/sysconfig/network-scripts/ifcfg-ens33 pour activer le DHCP pour que la VM ait une adresse ip, car le DHCP n'était pas activé de base
A la suite de ça, yum update et yum upgrade pour mettre à jour la VM

Ajout d'un disque
Sur VMWare, j'ai rajouté un disk de 15Go pour la partie DATA.

1. pvcreate /dev/sdb
2. vgcreate 
3. lvcreate vgdata -L +15G --name lvl
4. mkfs.ext4 /dev/vgdata/lvl
5. mkdir /data
6. mount /dev/vgdata/lvl /toto

Enregistrer un fichier en read-only que l'on a modifié: :w !sudo tee

Alors

déplacer le certificat: mv /root/server.crt /etc/gitlab/ssl/tp-gitlab.crt
déplacer la clef: mv /root/server.key /etc/gitlab/ssl/tp-gitlab.key

Il faut éditer le fichier gitlab.rb dans /etc/gitlab/gitlab.rb:
external_url='https://tp-gitlab'

Ne pas oublier d'éditer le fichier /etc/hosts:
192.168.11.177(pour ma part)    tp-gitlab

Et sur Windows, penser à éditer le fichier hosts:
192.168.11.177  tp-gitlab

Pour configurer le firewall, dans /etc/selinux/config:
SELINUX=disabled

Peu poussée, mais nous allons travailler dessus pour voir comment activer le port 443 pour le https

Pour redémarrer entièrement les services de gitlab: gitlab-ctl reconfigure

Puis on peut se rendre sur: https://tp-gitlab

