Configuració de la interfície de xarxa IPv4 amb l'adreça IP estàtica 192.168.2.101 i el servidor DNS apuntant a la pròpia màquina per a la gestió del domini local.

<img width="466" height="486" alt="1" src="https://github.com/user-attachments/assets/3bc9c9f2-262d-43fe-b602-daf4a6e0b2b5" />


Comprovació de connectivitat mitjançant l'ordre ping des d'un sistema extern cap a la IP del servidor 192.168.2.101, confirmant que el servidor respon correctament a la xarxa.

<img width="1141" height="459" alt="2" src="https://github.com/user-attachments/assets/fab4024c-631a-48ff-9b4f-a5504f5efba4" />


Administració del servidor DNS on es mostra la creació d'un registre Host (A) anomenat "edgar" dins de la zona de cerca directa edgar.local, vinculat a la IP 10.0.2.6.

<img width="1105" height="802" alt="3" src="https://github.com/user-attachments/assets/67e33050-ce85-4723-a32a-d84f2edf6e9a" />


Verificació de la resolució de noms amb l'ordre nslookup edgar.edgar.local, on el servidor DNS respon correctament associant el nom del domini amb la IP 10.0.2.6.

<img width="843" height="372" alt="4" src="https://github.com/user-attachments/assets/fbcc40dd-b663-4dff-8abe-5d815391eed7" />


Accés al servidor web mitjançant HTTP des del navegador, on es visualitza el contingut del fitxer index.html mostrant el missatge "Hola" sota el domini edgar.edgar.local.

<img width="924" height="503" alt="5" src="https://github.com/user-attachments/assets/1addcefe-835c-4b15-9737-c5ac274b9ee6" />


Vista de l'explorador de fitxers mostrant la ruta C:\inetpub\wwwroot on s'ha allotjat el fitxer index.html necessari per al contingut del servidor web IIS.

<img width="840" height="558" alt="6" src="https://github.com/user-attachments/assets/98965051-e776-4e08-b8f4-c208b15dad8f" />


Execució de l'ordre certtmpl.msc des de la finestra "Executar" per obrir la consola de gestió de plantilles de certificat del sistema.

<img width="411" height="228" alt="7" src="https://github.com/user-attachments/assets/3a153aed-ef0d-4033-88c7-076347488162" />


Consola de plantilles de certificat on es visualitza la llista completa de plantilles disponibles, incloent la plantilla personalitzada "webserversan" amb versió d'esquema 2.

<img width="903" height="715" alt="8" src="https://github.com/user-attachments/assets/e49112e9-9dbb-46b8-89e5-7b6179697c0f" />


Ús de l'eina certreq per crear una nova sol·licitud de certificat (web.req) basada en la configuració del fitxer web.inf.

<img width="532" height="197" alt="9" src="https://github.com/user-attachments/assets/b9607299-8636-492b-aa78-9a7276d94db5" />


Tramitació final de la sol·licitud de certificat amb l'ordre certreq -submit, on el certificat ha estat finalment emès per l'Entitat de Certificació amb l'ID de sol·licitud 9.

<img width="641" height="229" alt="10" src="https://github.com/user-attachments/assets/957ef89e-d86c-4d6d-96ec-41761a874b80" />

Configuració del lligam (binding) de lloc web segur a l'IIS, on s'assigna el protocol HTTPS a través del port 443 i se selecciona el certificat SSL emès prèviament per al domini edgar.edgar.local.

<img width="527" height="422" alt="11" src="https://github.com/user-attachments/assets/c17b9d26-10ac-4025-b015-5a67e0a0bd39" />

Verificació final de la seguretat del servidor mitjançant el navegador, on es confirma l'accés satisfactori a https://edgar.edgar.local amb el missatge "Servidor de Edgar porfin es seguro!" i la presència de la icona del cadenat que indica una connexió xifrada i segura.

<img width="925" height="453" alt="12" src="https://github.com/user-attachments/assets/f4ab39bf-583a-4da3-ae88-2f3049b04c0a" />
