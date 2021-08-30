# Notes de rédaction

## Créer un Jupyter Book
- installer jupyter-book

## Créer un fichier toc

    jb create --cookiecutter .
    
    
    % jb create --cookiecutter .
    You've downloaded /Users/raphael/.cookiecutters/cookiecutter-jupyter-book before. Is it okay to delete and re-download it? [yes]: yes
    
Entrer des informations à utiliser pour le Jupyter-book:

    author_name [Captain Jupyter]: Raphael Holzer
    github_username [raphaelholzer]: rasql
    

    book_name [My Book]:
    book_slug [my_book]: 
    book_short_description [This cookiecutter creates a simple boilerplate for a Jupyter Book.]: Ce site contient le matériel du cours OC info.
    version ['0.1.0']: 

Choisir une license:

    Select open_source_license:
    1 - MIT license
    2 - BSD license
    3 - ISC license
    4 - Apache Software License 2.0
    5 - GNU General Public License v3
    6 - None
    Choose from 1, 2, 3, 4, 5, 6 [1]: 1

    Select include_ci:
    1 - github
    2 - gitlab
    3 - no
    Choose from 1, 2, 3 [1]: 1

    ===
    Your book template can be found at
    /Users/raphael/GitHub/oc-2021/doc/my_book/
    ===
    
## Publier un site web

Voici la commande pour créer une site web statique.

    ghp-import -n -p -f _build/html
    Enumerating objects: 113, done.
    Counting objects: 100% (113/113), done.
    Delta compression using up to 4 threads
    Compressing objects: 100% (83/83), done.
    Writing objects: 100% (113/113), 1.79 MiB | 4.08 MiB/s, done.
    Total 113 (delta 17), reused 113 (delta 17)
    remote: Resolving deltas: 100% (17/17), done.
    remote: 
    remote: Create a pull request for 'gh-pages' on GitHub by visiting:
    remote:      https://github.com/Bugnon/oc-2021/pull/new/gh-pages
    remote: 
    To https://github.com/Bugnon/oc-2021.git
    * [new branch]      gh-pages -> gh-pages
