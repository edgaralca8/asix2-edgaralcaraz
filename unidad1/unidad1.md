Aquesta imatge mostra dos fitxers de configuració del sistema (systemd) que serveixen per executar l'script anterior de forma automàtica.

capture_service.service: És el fitxer que li diu al sistema què ha d'executar. La línia clau és ExecStart, que bàsicament crida a l'script de la imatge 2.


capture_target.target : Aquest fitxer s'encarrega de quan s'ha d'activar el servei. Està configurat per arrencar quan el sistema s'inicia (WantedBy=multi-user.target)

<img width="1208" height="523" alt="image" src="https://github.com/user-attachments/assets/a8d71e7f-d000-4f0f-bfaf-87e43cadd936" />
<img width="1284" height="811" alt="image" src="https://github.com/user-attachments/assets/7d43f955-c53b-49ff-a8e6-3c975c82867f" />
Aquesta imatge mostra el fitxer /usr/local/bin/capture_service.sh. Aquest és l'script que fa
tota la feina:
Configuració: Al principi, es defineix a quin email s'envia (EMAIL_TO), l'assumpte
(SUBJECT) i el text del correu (BODY). També es fixa un interval de 60 segons.
Bucle: Hi ha un bucle infinit (while true: do) que fa el següent:
Fa una captura de pantalla amb gnome-screenshot.
Envia la captura per correu amb mail.
Espera 60 segons (sleep) abans de tornar a començar.
<img width="1276" height="802" alt="image" src="https://github.com/user-attachments/assets/1033014a-c593-423f-afa1-9d55e9062c98" />
Prova de funcionament:
<img width="1763" height="644" alt="image" src="https://github.com/user-attachments/assets/2a60d1f8-67e9-498a-82e9-a04244dfebe3" />
