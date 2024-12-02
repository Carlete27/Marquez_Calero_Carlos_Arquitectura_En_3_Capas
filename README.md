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
A continuación nos dispondremos a crear una serie de instancias con una AMI de Ubuntu-Server 24.04. Una de ellas será la encargada de balancear las solicitudes recibidas desde internet, situada en la primera de las tres capas de nuestro despliege, hacia los servidores bakend, situada en la segunda de las tres capas de nuestro despliege, las cuales se conectarán al servidor de MySQL, situado







