
Preparació i Modificació del Kernel Linux 6.8.6

Aquest document detalla el procediment tècnic realitzat per preparar l'entorn de desenvolupament, descarregar el codi font original (Vanilla) del nucli Linux i aplicar-hi una modificació personalitzada en el codi d'inicialització.

1. Configuració i Verificació del Sistema
Abans d'iniciar la manipulació del nucli, s'ha configurat el sistema de fitxers i verificat l'estat actual de la màquina.

1.1. Esquema de Particionament
Durant la instal·lació del sistema operatiu (Ubuntu), s'ha definit un particionament manual per garantir espai suficient per a la compilació i l'àrea d'intercanvi (swap). S'ha configurat /dev/sda amb particions separades per a EFI, Swap (20GB), Arrel (20GB) i Home.

<img width="846" height="643" alt="1" src="https://github.com/user-attachments/assets/22bdaa85-71f4-4ec5-96dc-01978bc05403" />

1.2. Verificació de la Memòria d'Intercanvi (Swap)
Es valida que la partició d'intercanvi estigui activa, ja que la compilació del kernel és un procés intensiu que pot requerir més memòria de la que disposa la RAM física.

Comanda: swapon --show


<img width="673" height="98" alt="2" src="https://github.com/user-attachments/assets/8e85f638-627d-4fc8-9874-8b1e2129f60f" />

1.3. Versió del Nucli Actual
Es comprova la versió del nucli que s'està executant actualment abans de realitzar cap actualització o canvi.

Comanda: uname -r

Resultat: 6.8.0-87-generic


<img width="552" height="93" alt="3" src="https://github.com/user-attachments/assets/36167291-0251-4e93-8655-c0aaa7439900" />


2. Gestió de Dependències i Entorn de Compilació
Per poder compilar el codi font, és imprescindible descarregar les eines de construcció (build tools) i les llibreries de desenvolupament necessàries.

2.1. Habilitació de Repositoris de Codi Font
S'edita el fitxer de configuració dels repositoris APT per permetre la descàrrega de paquets de codi font (deb-src). S'han descomentat les línies corresponents als repositoris main, restricted, universe i multiverse.

Fitxer: /etc/apt/sources.list


<img width="851" height="776" alt="4" src="https://github.com/user-attachments/assets/10d2e58d-11ee-4e19-abce-d9a55c4c4e4b" />

2.2. Actualització de la Llista de Paquets
Un cop modificats els repositoris, s'actualitza l'índex local de paquets per aplicar els canvis.

Comanda: sudo apt update

<img width="660" height="96" alt="5" src="https://github.com/user-attachments/assets/554b8ebe-12f4-48ee-b5cd-10110eef458d" />


2.3. Instal·lació de Paquets de Desenvolupament
S'instal·len les eines essencials per a la compilació del kernel, incloent-hi compiladors (gcc, g++), make, i llibreries específiques (ncurses per a menús, ssl per a signatures, etc.).

Comanda: apt install -y build-essential libncurses-dev flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf dwarves


<img width="858" height="561" alt="6" src="https://github.com/user-attachments/assets/bee0acbc-12e7-4025-8654-61c0a3c767b1" />

3. Obtenció del Codi Font (Kernel Vanilla)
Es procedeix a obtenir el codi net i sense modificacions directament des dels repositoris oficials de Linux.

3.1. Descàrrega de l'Arxiu
Des del navegador web, s'accedeix a cdn.kernel.org i es localitza la versió específica del nucli amb la qual es vol treballar.

Versió objectiu: Linux 6.8.6 (linux-6.8.6.tar.gz)

<img width="1377" height="826" alt="7" src="https://github.com/user-attachments/assets/171fe82a-ea23-4ddc-9176-9f57a98c85ab" />

3.2. Descompressió del Codi
Un cop descarregat el fitxer comprimit, s'extreu el seu contingut al directori de treball per accedir a l'arbre de directoris del codi font.

Comanda: tar -xvf linux-6.8.6.tar.gz

<img width="689" height="31" alt="8" src="https://github.com/user-attachments/assets/81c9b5a3-e02e-438d-a7c7-626d73a705e3" />

4. Modificació del Codi Font (Customització)
L'objectiu final d'aquesta fase és injectar una línia de codi personalitzada que s'executi durant l'arrencada del sistema operatiu.

4.1. Còpia de Seguretat
Abans de modificar qualsevol fitxer del sistema, es realitza una còpia de seguretat del fitxer que conté la funció principal d'inicialització.

Fitxer original: init/main.c

Comanda: cp init/main.c init/main.c.copia

<img width="757" height="83" alt="9" src="https://github.com/user-attachments/assets/831a6515-6353-4c14-9d2a-2c7928eea90c" />


4.2. Edició i Injecció de Codi
S'edita el fitxer init/main.c i es localitza la funció start_kernel(void). S'afegeix una crida a pr_notice per imprimir un missatge d'alerta als logs del sistema just després de carregar el bàner de Linux.

<img width="858" height="749" alt="10" src="https://github.com/user-attachments/assets/69018c24-9476-4eec-90dd-f7e0944949cd" />


5. Gestió de Canvis i Configuració Base
Un cop modificat el codi font, és bona pràctica generar un fitxer de diferències (patch) i preparar la configuració base del nucli utilitzant la del sistema actual.

5.1. Creació i Aplicació del Pedaç (Patch)
Es genera un fitxer .patch que conté les diferències entre el fitxer original i el modificat. Posteriorment, s'aplica aquest pedaç per validar que el sistema de patching funciona correctament i es verifica que la línia d'advertència ("ADVERTENCIA") existeix al codi.

Comandes:

diff -u init/main.c init/main.c.copia > parche-edgar.patch

patch -p0 < parche-edgar.patch 

grep "ADVERTENCIA" | init/main.c

<img width="891" height="156" alt="11" src="https://github.com/user-attachments/assets/9283bbcf-db63-4926-9186-941d4fb06267" />

5.2. Importació de la Configuració Actual
Per no començar la configuració des de zero, es copia el fitxer de configuració del nucli que s'està executant actualment (/boot/config-6.8.0-87-generic) a la carpeta del codi font, anomenant-lo .config.

Comanda: cp /boot/config-6.8.0-87-generic .config



<img width="900" height="93" alt="12" src="https://github.com/user-attachments/assets/68e2b91f-0c70-4111-bfbb-9751ced5e4ec" />

5.3. Actualització de la Configuració (Oldconfig)
S'executa l'eina per adaptar l'antiga configuració a la nova versió del kernel (6.8.6). Aquest procés pregunta com configurar les noves funcionalitats que no existien a la versió anterior.

Comanda: make oldconfig


<img width="931" height="773" alt="13" src="https://github.com/user-attachments/assets/0164fbeb-dff8-4d59-b747-d9073d79ec78" />




6. Personalització via Menú Gràfic
Es realitza una personalització més fina de les característiques del nucli mitjançant la interfície gràfica de terminal (ncurses).

7.1. Accés al Menú de Configuració
S'inicia l'eina gràfica per navegar per les opcions del kernel.

Comanda: make menuconfig
<img width="812" height="299" alt="14" src="https://github.com/user-attachments/assets/366ac3ba-739a-45c8-aaf3-a53d4be1a00c" />

6.2. Desactivació de Mòduls de Xarxa
Com a exemple de personalització (o hardening), es desactiven certes funcionalitats de xarxa i drivers específics, com ara el suport TCP/IP (en aquest cas sembla una prova dràstica) o el filtratge VLAN.

Acció: Desmarcar opcions dins de "Networking options".


<img width="1158" height="738" alt="15" src="https://github.com/user-attachments/assets/d123450d-5fe5-491e-ace9-4673549952e4" />


7. Ajustament i Neteja de la Configuració (.config)
Abans de compilar, és necessari editar manualment paràmetres crítics dins del fitxer .config per evitar errors de certificats i reduir el temps de compilació.

7.1. Eliminació de Claus de Confiança (Trusted Keys)
S'edita el fitxer .config per buidar o modificar les variables relacionades amb els certificats de signatura de Canonical/Debian, ja que no disposem de les claus privades originals per signar el nou kernel.

Paràmetres: CONFIG_SYSTEM_TRUSTED_KEYS i CONFIG_SYSTEM_REVOCATION_KEYS.

<img width="849" height="751" alt="16" src="https://github.com/user-attachments/assets/623b189e-b19c-44df-b132-55e1d2dcbef6" />


7.2. Desactivació de la Depuració (Debug Info)
Per reduir dràsticament la mida del nucli resultant i accelerar el procés de compilació, es desactiva la generació d'informació de depuració.

Canvi: S'estableix CONFIG_DEBUG_INFO=n i es desactiven les opcions relacionades amb BTF.


<img width="848" height="786" alt="17" src="https://github.com/user-attachments/assets/44b78ac2-d036-4189-8db9-b58d07a906e2" />

8. Compilació i Empaquetament
Aquesta fase implica la preparació de les eines d'empaquetament Debian i la construcció final dels paquets instal·lables.

8.1. Resolució de Dependències de Empaquetament
S'intenta instal·lar kernel-package. En detectar errors de dependències faltants (xmlto, gettext, etc.), s'executa una comanda per corregir l'arbre de dependències automàticament.

Comanda: sudo apt -f install


<img width="856" height="536" alt="18" src="https://github.com/user-attachments/assets/6ea93392-5b91-419e-a5e5-a89721ffe646" />


8.2. Compilació del Kernel (Make kpkg)
S'inicia el procés de compilació utilitzant make-kpkg. Aquesta eina compila el codi font i genera fitxers .deb (imatge del kernel i capçaleres) llestos per instal·lar, facilitant la gestió posterior.

Comanda: make-kpkg --initrd kernel_image kernel_headers


<img width="1208" height="420" alt="19" src="https://github.com/user-attachments/assets/2e2fcda5-a5fe-4002-9cb0-ac541ccc0ac7" />


8.3. Instal·lació del Nou Kernel
Un cop finalitzada la compilació, s'instal·len els paquets .deb generats (que apareixen al directori superior). Això instal·la el nucli a /boot, actualitza el initramfs i reconfigura el gestor d'arreVerificació Final (Logs del Sistema)
Després de reiniciar la màquina amb el nou kernel 6.8.6, es verifica que la modificació del codi C (el pr_notice afegit a main.c) s'ha executat correctament.

Comanda: cat /var/log/syslog | grep "ADVERTENCIA"

Resultat: El filtre troba la línia injectada:

"ADVERTENCIA! Els logs del sistema han detectat un accés no autoritzat."

Conclusió: Això confirma que el kernel personalitzat s'ha carregat, executat i que la modificació en el codi font és funcional.ncada GRUB automàticament.

Comanda: dpkg -i linux-image-6.8.6...custom...deb


<img width="1138" height="575" alt="20" src="https://github.com/user-attachments/assets/70a5532e-6b50-4d71-bf43-0bf590a83248" />

Configuració de Certificats de Signatura (Pas previ a la compilació)
Abans de compilar, és necessari modificar el fitxer de configuració per evitar errors relacionats amb les claus de signatura oficials d'Ubuntu/Debian, de les quals no disposem.

Fitxer: .config (a l'arrel del codi font).

Acció: S'editen les línies CONFIG_SYSTEM_TRUSTED_KEYS i CONFIG_SYSTEM_REVOCATION_KEYS.

Detall tècnic: S'eliminen els valors predeterminats ("debian/canonical-certs.pem", etc.) i es deixen les cometes buides "". Això evita que el procés de compilació falli en intentar buscar uns certificats privats que no tenim.



<img width="1027" height="216" alt="21" src="https://github.com/user-attachments/assets/273059fe-2575-4cff-9500-69d3209b004d" />


Configuració del Gestor d'Arrencada (GRUB)
Un cop instal·lat el nou kernel, es configura el GRUB per assegurar-nos que podem veure el menú d'arrencada i seleccionar el nou nucli si no arrenca automàticament.

Fitxer: /etc/default/grub

Acció: Es comenta (s'afegeix un # al davant) la línia GRUB_TIMEOUT_STYLE=hidden.

Objectiu: Forçar que el menú del GRUB es mostri sempre durant l'inici, permetent l'elecció manual del sistema operatiu o versió del kernel.


<img width="1090" height="740" alt="22" src="https://github.com/user-attachments/assets/28921e40-2955-4655-bb78-4b5a675a15a3" />


Actualització del GRUB
Després de modificar la configuració o instal·lar nous nuclis, és obligatori actualitzar el carregador perquè detecti els canvis.

Comanda: update-grub

Sortida observada: El sistema detecta les imatges del nucli instal·lades:

linux-image-6.8.6 (El nou kernel compilat).

linux-image-6.8.0-87-generic (El kernel original).

Resultat: Es genera un nou fitxer grub.cfg que inclou la nova versió 6.8.6 al menú d'inici.


<img width="881" height="310" alt="23" src="https://github.com/user-attachments/assets/3cbeaffe-0336-402e-8d23-9b95949ac491" />

Verificació Final (Logs del Sistema)
Després de reiniciar la màquina amb el nou kernel 6.8.6, es verifica que la modificació del codi C (el pr_notice afegit a main.c) s'ha executat correctament.

Comanda: cat /var/log/syslog | grep "ADVERTENCIA"

Resultat: El filtre troba la línia injectada:

"ADVERTENCIA! Els logs del sistema han detectat un accés no autoritzat."

Conclusió: Això confirma que el kernel personalitzat s'ha carregat, executat i que la modificació en el codi font és funcional.



<img width="1200" height="107" alt="24" src="https://github.com/user-attachments/assets/61483387-3d11-493e-a370-38ba74f1b23b" />

