# 42-Procedures
Set-up de votre environnement de travail pour vous préparer à 42
```
## Installations à faire
### OhMyZsh
### Vim
### Norminette
### Header 42

## Racourcis
### "F2" dans vim pour lancer la norminette
### Raccourcis ZSH

## Procédures GIT
### Initialisation d'un projet
### Maintenance et envoie
```

## Installations à faire

Ce fichier a été conçu pour un environnement Linux, il se peut que certaines adaptations soient nécéssaires pour les appliquer aux environnements MacOS et Windows.

### OhMyZSH

Le terminal sera votre outil à maitriser pour naviguer, déplacer, récupérer et envoyer tous les exercices, mais aussi lors des exams.
OhMyZsh est une surcouche de ZSH, elle même une surcouche de Shell qui vous facilitera la vie sur votre terminal, le rendra bien plus agréable et vous permettra de rajouter des raccourcis.

ATTENTION : Vous n'aurez pas OhMyZSH en examen. Vous devrez donc travailler sur le terminal par défault du terminal.

Voici les procédures pour l'installer : 

#### Curl

Curl est un outil en ligne de commande pour transférer des données depuis ou vers un serveur. Il nous servira donc à récupérer OhMyZSH.

```bash
sudo apt install curl
```

#### ZSH

Ouvrez votre terminal et coller la commande suivante pour installer `ZSH` : 

```bash
sudo apt install zsh
```

#### OhMyZSH
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Après avoir installer OhMyZSH vous devez redémarrer l'ordinateur. Vous pouvez le faire du terminal avec la commande suivante :
```bash
reboot
```

### Vim

Vim est un éditeur de text, c'est lui qui vous permettra d'éditer vos fichiers (notamment `C`).
C'est avec Vim que vous rédigerez vos Days, mais aussi vos sujets d'examen. 
Il est indispensable de vous en servir dès votre préparation à la piscine pour bien intégrer ses subtilités.
Arrivé à la piscine de faite pas l'erreur d'utiliser VSCode, car découvrir Vim lors de l'exam est la meilleur façon de vous assurer une perte de temps considérable pour le comprendre... voir un 0% !

```bash
sudo apt install vim
```

#### Configuration de Vim

Editez votre fichier .vimrc pour le configurer à votre guise.

```bash
vim ~/.vimrc
```

Ajoutez les commandes qui vous intéressent. Voici une configuration basique qui vous permet de faire quelques setup pour mieux s'adapter au C pour l'école 42 : 
```vim
set tabstop=4        " Largeur d'une tabulation = 4 espaces (affichage)
set shiftwidth=4     " Indentation automatique = 4 espaces
set noexpandtab      " Utiliser des vraies tabulations (\t), pas des espaces
set autoindent       " Reprend l'indentation de la ligne précédente
set number           " Affiche les numéros de ligne
set cindent          " Active l'indentation de style C (structurée)
```

Voici une liste des configurations bien bien plus complète, vous pouvez piochez ceux qui vous interesse et les ajouter à votre fichier `.vimrc` :
```vim
INDENTATION
set tabstop=4        " Nombre d'espaces pour un tab
set shiftwidth=4     " Nombre d'espaces pour le retrait automatique
set softtabstop=4    " Nombre d'espaces à insérer/supprimer quand tu appuies sur tab/backspace
set noexpandtab      " Utilise des tabulations réelles (pas des espaces)
set autoindent       " Copie l'indentation de la ligne précédente
set smartindent      " Indentation automatique intelligente
set cindent          " Indentation de style C

AFFICHAGE
set number           " Affiche les numéros de ligne
set relativenumber   " Affiche les numéros de ligne relatifs
set cursorline       " Surligne la ligne courante
set showcmd          " Affiche les commandes tapées en bas
set showmode         " Affiche le mode (INSERT, VISUAL, etc.)
set ruler            " Affiche la position du curseur (ligne/colonne)
syntax on            " Active la coloration syntaxique
set background=dark  " Optimisé pour un thème sombre (ou light)

RECHERCHE
set ignorecase       " Ignore la casse dans les recherches
set smartcase        " Mais si tu mets une majuscule, ça respecte la casse
set incsearch        " Recherche incrémentale (au fur et à mesure)
set hlsearch         " Met en surbrillance les résultats de recherche

FICHIERS ET SAUVEGARDE
set autoread         " Recharge le fichier s’il a été modifié à l’extérieur de Vim
set nobackup         " Ne crée pas de fichiers de sauvegarde
set nowritebackup    " Ne crée pas de fichiers de sauvegarde avant d’écrire
set noswapfile       " Ne crée pas de fichier d’échange (.swp)

CLAVIER ET COMMANDES
set wildmenu         " Autocomplétion visuelle dans la ligne de commande
set clipboard=unnamedplus " Partage le presse-papiers avec le système
set mouse=a          " Active la souris (clics, sélection, etc.)
set ttyfast          " Indique que ton terminal est rapide (accélère le rendu)

```

### Norminette

La Norminette vous permet de vérifier si votre code en `.c` et `.h` est à la norme 42.
Elle vous indique les erreurs de norme (problème d'indentation, d'espaces, de nombre de paramètres, du nombre de déclarations de variables...).
Elle vous indique la ligne et la colonne où se trouve l'erreur que vous devrez corriger.
Vous devez obtenir `OK !` pour vous assurer d'être à la norme.

Deux choses à savoir sur la norme : 
- Lors de l'envoie des 'days' (modules à rendre) pour correction, si votre exercice compile et est bon, il sera KO s'il ne respecte pas la norme !
- Lors des examen, aucune norme à respecté ! Il faut que votre code fonctionne, même s'il n'est pas à la norme.

Voici le procéssus d'installation de la Norminette : 
```bash
sudo apt install python3-setuptools
sudo apt install pipx
pipx install norminette
pipx ensurepath
```

#### Lancement de la Norminette : 

Vous pouvez lancer la Norminette sur le répertoire où se trouve votre fichier en y envoyant la commande suivante : 
Ceci fonctionne aussi si vous vous positionnez sur un répertoire contenant d'autres repertoire (exemple si vous voulez l'appliquer à tous les fichiers du c01 (ex01, ex02...)) :
```bash
watch -n 1 norminette -R CheckForbiddenSourceHeader
```
Le `watch` permet de relancer la Norminette à chaque fois que vous sauvegarder et ainsi de la mettre à jour avec les modifications apportées.

#### Intégration de la norminette sur Vim avec le raccourci F2

Afin de gagner beaucoup de temps, vous pouvez faire en sorte d'appuyer sur F2 lorsque vous êtes sur un fichier Vim afin de lancer la norminette sur un nouveau terminal.
Comme pour la commande précédente le `watch` permet de raffraichir la Norminette à chaque sauvegarde de votre fichier .`c`/`.h`.

```bash
mkdir -p ~/.vim/after/plugin/
cd $_
vim norminette.vim
```

Insérer le text suivant, puis sauvegardez et quitter : 
```vim
noremap <F2> :update<CR>:execute 'silent !bash -c ''setsid x-terminal-emulator -e bash -c "watch -n 1 norminette -R CheckForbiddenSourceHeader ' . shellescape(expand('%')) . '" >/dev/null 2>&1 < /dev/null &'''<CR>:redraw!<CR>
```

### Header 42

Afin que votre code soit aux normes, vous aurez besoin d'installer également l'en-tête de 42 qui vous permettra également de vérifier le nom de vos fichiers.
Ce header devra être ajouter dans tous vos fichiers `.c` et `.h`.

Pour installer le header 42 créer un nouveau fichier 

```bash
mkdir -p ~/.vim/plugin
cd $_
git clone  stdheader.vim 
```

Ouvrez un fichier avec vim et appuyer sur `F1` pour créer votre header automatique.
Vous pouvez également l'ajouter dans vim en sortant des différents modes (Insertion, Visual...) avec `ESC` et en écrivant `:Stdheader`.

### Batcat (lecteur de fichiers)

Afin de lire l'ensemble des fichiers d'un dossier et de ses sous-dossiers, vous pouvez utiliser une commande pour lancer `Batcat`.

Pour l'installer lancer la commande suivante : 
```bash
sudo apt install bat -y
```

### Alias ZSH

Avec ZSH vous pouvez créer des raccourcis (alias) qui vous permettront de gagner du temps avec de courtes lignes de commandes personnalisées.

```bash
vim ~/.zshrc
```

Une fois dans votre fichier `.zshrc` vous pouvez decendre tout en bas de votre fichier et écrire les prototypes qui peuvent vous intéresser de la façon suivante : 

```vim
alias nom_alias="commande en bash"
```

Voici une liste de quelques alias utile pour la piscine 42 :

```vim
alias ccc="cc -Wall -Wextra -Werror *.c"              " Compile avec les flags (qui considèrent les warnings comme des erreurs) tous les fichiers .c
alias gfr="git fetch && git rebase origin/main"       " Permet de récupérer tous les fichiers du repo distant de la branche origin/main
alias maj="sudo apt update && sudo apt upgrade -y"    " Mettre à jour votre ordinateur
alias bat="find . -type f | xargs batcat"             " Affiche l'ensemble des fichiers dans un répertoire et ses sous-repertoires
```

Après avoir modifier votre fichier `.zshrc` pensez à l'appliquer lançant la commande suivante sur votre terminal : 
```bash
source ~/zshrc
```

Une autre méthode existante pour modifier un fichier est d'utiliser `echo` directement du terminal. Si vous voulez ajouter l'ensemble, voici les commandes à entrer pour ajouter vos alias sur votre fichier `zshrc`. Ces lignes de commandes appliqueront aussi le `source ~/.zshrc`.
```bash
echo 'ccc="cc -Wall -Wextra -Werror *.c' >> ~/.zshrc && source ~/.zshrc
echo 'gfr="git fetch && git rebase origin/main"' >> ~/.zshrc && source ~/.zshrc
echo 'maj="sudo apt update && sudo apt upgrade -y"' >> ~/.zshrc && source ~/.zshrc
echo 'alias bat="find . -type f | xargs batcat"' >> ~/.zshrc && source ~/.zshrc
```

## Procédures GIT
### Initialisation d'un projet
### Maintenance et envoie
