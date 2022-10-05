# TP4 
Yasmin SAHLI 3ICS 

## Exercice 1 - Commandes de bases 

*1. Commencez par mettre à jour votre système avec les commandes vues dans le cours.*

```
sudo apt update 
sudo apt upgrade 
```
Avec ces deux commandes on redemmare des services. (tous les logiciels qui tournent en continue)

*2. Créez un alias “maj” de la ou des commande(s) de la question précédente. Où faut-il enregistrer cet
alias pour qu’il ne soit pas perdu au prochain redémarrage ?*

```
nano .bashrc
alias maj = 'sudo apt update ; sudo apt upgrade'
source ~/.bashrc (pour redémarrer bash de manière forcé)
maj 

```
Et en mettant l'alias dans bashrc cela permet de ne pas le perdre.

*3. Utilisez le fichier /var/log/dpkg.log pour obtenir les 5 derniers paquets installés sur votre machine.*
```
tail -5 /var/log/dpkg.log
```
*4. Listez les derniers paquets qui ont été installés explicitement avec la commande apt install*

Pour lister les derniers paquets installés on utilise la commande : 
```
apt list -i
```

*5. Utilisez les commandes dpkg et apt pour compter de deux manières différentes le nombre de total de
paquets installés sur la machine (ne pas hésiter à consulter le manuel !). Comment explique-t-on la
(petite) différence de comptage ? Pourquoi ne peut-on pas utiliser directement le fichier dpkg.log ?*

Pour afficher le nombre total de paquets installés sur la machine on fait : 
``` 
apt list -i | wc -l
dpkg -l | wc -l

```

On obtient pas les même nombre car avec dpkg on a des lignes d'erreurs et d'informations en plus

*6. Combien de paquets sont disponibles en téléchargement sur les dépôts Ubuntu ?*

Pour savoir combien de paquets sont disponibles en téléchargement sur les dépots Ubuntu on fait : 

```
apt list | wc -l
```

Il y en a 68744.

*7. A quoi servent les paquets glances, tldr et hollywood ? Installez-les et testez-les.*

Pour installer les paquets énoncés on fait : 

```
sudo apt install
```
GLANCES : un outil de surveillance multi-plateforme 
TLDR : une abréviation très souvent utilisée sur Internet de Too long; didn't read qui exprime un texte trop long et propose donc un résumé
HOLLYWOOD : un programme qui simule un genre de centre de contrôle affichant des logs qui défilent, des lignes de commandes et du binaire façon Matrix.

*8. Quels paquets proposent de jouer au sudoku ?*

Pour savoir quels paquets proposent de jouer au sudoku on fait : 

```
apt search sudoku 
```
La majorité des paquets permettent de jouer à sudoku.

## Exercice 2 

*A partir de quel paquet est installé la commande ls ? Comment obtenir cette information en une
seule commande, pour n’importe quel programme ? Utilisez la réponse à cette question pour écrire un
script appelé origine-commande (sans l’extension .sh) prenant en argument le nom d’une commande, et
indiquant quel paquet l’a installée.*

La commande pour savoir à partir de quel paquet est installé la commande ls est : 
```
dpkg -S /bin/ls 
```
Et c'est donc depuis le paquet *coreutils* que la commande ls est installée.

!!!!! LA COMMANDE WHICH !!!!! 

Cependant, si nous utilisons le -a (tous) option comme indiqué ci-dessous, which continue la recherche même s’il trouve une correspondance

## Exercice 3 

*Ecrire une commande qui affiche “INSTALLÉ” ou “NON INSTALLÉ” selon le nom et le statut du package
spécifié dans cette commande.*

## Exercice 4 

*Lister les programmes livrés avec coreutils. En particulier, on remarque que l’un deux se nomme [. De
quoi s’agit-il ?*

## Exercice 5 - aptitude 

## Exercice 6 - Installation d'un paquet par PPA 

*Certains logiciels ne figurent pas dans les dépôts officiels. C’est le cas par exemple de la version ”officielle”
de Java depuis qu’elle est développée par Oracle. Dans ces cas, on peut parfois se tourner vers un ”dépôt
personnel” ou PPA.*

*1. Installer la version Oracle de Java (avec l’ajout des PPA)*

sudo add-apt-repository ppa:linuxuprising/java

sudo apt update

sudo apt install oracle-java15-installer


*2. Vérifiez qu’un nouveau fichier a été créé dans /etc/apt/sources.list.d. Que contient-il ?*

## Exercice 7. Installation d’un logiciel à partir du code source

*Lorsqu’un logiciel n’est disponible ni dans les dépôts officiels, ni dans un PPA, ou encore parce qu’on
souhaite n’installer qu’une partie de ses fonctionnalités, on peut se tourner vers la compilation du code source.*

*1. Commencez par cloner le dépôt git suivant :
git clone https://gitlab.com/jallbrit/cbonsai
Ceci permet de récupérer en local le code source du logiciel cbonsai.*

*2. Rendez vous dans le dossier cbonsai. Un fichier README.md) est livré avec les sources, et vous explique
comment compiler le programme (vous pouvez installer un lecteur de Markdown pour Bash, comme
mdless pour vous faciliter la lecture de ce type de fichiers).*

*Un fichier Makefile est également présent. Un Makefile est un fichier utilisé par l’outil make, et
contient toutes les directives de compilation d’un logiciel. Un Makefile définit un certain nombre de
règles permettant de construire des cibles. Les cibles les plus communes étant install (pour la com-
pilation et l’installation du logiciel) et clean (pour sa suppression).*

*En suivant les consignes du fichier README.md, et en installant les éventuels paquets manquants, com-
pilez ce programme et installez le en local.*

*3. Malheureusement, cette installation “à la main” fait qu’on ne dispose pas des bénéfices de la gestion
de paquets apportés par dpkg ou apt. Heureusement, il est possible de transformer un logiciel installé
“à la main” en un paquet, et de le gérer ensuite avec apt ; c’est ce que permet par exemple l’outil
checkinstall.*

*4. Recommencez la compilation à l’aide de checkinstall :
sudo checkinstall
Un paquet a été créé (fichier xxx.deb), et le logiciel est à présent installé (tapez cbonsai depuis n’importe
quel dossier pour vous en assurer) ; on peut vérifier par exemple avec aptitude qu’il provient bien du paquet
qu’on a créé avec checkinstall.
Vous pouvez à présent profiter d’un instant de zenitude avant de passer au dernier exercice.*

## Exercice 8. Création de dépôt personnalisé


Création d’un paquet Debian avec dpkg-deb1. 

Dans le dossier scripts créé lors du TP 2, créez un sous-dossier origine-commande où vous créerez un
sous-dossier DEBIAN, ainsi que l’arborescence usr/local/bin où vous placerez le script écrit à l’exercice
2

2. Dans le dossier DEBIAN, créez un fichier control avec les champs suivants :
```
Package: origine-commande
#nom du paquet
Version: 0.1
#numéro de version
Maintainer: Foo Bar
#votre nom
Architecture: all
#les architectures cibles de notre paquet (i386, amd64...)
Description: Cherche l'origine d'une commande
Section: utils
#notre programme est un utilitaire
Priority: optional
```
#ce n'est pas un paquet indispendable

3. Revenez dans le dossier parent de origine-commande (normalement, c’est votre $HOME) et tapez la
commande suivante pour construire le paquet :
dpkg-deb --build origine-commande
Félicitations ! Vous avez créé votre propre paquet !

### Création du dépôt personnel avec reprepro

1. Dans votre dossier personnel, commencez par créer un dossier repo-cpe. Ce sera la racine de votre
dépôt

2. Ajoutez-y deux sous-dossiers : conf (qui contiendra la configuration du dépôt) et packages (qui contien-
dra nos paquets)

3. Dans conf, créez le fichier distributions suivant :
```
Origin: Un nom, une URL, ou tout texte expliquant la provenance du dépôt
Label: Nom du dépôt
// Suite: stable
Codename: focal
#!! A MODIFIER selon la distribution cible !!
Architectures: i386 amd64
#(architectures cibles)
Components: universe
#(correspond à notre cas)
Description: Une description du dépôt
```
4. Dans le dossier repo-cpe, générez l’arborescence du dépôt avec la commande
reprepro -b . export

5. Copiez le paquet origine-commande.deb créé précédemment dans le dossier packages du dépôt, puis,
à la racine du dépôt, exécutez la commande
reprepro -b . includedeb cosmic origine-commande.deb
afin que votre paquet soit inscrit dans le dépôt.

6. Il faut à présent indiquer à apt qu’il existe un nouveau dépôt dans lequel il peut trouver des logiciels.
Pour cela, créez (avec sudo) dans le dossier /etc/apt/sources.list.d le fichier repo-cpe.list
contenant :
```
deb file:/home/VOTRE_NOM/repo-cpe cosmic multiverse
```
(cette ligne reprend la configuration du dépôt, elle est à adapter au besoin)

7. Lancez la commande sudo apt update.
Féliciations ! Votre dépôt est désormais pris en compte ! ... Enfin, pas tout à fait... Si vous regardez
la sortie d’apt update, il est précidé que le dépôt ne peut être pris en compte car il n’est pas signé.
La signature permet de vérifier qu’un paquet provient bien du bon dépôt. On doit donc signer notre
dépôt.
### Signature du dépôt avec GPG

GPG est la version GNU du protocole PGP (Pretty Good Privacy), qui permet d’échanger des données de
manière sécurisée. Ce système repose sur la notion de clés de chiffrement asymétriques (une clé publique et
une clé privée)

1. Commencez par créer une nouvelle paire de clés avec la commande
```
gpg --gen-key
```

Attention ! N’oubliez pas votre passphrase !!!

2. Ajoutez à la configuration du dépôt (fichier distributions la ligne suivante :
```
SignWith: yes
```

3. Ajoutez la clé à votre dépôt :
```
reprepro --ask-passphrase -b . export
```

Attention ! Cette méthode n’est pas sécurisée et obsolète ; dans un contexte professionnel, on utiliserait
plutot un gpg-agent.

4. Ajoutez votre clé publique à votre dépôt avec la commande
```
gpg --export -a "auteur" > public.key
```

5. Enfin, ajoutez cette clé à la liste des clés fiables connues de apt :
```
sudo apt-key add public.key
```

Félicitations ! La configuration est (enfin) terminée ! Vérifiez que vous pouvez installer votre paquet comme
n’importe quel autre paquet.
