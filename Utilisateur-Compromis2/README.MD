

# Un Agent Compromis 2/3



- Category: `Forensic`
- Points: `1000` => `917`
- Difficulty: Easy
- Solves: `305`


**Description**

> Maintenant, nous avons besoin de savoir quels fichiers il a exfiltré.
>Format du flag : 404CTF{fichier1,fichier2,fichier3,...} Le nom des fichiers doit être mis par ordre alphabétique.
>
> Auteur : Typhlos#9037
>


**Attachments**

- `capture-reseau.pcapng`

### :book: Introduction
![script](https://user-images.githubusercontent.com/64932654/173409766-57acbf31-75b3-49d5-9672-8f55f164f252.PNG)


 
Nous partons donc avec notre script trouve dans Un Utilisateur Compromis 1/3. Le but etant de trouver quelles fichiers ont 
etes exfiltres ont va devoir mettre les mains dans le cambouis. Le script est assez simple, il liste d'abord les fichiers
dans le dossier ou se trouve le script et fait ensuite une resolution dns avec le nom du fichier qu'il export puis un text 
"BEGIN" (sous la forme de 626567696E ) pour signifier qu'il va enoncer le contenu du fichier et des char de fin "END " (sous la forme de 656E64 ) 
signifiant que le programme a fini d'enoncer le contenu du fichier.
Il nous suffit donc d'exporter toute les resolutions dns de la capture reseau avec tshark:
> tshark -r capture-reseau.pcapng -T fields -e ip.src -e dns.qry.name -Y "dns.flags.response eq 0 and dns.qry.name contains hallebarde"


on supprime toutes les occurences de 192.168.0.55 ainsi que celle de never-gonna-give-you-up et hallebarde.404ctf.fr 
dans visual studio code pour ne garder plus que les strings encoder en hex.
A partir de cette etape j'avoue ne pas m'etre trop casse la tete, j'ai simplement mis tout mes hex dans un fichier
texte et je les ai decoder avec la fonction unhexlify() de binascii. 

![decode](https://user-images.githubusercontent.com/64932654/173411894-18769b84-cd18-4752-8d7a-3832e8d24a01.PNG)

apres avoir laisse tourner le programme on se retrouve avec un fichier gros comme le bras (j'ai redirige l'output de mon script ) 
vers un fichier text :


![fin](https://user-images.githubusercontent.com/64932654/173412139-f14d9890-eae7-4ceb-a395-e68b183f3a20.PNG)

On voit deja certain fichier comme flag.txt mais ce serait trop long de chercher le reste a la main donc il suffit de 
trouver le debut des begin et de supprimer jusqu'au end et ainsi de suite. (J'avoue que je ne me suis pas foule mais bon)
On finit donc avec ce rendu: 


![presque](https://user-images.githubusercontent.com/64932654/173412917-59e584a1-7595-47aa-92f9-4c3bb7d257ad.PNG)

le format du flag est: 404CTF{fichier1,fichier2,fichier3,...} dans l'ordre alphabetique donc le flag est:

404CTF{exfiltration.py,flag.txt,hallebarde.png,super-secret.pdf}




