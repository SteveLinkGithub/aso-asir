# Prioritat i monitorització de processos
L’objectiu d’aquesta activitat és entendre el funcionament del sistema de prioritats a Linux i fer ús de les ordres associades a la seva gestió. També caldrà conèixer les eines de monitorització ps i top.

Per fer aquesta tasca es demanen les activitats següents:

Arrancar l’editor de text gedit en l’entorn gràfic.
Localitzar el PID del procés i visualitzar la seva prioritat general i la prioritat d’usuari nice.
Baixar al mínim la prioritat nice d’aquest procés. Comprovar el resultat i veure com es comporta la prioritat general.
Fer servir la utilitat top per assignar ara la màxima prioritat al procés. Convé que proveu com es poden ordenar els processos per diferents camps.


Una vegada engegada l’aplicació gedit obrim una consola de text per poder efectuar les diferents ordres administratives.

Si fem una ordre ps genèrica només veurem els processos de la nostra sessió. Si fem servir les opcions aux podrem veure gairebé tots els processos:

PS AUX, con este comando (**estlinye    2905  0.0  0.0  29140 11984 ?        Ss   08:01   0:00 /lib/systemd/systemd --user**

Este ha sido el resultado del comando **ps aux**

<img width="869" height="60" alt="image" src="https://github.com/user-attachments/assets/1b6d99cf-4fe8-41e9-b746-2a17f7bb0738" />


Aquestes opcions ens donen un llarg llistat poc pràctic, però ens ajuden a localitzar el procés en qüestió que té un PID=2213 en aquest cas. Ara podem aplicar el paràmetre estil BSD (l)ong, que ens permet presentar informació ampliada, i el paràmetre estil Unix -p, que permet limitar la informació a un procés concret.


F   UID     PID    PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND

(**0 1219642705 132566 132535 20 0  22376  5832 do_wai Ss   pts/1      0:00 /bin/bash**)
(**4 1219642705 221006 132566 20 0  14136  3340 -      R+   pts/1      0:00 ps l**)

Este ha sido el reusltado de la salida del comando **ps l**

<img width="807" height="83" alt="image" src="https://github.com/user-attachments/assets/afafba22-cac1-4595-afd0-fb32349e33a9" />


Veiem que la prioritat general (PRI) és 20 i la prioritat d’usuari nice (NI) està a 0. Baixem ara al mínim la prioritat nice:

**renice 30 132566 - (132566 (process ID) prioridad anterior 0, nueva prioridad 19)**

Es el resultado de la salida renice 

<img width="560" height="72" alt="image" src="https://github.com/user-attachments/assets/667419ed-3957-4dac-98bf-ba50f4d113ab" />

Ara farem servir la utilitat top per donar al procés la prioritat màxima. Arranquem la utilitat interactiva:

Este es el resultado de la salida Top

<img width="1160" height="438" alt="image" src="https://github.com/user-attachments/assets/d42c69ef-b4f7-4733-a442-644de20ace7c" />

el Top me da un error y no me deja continuar 

