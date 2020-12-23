# -The-Facial-recognition-and-Mask-Wearing-Alert-with-Opencv.-
Hello. This is The code for Facial Recognition wich alert when a person get off its mask !

Reconnaissance Faciale associée à une base de données :
En direct _ Vidéo Webcam.
* Recommandations d installation d'Opencv :
POUR INSTALLER OPENCV, il faut tenir compte de la version installée de Python.. Pour ma part, je suis Python 3.7.4 il faut donc que je récupère le fichier Opencv contrib correspondant : " opencv_python-4.1.2-cp37-cp37m-win_amd64.whl " .. en effet dans ce fichier on voit écrit cp37 qui correspond à ma version python .. le win pour windows et amd64 pour le 64bits ==> on trouve ces contrib au site suivant : " https://www.lfd.uci.edu/~gohlke/pythonlibs/#opencv " il faut placer ce fichier téléchargé là ou se trouve votre fichier python.exe, pour moi, cela se trouve ici : C:\ProgramData\Anaconda3 --> Puis, ouvrir cmd en tant qu'administrateur .. --> Placez-vous à l'endroit où vous avez copiez le ficher téléchargé précédemment avec la commande : cd C:\ProgramData\Anaconda3 Préparez le terrain pour Opencv en installant, (si ce n'est pas déjà fait !), numpy et matplotlib (pip install numpy, pip install matplotlib) Enfin : faire : pip3 install opencv_python-4.1.2-cp37-cp37m-win_amd64.whl ou : pip install opencv_python-4.1.2-cp37-cp37m-win_amd64.whl Et voilà ! Redémarrer Relancez un prompt, demandez python : >>>python et écrire la commande python : import cv2 Si tout se passe bien, il ne doit pas y avoir de message d'erreur !!

Puis, Il faut installer les fichiers haarcascades pour la reconnaissance par ordi : --> il se trouvent soit en allant dans le site officiel d'Opencv Release : https://opencv.org/releases/ .. puis chercher sa version d'opencv, moi c'est opencv 4.1.2 : et dans l'encadré opencv 4.1.2, cliquez sur source .. .. dès lors se télécharge le dossier zippé d'opencv, dézipez le dossier.. .. puis dedans : data\haarcascades : vous trouverez le dossier contenant toutes les haarcascades .. Vous devrez alors placer le fichier d'intérêt (ex : haarcascade_frontalface_alt.xml) là où se trouve l'algorithme qui l'utilise !

Solution : Après blocage de : " recognizer=cv2.createLBPHFaceRecognizer(); " --> le site suivant : " https://stackoverflow.com/questions/44633378/attributeerror-module-cv2-cv2-has-no-attribute-createlbphfacerecognizer " --> propose de remplacer cette ligne par : --> recognizer=cv2.face.LBPHFaceRecognizer_create(); --> Attention, si on est sur une version d'Opencv >4, il faut alors réinstaller opencv : --> le site propose..et ça marche !! : --> Dans le promt administrateur : faire : python , puis : python -m pip install --user opencv-contrib-python --> Ensuite, on redémarre l'ordi et la ligne recognizer=cv2.face.LBPHFaceRecognizer_create(); fonctionne !
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
--> Organisation des dossiers et des fichiers :
--> PLacez ce fichier Jupyter .ipynb dans un dossier ('X').
--> Dans ce même dossier, vous devez avoir le(s) fichier(s) 'haarcascade_frontalface_alt.xml'.
--> dans ce même dossier, vous devez avoir 2 autres dossiers : 'dataSet' et 'recognizer'.
==> Enfin, dans ce même dossier, vous devrez avoir le fichier de la base de données 'FaceBase.db' que nous allons créer dans la cellule qui suit.
1ère partie : Création de la base de données (BD) de reconnaissance faciale :
--> Téléchargez (si ce n'est pas déjà fait) SQLiteStudio : Dans Download, choisir la version correspondant à votre ordinateur.
--> Dézippez le dossier, puis repérez le fichier SQLiteStudio.exe et ouvrez le ;
--> Dans la barre de menu, Cliquez sur 'DataBase', et choisir 'Add a DataBase' : une fenêtre s'ouvre : Dans File, écrire le nom de la BD : 'FaceBase'.
--> Cliquez sur le '+' en vert (Create a new Datafile), et choisir l'emplacement de son enregistrement : Dans le dossier 'X' où se trouve le fichier Jupyter.
--> Faire 'Save', puis 'OK'
--> Dans la colonne de gauche, on observe le nom 'FaceBase' : double cliquez dessus, puis doucle cliquez sur 'table' juste en dessous : une table vide s'ouvre.
--> Dans la barre de menu, cliquez sur l'icône 'Create a new table', et renseignez alors, dessous dans l'encadré, le 'Table name' : écrire 'People', et validez ;
--> Cliquez alors sur l'icône 'Add column' : une fenêtre 'column' s'ouvre ;
--> Renseignez l'encadré 'Column name' par 'ID', l'encadré 'Data type' par 'INT', puis cochez 'Primary Key' car c'est l'ID qui servira de matricule aux infos d'une personne, cochez aussi 'Not Null', enfin faîtes 'OK' ;
--> Cliquez à nouveau sur l'icône 'Add column' : une fenêtre 'column' s'ouvre ;
--> Renseignez l'encadré 'Column name' par 'Name', l'encadré 'Data type' par 'STRING', cochez aussi 'Not Null', enfin faîtes 'OK' ;
--> Cliquez à nouveau sur l'icône 'Add column' : une fenêtre 'column' s'ouvre ;
--> Renseignez l'encadré 'Column name' par 'Age', l'encadré 'Data type' par 'INT', enfin faîtes 'OK' ;
--> Cliquez à nouveau sur l'icône 'Add column' : une fenêtre 'column' s'ouvre ;
--> Renseignez l'encadré 'Column name' par 'Genre', l'encadré 'Data type' par 'TEXT', enfin faîtes 'OK' ;
--> Cliquez à nouveau sur l'icône 'Add column' : une fenêtre 'column' s'ouvre ;
--> Renseignez l'encadré 'Column name' par 'Profession', l'encadré 'Data type' par 'TEXT', enfin faîtes 'OK' ;
==> Cochez alors sur la coche verte (commit structure changes) du sous-onglet 'structure', et faîtes 'ok'
==> C'est tout ! L'algorythme jupyter qui suit se chargera d'initier les personnes (id et name) dans la base de données.. Ce sera à vous, plus tard, de remplir les autres cases du tableau (en oubliant pas de cocher la coche verte au dessus du tableau pour valider les données).
2ème partie : Captures de photos d'identification d'un individu avec id défini
--> Lancez la cellule, --> donnez un N° d'Id à la personne filmée pendant 20 secondes, Attention : le Nom doit être mis entre Guillemets ! --> La capture vidéo s'arrête toute seule.
** Vérifiez dans votre dossier 'dataset' la qualité des captures de visages enregistrées (id correcte, un seul visage par id...) **
==> Relancez cette 1ère partie, autant de fois que de captures de visages souhaités, avec des id différents !

 3ème partie : Entrainement de l'algorithme pour la détection des visages photographiés présents dans le dossier 'dataset' :
--> Lancez cette cellule obligatoirement avant de lancer la 3ème partie, et renouvellez si un nouveau visage est inséré dans la base de données.
==> Vous devez normalement observer le défilement des photos capturées à votre écran ;
==> A la fin, vérifiez que le fichier 'trainningData.yml' a bien été créé dans votre dossier 'recognizer'.

 4ème partie : Lancement de la détection des visages en prise de vidéo directe :
--> Lancez la cellule suivante : FAIRE ' q ' POUR SORTIR DE LA VIDEO !

 5ème partie : Détection des visages non masqués :

* Il faut d'abord installer le module pour la Synthèse vocale : --> Prompt Anaconda : pip install pyttsx3

--> Lancez la cellule suivante : FAIRE ' q ' POUR SORTIR DE LA VIDEO !
à tester avec/puis sans Masque : Changer les messages d'avertissement pour remettre son masque.


