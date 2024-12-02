# Marquez_Calero_Carlos_Arquitectura_En_3_Capas

## ÍNDICE
#### 1. INTRODUCCIÓN
#### 2. OBJETIVOS
#### 3. DESARROLLO
#### 4. DOMINIO

### 1. INTRODUCCIÓN
En esta práctica se implementará una arquitectura LAMP para WordPress distribuida en tres niveles. En la capa 1, un balanceador de carga distribuirá el tráfico entre dos servidores backend en la capa 2, donde se ejecutarán Apache y PHP conectados a un servidor NFS para almacenamiento compartido. Finalmente, en la capa 3, un servidor MySQL gestionará la base de datos, asegurando un diseño escalable, redundante y eficiente.

### 2. OBJETIVO
El objetivo de esta práctica es diseñar e implementar una arquitectura LAMP en tres niveles para alojar WordPress, garantizando escalabilidad, redundancia y eficiencia. Esto incluye configurar un balanceador de carga, servidores backend con acceso a almacenamiento compartido mediante NFS y un servidor MySQL para la gestión centralizada de la base de datos.

### 3. DESARROLLO

#### 3.1 Creación de las VPCs
Para esta practica que desarrollaremos en AWS, necesitaremos crear un Virtual Private Network o VPC. Esta VPC dispondrá de 3 subredes, una de ellas será **Pública**, esta estará conectada a una instancia situada en la capa 1 de nuestro entorno, cuya función será la de actuar como un Balanceador de Carga. Las otras dos subredes **Privadas** estaran conectadas a las instancias que se encuentren en la capa 2 y en la capa 3, es decir, los servidores Backend, NFS y MySQL.

##### Paso 1: Asignamos un nombre a nuestra nueva VPC y definimos su bloque CIRD IPv4:
![image](https://github.com/user-attachments/assets/25461ddd-61d9-4e03-8deb-28d05cee460e)

##### Paso 2: Definimos el numero de zonas de disponibilidad y la cantidad de subredes públicas y privadas:
![image](https://github.com/user-attachments/assets/eadd99c7-541a-447f-9635-30c011b6d66a)

##### Paso 3: Le damos click al botón de **Crear VPC** y esperamos a que el proceso finalize:
![image](https://github.com/user-attachments/assets/5f5861d6-acdc-4c73-aa62-a4299f12f7d1)

##### Paso 4: Comprobamos que se ha creado la vpc  y las subredes de esta de forma correcta:
![image](https://github.com/user-attachments/assets/9c1b8299-339a-43cc-a8be-fc994f955f4e)
![image](https://github.com/user-attachments/assets/296fe761-524c-4c95-8e30-f646b4d51deb)

#### 3.2 Creación de Instancias
A continuación nos dispondremos a crear una serie de instancias con una AMI de Ubuntu-Server 24.04. Una de ellas será la encargada de balancear las solicitudes recibidas desde internet, situada en la primera de las tres capas de nuestro despliege, hacia los servidores bakend, situada en la segunda de las tres capas de nuestro despliege, las cuales se conectarán al servidor de MySQL, situado este útimo en la capa 3 de nuestro despliegue en 3 capas. En este caso mostraré como se crea el balanceador como demostración pra todas las intancias, y cual tiene que ser el resultado final y la cantidad de maquinas que tiene que estar disponibles despues del proceso.

##### Paso 1: Configuramos El Nombre De La Instancia y La AMI Que Vamos Ha Usar:
En esta practica utilizaremos instancias que tengan un S.O o AMI (en este cado de Amazón, aunque si quisieramos hacerlo en un entorno de prueba como vagrant o virtual box serian ISOs o Imagenes de Sistemas Operativos) de **Ubutu Server Versión 24.04 LTS**:
![Captura de pantalla 2024-11-28 133114](https://github.com/user-attachments/assets/adbcd779-e5be-4f8d-980d-a3fc3b4db2f6)

##### Paso 2: Definir el tipo de Instancia y crear las Claves de SSH:
En este caso como la primera instancia que crearemos será el balanceador de carga, crearemos una instancia de tipo **t2:small**, la cual dispondrá de un núcleo de procesamiento lógico y 2 GB de Memoria RAM, a parte crearemos un archivo .pem para poder conectarnos via SSH desde nuestro equipo local:
![Captura de pantalla 2024-11-28 133123](https://github.com/user-attachments/assets/0ffb720a-303a-428f-a139-a975cd589c5e)

##### Paso 3: Configuración de Red:
Ahora a la instancia creada le asignaremos la red VPC que hemos creado antes para su correcto funcionamiento, en este caso dado a que la instancia en cuestión es la que utilizaremos como balanceador de carga, la asociaremos a una subred pública para acceder a ella posteriormente via SSH desde nuestro equipo local:
![Captura de pantalla 2024-11-28 133138](https://github.com/user-attachments/assets/81c49ef7-cd3c-4150-88e6-2eb9206a653b)

##### Paso 4: Creación de Grupo de Seguridad para la Instancia:
Dado a que la instancia que estamos creando, va a situarse en una subred pública, dentro de las directrices destacaremos la regla de SSH desde cualquier dirección, HTTP desde cualquier dirección y HTTPS desde cualquier dirección:
![Captura de pantalla 2024-11-28 133233](https://github.com/user-attachments/assets/550f1a63-ba3b-445a-b05e-79fdbc41533d)
![Captura de pantalla 2024-11-28 133244](https://github.com/user-attachments/assets/622c34d7-6d80-4546-bd5c-bed8d6235cc8)














