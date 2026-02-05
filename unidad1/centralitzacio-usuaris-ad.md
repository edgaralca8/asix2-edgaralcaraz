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


Script Bash executat al client Ubuntu per automatitzar la instal·lació dels paquets necessaris (realmd, sssd, adcli) i la configuració del sistema per a la unió al domini edgar.local.


<img width="855" height="944" alt="1ubuntu" src="https://github.com/user-attachments/assets/5955e5cd-57e3-430f-a230-742148b18219" />


Configuració manual del fitxer /etc/resolv.conf on s'especifica el servidor DNS del domini (192.168.2.101) per garantir que el client pugui localitzar el controlador de domini Windows.


<img width="861" height="606" alt="2ubuntu" src="https://github.com/user-attachments/assets/456adb07-3f58-49b0-a387-582997790859" />

Inici de l'execució de l'script d'unió, realitzant la descàrrega de les llistes de paquets i la verificació de les dependències de programari al repositori oficial d'Ubuntu.

<img width="868" height="837" alt="3ubuntu" src="https://github.com/user-attachments/assets/a553c938-67a2-4c27-9b82-9f33a151e0cf" />


Finalització de la instal·lació de paquets i transició a la Fase 2, on el sistema sol·licita l'adreça IP del servidor Windows Server per procedir amb la configuració de l'Active Directory DNS.


<img width="889" height="945" alt="4ubuntu" src="https://github.com/user-attachments/assets/9364fd4c-6989-4a96-9c89-10ba9e47da51" />


Confirmació de l'èxit del procés: s'ha configurat l'accés sudo per als administradors del domini i s'informa que el client ja pot acceptar inicis de sessió d'usuaris d'Active Directory.


<img width="774" height="164" alt="5ubuntu" src="https://github.com/user-attachments/assets/2d24a0e0-b82f-4c58-b7a1-35929a86bbb2" />


Gestió d'usuaris des del servidor Windows: verificació de les propietats del compte de l'usuari "mireia2" dins de la unitat organitzativa d'Active Directory abans de provar l'accés des de Linux.


<img width="863" height="676" alt="6ubuntu" src="https://github.com/user-attachments/assets/98c43499-5381-4d96-86d1-8d0ec988fe32" />


Validació de l'inici de sessió al terminal d'Ubuntu amb l'usuari mireia2@edgar.local, on el sistema confirma la creació automàtica del directori personal (home) de l'usuari.


<img width="674" height="68" alt="7ubuntu" src="https://github.com/user-attachments/assets/3718167a-0210-49b4-933b-16b48a99e2fa" />


Interfície d'inici de sessió gràfica d'Ubuntu reconeixent l'usuari del domini mireia2@edgar.local, demostrant la integració completa del client Linux en l'ecosistema de Windows Server.


<img width="523" height="313" alt="8ubuntu" src="https://github.com/user-attachments/assets/9304208f-1788-4811-bdb4-9616665799c9" />


Sessió d'escriptori activa d'Ubuntu amb l'usuari de domini connectat, verificant el nom d'usuari i la màquina mitjançant el prompt del terminal.


<img width="722" height="306" alt="9ubuntu" src="https://github.com/user-attachments/assets/dea9721c-ece3-45f8-9b8e-6cfaaac22d56" />
