# oc-2021
OC informatique

## Le terminal
Le terminal permet d'ouvrir 

## Se déplacer dans l'arborescence

- pwd (print working directory)
- cd ()
- cd /
- cd ~
- cd ..

## Votre home directory

C'est votre dossier personnel local. Les fichiers résident en local sur cet ordinateur.

    $ cd
    $ pwd
    /Users/pp77xir

## Aller sur serveur

Utiliser la touche TAB (tabulateur) pour compléter un chemin

    cd /V (TAB)
    cd /Volumes
    cd /Volumes/p (TAB)
    cd /Voluves/pp77xir

## Dossier particuliers

    / (root)
    ~ (home directoery cmd+N)
    .. (parent directory)
    ../.. (grandparent)
    . (current directory)

# Créer des dossier

    mkdir oc
    mkdir oc/music
    
## Chemin relatif/absolue

    cd oc (relatif)
    cd /Volumes/pp77xir/oc/ (absolu)

    cd .. (relatif)
    cd /Volumes/pp77xir/ (absolu)

## Moving

La commande `mv` (move) permet de déplacer (ou renommer) un fichier.

    mv game game2
    mv game2 ..
    mv video demo

## Touch

La commande `touch` (toucher) permet de mettre à jour la date de modification.
Si le fichier n'existe pas, un fichier de taille 0 est créé.

    touch file_a
    touch dossier_a

## Jour et date

La commande `date` écrit la date et le temps actuel.

    $ date
    Mer 25 aoû 2021 14:09:10 CEST

La commande `cal` écrit un calendrier.

    $ cal
        Août 2021        
    Di Lu Ma Me Je Ve Sa  
    1  2  3  4  5  6  7  
    8  9 10 11 12 13 14  
    15 16 17 18 19 20 21  
    22 23 24 25 26 27 28  
    29 30 31                  

## L'éditeur nano

    nano

    # Titre
    Ceci est une ligne de text.

Etappes:
- ctr-X exit
- Y pour sauvegarder
- donner le nom demo.txt

Vérifier le fichier

    ls
    cat demo.txt

## Lancer python

