# Blue

Hago un escaneo con nmap a la máquina intentando detectar versiones de los servicios y ejecutando scripts por defecto asi como scripts para detectar vulnerabilidades, luego guardando el resultado en un archivo <br>
<img width="1079" height="1002" alt="image" src="https://github.com/user-attachments/assets/38c1d619-f960-4c07-8a01-9762ed58195f" />

El escaneo revela que la máquina es vulnerable a ms17-010 el cual corresponde a la conocida vulnerabilidad de smb eternalblue asique desde metasploit busco un módulo para explotar la vulnerabilidad, en este caso voy a utilizar el siguiente: "exploit/windows/smb/ms17_010_eternalblue" <br>
<img width="955" height="598" alt="image" src="https://github.com/user-attachments/assets/b8a51ce4-78e6-4ced-b0f0-042c6c173a97" />

Miro las opciones del exploit y veo que en este caso solo hace falta establecer la máquina objetivo y la atacante, asique la añado y además establezco un payload para que al ejecutar el exploit me devuelva una reverse shell<br>
<img width="727" height="645" alt="image" src="https://github.com/user-attachments/assets/8b8d4aee-999f-4e13-a4d8-19610831be3f" /><br>
Tras ejecutar el exploit ya está establecida la reverse shell<br>
<img width="1008" height="613" alt="image" src="https://github.com/user-attachments/assets/92dcfd2d-834e-4039-9c0a-d412690d2161" />

Busco el modulo de meterpreter para escalar privilegios, lo ejecuto y se abre una nueva shell como meterpreter<br>
<img width="872" height="618" alt="image" src="https://github.com/user-attachments/assets/7791a401-3f18-4822-a46c-89c341b24b3a" />

Abro la shell y compruebo que soy un usuario privilegiado de Windows <br>
<img width="522" height="188" alt="image" src="https://github.com/user-attachments/assets/c98dee0c-55a2-49db-b0f2-9ad6f032cc67" /><br>
Busco los procesos que estan ejecutandose en la máquina<br>
<img width="253" height="292" alt="image" src="https://github.com/user-attachments/assets/11602bc1-8987-4c0c-8db4-46c7dd3d9f50" /><br>
migro a un proceso que pertenezca al usuario nt authority\system para asegurar que el proceso tambien tenga privilegios, luego obtengo los hashes de las contraseñas de los usuarios de la máquina<br>
<img width="704" height="135" alt="image" src="https://github.com/user-attachments/assets/b2d7649e-2986-4fb7-a06c-1cb64cd621b9" /><br>

Guardo el hash del usuario John en un archivo y con la herramienta John the ripper obtengo la contraseña<br>
<img width="804" height="229" alt="image" src="https://github.com/user-attachments/assets/da502103-1f9d-470e-9483-143c07173025" />

Voy al directorio raiz y veo que ahí se ubica la primera flag<br>
<img width="697" height="436" alt="image" src="https://github.com/user-attachments/assets/6bcc4635-4a27-4314-bbf9-9857944b4118" />

La siguiente flag se ubica en el directorio donde se almacenan la contraseñas en Windows<br>
<img width="414" height="61" alt="image" src="https://github.com/user-attachments/assets/aa5e051d-2cba-487d-8d73-6a9e5cca898e" />

La ultima flag se encuentra en la carpeta de documentos del usuario Jon<br>
<img width="558" height="252" alt="image" src="https://github.com/user-attachments/assets/8d70a2a3-3047-420d-8a44-6947b68727f3" />
