Prioritat i monitorització de processos
L’objectiu d’aquesta activitat és entendre el funcionament del sistema de prioritats a Linux i fer ús de les ordres associades a la seva gestió. També caldrà conèixer les eines de monitorització ps i top.

Per fer aquesta tasca es demanen les activitats següents:

Arrancar l’editor de text gedit en l’entorn gràfic.
Localitzar el PID del procés i visualitzar la seva prioritat general i la prioritat d’usuari nice.
Baixar al mínim la prioritat nice d’aquest procés. Comprovar el resultat i veure com es comporta la prioritat general.
Fer servir la utilitat top per assignar ara la màxima prioritat al procés. Convé que proveu com es poden ordenar els processos per diferents camps.


Una vegada engegada l’aplicació gedit obrim una consola de text per poder efectuar les diferents ordres administratives.

Si fem una ordre ps genèrica només veurem els processos de la nostra sessió. Si fem servir les opcions aux podrem veure gairebé tots els processos:


PS AUX, con este comando (estlinye    2905  0.0  0.0  29140 11984 ?        Ss   08:01   0:00 /lib/systemd/systemd --user)




