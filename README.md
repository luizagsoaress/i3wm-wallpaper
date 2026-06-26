# i3wm-wallpaper

## Sobre

Um pequeno script que altera o wallpaper a cada "shutdown" da máquina, no i3wm. Para cada wallpaper o tema é atualizado automaticamente para combinar com as cores gerais da imagem.

## Sumário

- [Configuração rápida](#configuração-rápida)
- [Passo a passo](#como-usar)

## Configuração rápida

Clone o repositório e execute o makefile:

```

git clone "https://github.com/luizagsoaress/i3wm-wallpaper.git"
cd i3wm-wallpaper

make install
make run

```

## Como usar?

Para executar a tarefa, vamos usar a ferramenta **wpgtk**, então, antes de tudo, siga os passos abaixo para baixá-la:

```

git clone https://github.com/deviantfero/wpgtk
cd wpgtk
sudo pip install .
cd wpgtk/misc
./wpg-install.sh

# Para garantir que a pasta de configuração do wpgtk foi criada execute:

mkdir -p ~/.config/wpg         
touch ~/.config/wpg/wpg.conf

```

Também precisamos do **feh** para exibir as imagens:

```

# pacman
sudo pacman -S feh

# AUR (yay)
yay -S feh

# debian/ubuntu
sudo apt install feh

```

Renomeie todos os seus wallpapers para um **valor x sequencial onde x > 0 e  x < que a quantidade de wallpapers**, por exemplo se você tiver 2 imagens:

> 1.jpg

> 2.jpg

Agora entre na pasta de configuração do i3:

```

cd ~/.config/i3

```

Crie o script responsável pela troca dos wallpapers:

```

touch wallpaper_script.sh
nano wallpaper_script.sh

### Cole o seguinte conteudo dentro do script (modifique as pastas/qtd de acordo com as necessidades):

#!/bin/bash

WALLPAPER_DIR="$HOME/Imagens/{(coloque aqui o caminho para a sua pasta com os wallpapers desejados)}"

MAX={(quantidade de wallpapers a serem utilizados)}

N=$(( (RANDOM % MAX) + 1 ))
feh --bg-scale "$WALLPAPER_DIR/$N.jpg"
wpg -a "$WALLPAPER_DIR/$N.jpg"
wpg -s "$N.jpg"

```

Depois, cole a seguinte linha dentro do **arquivo** config do i3:

```

nano config

### Cole isso aqui e salve as alterações:

exec_always --no-startup-id ~/.config/i3/wallpaper_script.sh

```

Pronto! Para adicionar mais imagens basta editar o **wallpaper_script.sh**



