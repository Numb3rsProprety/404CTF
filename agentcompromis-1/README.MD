
# Un Agent Compromis 1/3



- Category: `Forensic`
- Points: `1000` => `864`
- Difficulty: Intro
- Solves: `390`


**Description**

> Nous avons surpris un de nos agents en train d'envoyer des fichiers confidentiels depuis son ordinateur dans nos locaux vers Hallebarde. Malheureusement, >il a eu le temps de finir l'exfiltration et de supprimer les fichiers en question avant que nous l'arrêtions.
>Heureusement, nous surveillons ce qu'il se passe sur notre réseau et nous avons donc une capture réseau de l'activité de son ordinateur. Retrouvez le >fichier qu'il a téléchargé pour exfiltrer nos fichiers confidentiels.
>
> Auteur : Typhlos#9037
>


**Attachments**

- `capture-reseau.pcapng`

### :book: Introduction
![http](https://user-images.githubusercontent.com/64932654/173407843-d85de860-a773-4d4e-ab8b-56836b0c2fa8.PNG)

 Chall super rapide a faire et super facile
En arrivant sur la capture reseau je commence tout de suite a regarder le trafic http


Apres avoir cherche pendant 10 secondes on tombe sur une requete ` http://hallebarde.404ctf.fr/exfiltration.py`



![exfil](https://user-images.githubusercontent.com/64932654/173408038-5709d261-ca8c-4baa-8dbd-505a9a291cb2.PNG)

en suivant la requete HTTP on obtient le code de exfiltration.py et en regardant tout en bas on obtient notre premier flag 







![flag](https://user-images.githubusercontent.com/64932654/173408365-9fb709d7-c7dc-440a-8d2a-32241d271e41.PNG)




```

Flag: `404CTF{t3l3ch4rg3m3n7_b1z4rr3}`


```

