En aquest primer pas s'inicia la configuració del servidor promovent-lo a Controlador de Domini, on se selecciona l'opció d'afegir un nou bosc i s'estableix edgar.local com a nom del domini arrel per a l'organització.

<img width="768" height="559" alt="1" src="https://github.com/user-attachments/assets/ce9f11ee-f7bc-4af6-8530-418e331b1f78" />

Es mostra la interfície de creació d'objectes dins d'Usuaris i equips de l'Active Directory, presentant el formulari buit que s'utilitzarà per donar d'alta nous usuaris definint el seu nom real i el nom d'inici de sessió.

<img width="438" height="384" alt="2" src="https://github.com/user-attachments/assets/f5e4504e-fe90-4d6f-934b-e5c9ab272d95" />

Aquesta imatge presenta l'entorn de l'equip client, una màquina virtual amb Windows 10, que es troba a l'escriptori a punt per començar amb les configuracions de xarxa necessàries per connectar-se al servidor.

<img width="1270" height="805" alt="3" src="https://github.com/user-attachments/assets/1a6a9f6e-e02a-4057-b94b-94928585368c" />

Dins les propietats del sistema del client Windows 10, es procedeix a canviar la pertinença de l'equip d'un Grup de treball a un Domini, escrivint el nom edgar.local per iniciar la sol·licitud d'unió a la xarxa corporativa.

<img width="840" height="754" alt="4" src="https://github.com/user-attachments/assets/d4de4f5d-f960-4a5b-ba79-8958b1342c11" />

Per garantir la connectivitat amb el servidor, es configura manualment el protocol IPv4 del client assignant la IP 10.10.1.2 i establint com a Servidor DNS preferit l'adreça 10.10.1.1, que correspon al Controlador de Domini.

<img width="788" height="650" alt="5" src="https://github.com/user-attachments/assets/ac787426-3a50-45f3-919c-79c6cc583626" />

Després d'introduir les credencials d'administrador i validar la configuració, el sistema operatiu del client mostra un missatge de confirmació indicant que l'equip s'ha unit correctament al domini edgar.local.

<img width="680" height="516" alt="6" src="https://github.com/user-attachments/assets/1f0b4b6f-e793-4f7d-803e-f8aafeb7c692" />


De tornada al servidor, s'accedeix a les propietats d'un compte d'usuari específic anomenat vpn_edgar per verificar o modificar les seves dades generals, assegurant que el perfil estigui configurat correctament.

<img width="455" height="539" alt="7" src="https://github.com/user-attachments/assets/6dbf0aaa-73e3-45d5-b745-2be71fc4b5f2" />


Al llistat d'usuaris del Directori Actiu es pot observar la creació de diversos comptes destinats a proves o serveis específics, visualitzant-se aquí l'existència dels usuaris vpn_edgar i vpn_edgar2.

<img width="478" height="58" alt="8" src="https://github.com/user-attachments/assets/c3207aab-cb87-4930-ad7f-0ba520643cb2" />


Aquesta imatge serveix com a validació final de la primera fase mostrant una comparativa on a l'esquerra apareix l'usuari usuari creat al servidor i a la dreta es veu que aquest ha pogut iniciar sessió exitosament al client Windows 10.

<img width="1504" height="805" alt="9" src="https://github.com/user-attachments/assets/17e62287-02d7-47ab-becc-5ccd521e4fb8" />


Es mostra la llista completa d'usuaris a l'eina d'administració del servidor, destacant la selecció d'un usuari anomenat messi per confirmar que es poden gestionar i visualitzar correctament tots els membres afegits al domini.

<img width="462" height="263" alt="10" src="https://github.com/user-attachments/assets/e775f359-8c0f-42ae-a1c0-9963a48ce9a2" />

Com a pas previ per evitar conflictes de connectivitat durant la configuració de la VPN, es procedeix a desactivar el Firewall del Windows Defender en tots els perfils de xarxa, assegurant que el trànsit no sigui bloquejat.

<img width="788" height="638" alt="11" src="https://github.com/user-attachments/assets/5f4b0273-72d8-4665-bd2f-c797153e5076" />


El procés d'instal·lació comença a l'assistent per afegir rols i característiques del servidor, on es marquen les caselles corresponents als rols d'Accés remot i Serveis d'accés i directives de xarxes.

<img width="815" height="580" alt="12" src="https://github.com/user-attachments/assets/366efd07-519a-4771-9cd7-3885572b34a8" />


Dins la selecció de serveis del rol per a Accés remot, s'habilita específicament l'opció "DirectAccess i VPN (RAS)", component fonamental que permetrà gestionar les connexions de xarxa privada virtual.

<img width="798" height="571" alt="13" src="https://github.com/user-attachments/assets/1fd98b65-c59d-4393-8929-b017d14ea3cc" />


El sistema mostra el progrés de la instal·lació de les característiques seleccionades al servidor de destinació, confirmant que s'estan instal·lant les eines d'administració remota i els components necessaris.

<img width="803" height="569" alt="14" src="https://github.com/user-attachments/assets/4450f5a8-b4d7-4898-866e-d01634df5c31" />

Un cop instal·lats els rols, s'inicia l'assistent de configuració d'accés remot i se selecciona l'opció "Implementar només VPN", la qual cosa permet configurar la consola específicament per a connexions VPN tradicionals.


<img width="648" height="535" alt="15" src="https://github.com/user-attachments/assets/e263b26b-8879-4c9b-a2f4-490250a9d04e" />


En obrir-se l'assistent per a la instal·lació del servidor d'enrutament i accés remot, es tria l'opció de configuració estàndard per permetre que els clients remots es connectin a aquest servidor a través d'una 
connexió segura.


<img width="712" height="517" alt="16" src="https://github.com/user-attachments/assets/05bcc627-9732-4f28-8ad6-d688215f5457" />


A la pantalla de selecció de serveis específics, es marca únicament la casella "VPN" per habilitar el servidor com a porta d'enllaç virtual, deixant desmarcada l'opció d'accés telefònic.

<img width="509" height="485" alt="17" src="https://github.com/user-attachments/assets/65c1cd11-5415-41c9-8fc3-c8a438880dcf" />


L'assistent sol·licita identificar la interfície de xarxa que connecta aquest servidor a Internet o a la xarxa local; se selecciona la interfície "Ethernet 2" amb la IP 10.10.1.1, que actuarà com a punt d'entrada.


<img width="497" height="481" alt="18" src="https://github.com/user-attachments/assets/d02d36d4-8e44-4bf9-ba5a-0cbe48a7ee54" />


Per a la gestió d'adreces IP dels clients que es connectin, s'opta per la configuració "D'un interval d'adreces especificat", permetent definir un pool estàtic d'IPs en lloc de dependre d'un servidor DHCP.


<img width="505" height="491" alt="19" src="https://github.com/user-attachments/assets/67e71794-7904-43b1-a362-0f6e8a82737f" />

Finalment, es defineix el rang d'adreces IPv4 que s'assignaran als clients remots, establint un interval que va des de la 172.16.0.0 fins a la 172.16.0.10, atorgant un total d'11 adreces disponibles.


<img width="727" height="491" alt="20" src="https://github.com/user-attachments/assets/dc95eee6-31f4-4224-af41-44a2c7115ce9" />


L'assistent pregunta sobre l'autenticació amb un servidor extern; se selecciona "No, utilitzar Enrutament i accés remot per autenticar les sol·licituds" per gestionar-ho localment al servidor.


<img width="515" height="489" alt="21" src="https://github.com/user-attachments/assets/16d3b084-d917-40e2-af01-67b7ece4d8d3" />


Es mostra el resum final de l'assistent, confirmant que els clients es connectaran a la interfície pública "Ethernet 2" i rebran adreces de la xarxa especificada.


<img width="660" height="482" alt="22" src="https://github.com/user-attachments/assets/cabc627b-7eaa-4199-8ee4-480f82af9574" />


Un cop finalitzat l'assistent, la consola mostra el servidor (WIN-N34...) amb la icona en verd, indicant que el servei "Enrutament i accés remot" està configurat i operatiu.


<img width="758" height="523" alt="23" src="https://github.com/user-attachments/assets/dc759e02-81b4-425f-8c87-433c03f2e27a" />


S'accedeix a les propietats de l'usuari usuari a l'Active Directory, i a la pestanya "Marcatge" (Dial-in), es marca "Permetre accés" a la secció de Permís d'accés a xarxes.


<img width="811" height="613" alt="24" src="https://github.com/user-attachments/assets/7450695c-be64-4483-80fc-897bb9a4b82e" />


Es repeteix el mateix procediment per a l'usuari messi, assegurant que la configuració de "Permetre accés" estigui habilitada per permetre-li establir la connexió VPN.


<img width="467" height="553" alt="25" src="https://github.com/user-attachments/assets/4e0c74c7-b526-45a8-af8b-bde6781ad505" />


Es verifiquen les propietats de l'adaptador de xarxa "Ethernet 2" al servidor per assegurar que els protocols necessaris, com el Protocol d'Internet versió 4 (TCP/IPv4), estiguin marcats i actius.


<img width="435" height="496" alt="26" src="https://github.com/user-attachments/assets/0ba1bc35-e7b1-4c20-9cda-432140b98ccd" />


Ja a l'equip client (Windows 10), s'inicia l'assistent per "Configurar una connexió o xarxa" i es tria l'opció "Connectar-se a una àrea de treball".


<img width="613" height="449" alt="27" src="https://github.com/user-attachments/assets/f3bf867c-0f4d-4d17-8b27-76b1730c8c1a" />


A la pregunta de com es desitja connectar, se selecciona l'opció "Utilitzar la meva connexió a Internet (VPN)" per crear el túnel virtual a través de la xarxa existent.


<img width="616" height="457" alt="28" src="https://github.com/user-attachments/assets/c34c3075-3384-40c9-a423-a25531ae8896" />


Durant la configuració, es tria l'opció "Configuraré més tard una connexió a Internet" per saltar passos de configuració automàtica i procedir a definir els paràmetres manualment.


<img width="608" height="457" alt="29" src="https://github.com/user-attachments/assets/abc61227-f601-47be-8eb9-42d5ce353588" />


Finalment, s'introdueix l'adreça del servidor VPN al camp "Adreça d'Internet", escrivint la IP 10.10.1.1, i s'assigna un nom de destí com "Connexió VPN".


<img width="613" height="471" alt="30" src="https://github.com/user-attachments/assets/dbf733d6-6cb4-4515-b795-d1f3b071a6af" />


Després d'iniciar la connexió, el panell de configuració de Windows mostra l'estat "Connectat" sota "Connexió VPN", confirmant que el túnel s'ha establert correctament.


<img width="447" height="123" alt="31" src="https://github.com/user-attachments/assets/e3170bcd-edc5-4d0f-85a2-6829271acd56" />


A la configuració de la màquina virtual (VirtualBox), s'afegeix un nou dispositiu d'emmagatzematge, seleccionant un disc dur virtual (VDI) de 5,00 GB per utilitzar-lo com a espai de dades.


<img width="867" height="536" alt="32" src="https://github.com/user-attachments/assets/a4511db5-6527-4b07-9a69-cb6cd87fd92a" />


Dins del servidor, a l'administrador de discs, s'inicialitza i es formateja el nou "Disc 1" de 5 GB, creant un "Nou volum" amb sistema de fitxers NTFS llest per emmagatzemar dades.


<img width="777" height="357" alt="33" src="https://github.com/user-attachments/assets/1267cf47-5849-446b-864c-3594f4005760" />


A l'Explorador de fitxers, dins del nou volum creat (D:), es generen dues carpetes noves anomenades accesso_messi i accesso_usuari per organitzar els fitxers de cada usuari.


<img width="691" height="410" alt="34" src="https://github.com/user-attachments/assets/189d5c50-74db-4291-9208-b7592d82f2ae" />


S'obre la configuració de xarxa per compartir la carpeta accesso_messi, afegint l'usuari messi a la llista i atorgant-li permisos de "Lectura i escriptura".


<img width="620" height="482" alt="35" src="https://github.com/user-attachments/assets/6bd15ca1-f2cc-4b6c-8545-cb249c69c230" />


De manera similar, es configura la carpeta accesso_usuari, afegint l'usuari usuari i assignant-li també el nivell de permís "Lectura i escriptura".


<img width="651" height="481" alt="36" src="https://github.com/user-attachments/assets/a52bc953-8ac1-468c-92ed-da69f47fd572" />


Per afinar la seguretat, s'accedeix als permisos avançats de la carpeta accesso_usuari, verificant que l'usuari tingui marcades les caselles de "Control total", "Canviar" i "Llegir".


<img width="433" height="510" alt="37" src="https://github.com/user-attachments/assets/01291b03-44c1-4263-842e-08404c36a4b9" />


Es repeteix la verificació de permisos avançats per a la carpeta accesso_messi, confirmant que l'usuari messi apareix llistat amb els permisos adequats per gestionar els seus fitxers.


<img width="516" height="511" alt="38" src="https://github.com/user-attachments/assets/431a8859-a6df-41f3-a38d-e58a304ac026" />


Des del client Windows 10 (amb sessió iniciada com a messi), s'accedeix a través de l'explorador a la ruta de xarxa \\192.168.2.201\accesso_messi, visualitzant el contingut de la carpeta remota.


<img width="906" height="736" alt="39" src="https://github.com/user-attachments/assets/ff99135c-2b75-4c2e-8fbe-93e0cbc31d38" />



Finalment, es mostra l'interior de la carpeta compartida accesso_messi des del client, on es veu un fitxer de text de prova, demostrant que l'accés de lectura i escriptura a través de la xarxa funciona correctament.


<img width="870" height="841" alt="40" src="https://github.com/user-attachments/assets/7d8e6eae-ba2d-445b-8849-233546cb6896" />


Finalment, es mostra l'accés des del client a la carpeta accesso_usuari a través de la xarxa, on es crea un document de text anomenat "usuari", demostrant que l'altre usuari també té accés al seu espai privat.


<img width="791" height="634" alt="42" src="https://github.com/user-attachments/assets/696c26a4-94df-4fa0-ac51-aeac960e5c67" />
