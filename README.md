# 42-Procedures

Set-up de votre environnement de travail pour vous préparer à 42

---

## Installations à faire

Ce fichier a été conçu pour un environnement Linux. Il se peut que certaines adaptations soient nécessaires pour l'appliquer aux environnements macOS et Windows.

### OhMyZsh

Le terminal sera votre outil principal pour naviguer, déplacer, récupérer et envoyer tous les exercices, mais aussi pour passer les examens.OhMyZsh est une surcouche de ZSH, lui-même une surcouche du Shell. Il facilitera votre vie sur le terminal, le rendra plus agréable à utiliser et vous permettra d’ajouter des raccourcis pratiques.

**⚠️** Vous n'aurez pas OhMyZsh en examen. Vous devrez donc maîtriser le terminal par défaut.

#### Installation de Curl

Outil en ligne de commande pour transférer des données depuis ou vers un serveur.

```bash
sudo apt install curl
```

#### Installation de ZSH

```bash
sudo apt install zsh
```

#### Installation de OhMyZsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Puis redémarrez votre ordinateur :

```bash
reboot
```

---

### Vim

Vim est un éditeur de text, c'est lui qui vous permettra d'éditer vos fichiers (notamment C). C'est avec Vim que vous rédigerez vos Days, mais aussi vos sujets d'examen. Il est indispensable de vous en servir dès votre préparation à la piscine pour bien intégrer ses subtilités. Arrivé à la piscine de faite pas l'erreur d'utiliser VSCode, car découvrir Vim lors de l'exam est la meilleur façon de vous assurer une perte de temps considérable pour le comprendre... voir un 0% !

```bash
sudo apt install vim
```

#### Configuration de Vim

Editez votre fichier .vimrc pour le configurer à votre guise.
```bash
vim ~/.vimrc
```

Exemple de configuration de base :

```vim
set tabstop=4            " Largeur d'une tabulation = 4 espaces (affichage)
set shiftwidth=4         " Indentation automatique = 4 espaces
set noexpandtab          " Utiliser de vraies tabulations (\t), pas des espaces
set autoindent           " Reprend l'indentation de la ligne précédente
set number               " Affiche les numéros de ligne
set cindent              " Active l'indentation de style C (structurée)
```

Configuration plus complète :

```vim
" INDENTATION
set tabstop=4              " Nombre d'espaces pour une tabulation (affichage)
set shiftwidth=4           " Nombre d'espaces pour une indentation automatique
set softtabstop=4          " Nombre d'espaces insérés/supprimés avec Tab/Backspace
set noexpandtab            " Utilise des tabulations réelles (caractère \t)
set autoindent             " Reprend l'indentation de la ligne précédente
set smartindent            " Indentation automatique intelligente
set cindent                " Indentation de style C (structurée, blocs, etc.)

" AFFICHAGE
set number                 " Affiche les numéros de ligne
set relativenumber         " Numérotation relative (utile pour les déplacements)
set cursorline             " Surligne la ligne courante
set showcmd                " Affiche les commandes tapées en bas
set showmode               " Affiche le mode actif (INSERT, VISUAL, etc.)
set ruler                  " Affiche la position du curseur (ligne/colonne)
syntax on                  " Active la coloration syntaxique
set background=dark        " Optimisé pour un thème sombre (ou 'light' si besoin)

" RECHERCHE
set ignorecase             " Ignore la casse dans les recherches
set smartcase              " Mais respecte la casse si vous utilisez une majuscule
set incsearch              " Recherche incrémentale (au fur et à mesure de la frappe)
set hlsearch               " Met en surbrillance tous les résultats

" FICHIERS ET SAUVEGARDE
set autoread               " Recharge le fichier s’il a été modifié ailleurs
set nobackup               " Ne crée pas de fichier de sauvegarde (.bak)
set nowritebackup          " Pas de fichier de sauvegarde temporaire lors de l’écriture
set noswapfile             " Ne crée pas de fichier d’échange (.swp)

" CLAVIER ET COMMANDES
set wildmenu               " Menu d’autocomplétion dans la ligne de commande
set clipboard=unnamedplus  " Partage le presse-papiers avec le système
set mouse=a                " Active la souris (clics, sélection, etc.)
set ttyfast                " Indique que le terminal est rapide (accélère le rendu)

```

---

### Norminette

La Norminette vous permet de vérifier si votre code en `.c` et `.h` est conforme à la norme 42. Elle signale les erreurs de style (problèmes d'indentation, d'espaces, de nombre de paramètres, de déclarations de variables, etc.). Elle vous indique également la ligne et la colonne où se situe l’erreur à corriger. Vous devez obtenir OK ! pour vous assurer que votre fichier est conforme.

Deux choses importantes à savoir sur la norme :

Lors de l’envoi des days (modules à rendre) pour correction, si votre exercice compile mais ne respecte pas la norme, il sera noté KO.

Lors des examens, aucune norme n’est exigée ! Il suffit que votre code fonctionne, même s’il ne suit pas les règles de la Norminette.

```bash
sudo apt install python3-setuptools
sudo apt install pipx
pipx install norminette
pipx ensurepath
```

#### Lancement manuel

```bash
watch -n 1 norminette -R CheckForbiddenSourceHeader
```

#### Intégration dans Vim (F2)

```bash
mkdir -p ~/.vim/after/plugin/
echo "noremap <F2> :update<CR>:execute 'silent !bash -c ''setsid x-terminal-emulator -e bash -c "watch -n 1 norminette -R CheckForbiddenSourceHeader ' . shellescape(expand('%')) . '" >/dev/null 2>&1 < /dev/null &'''<CR>:redraw!<CR>" > ~/.vim/after/plugin/norminette.vim
```

---

### Header 42

```bash
mkdir -p ~/.vim/plugin
cd $_
curl -O https://raw.githubusercontent.com/RicoWD/42-Procedures/main/stdheader.vim
```

Utilisation dans Vim : `F1` ou `:Stdheader`

---

### Batcat

```bash
sudo apt install bat -y
```

---

## Alias ZSH

```bash
vim ~/.zshrc
```

Ajoutez vos alias :

```bash
alias nom_alias="commande en bash"
```

Exemples :

```bash
alias ccc="cc -Wall -Wextra -Werror *.c"
alias gfr="git fetch && git rebase origin/main"
alias maj="sudo apt update && sudo apt upgrade -y"
alias bat="find . -type f | xargs batcat"
```

Rechargez votre config (afin d'appliquer les changements ordonnés) :

```bash
source ~/.zshrc
```

Ajout automatique :

```bash
echo 'alias ccc="cc -Wall -Wextra -Werror *.c"' >> ~/.zshrc && source ~/.zshrc
echo 'alias gfr="git fetch && git rebase origin/main"' >> ~/.zshrc && source ~/.zshrc
echo 'alias maj="sudo apt update && sudo apt upgrade -y"' >> ~/.zshrc && source ~/.zshrc
echo 'alias bat="find . -type f | xargs batcat"' >> ~/.zshrc && source ~/.zshrc
```

---

## Procédures Git

```bash
gcl   | git clone https://lien_du_repo nom_du_dossier               # Clone un dépôt distant dans un dossier local
gst   | git status                                                  # Affiche les fichiers modifiés / non suivis
ga .  | git add .                                                   # Ajoute tous les fichiers modifiés ou nouveaux à l'index (à utiliser avec prudence)
gc    | git commit -m "Message clair décrivant vos modifications"   # Crée un commit avec les fichiers indexés
gp    | git push                                                    # Envoie les commits sur la branche distante
```
