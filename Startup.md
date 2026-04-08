# Startup

Realizo un escaneo con nmap sobre la máquina y descubro un FTP, un SSH y una web<br>
<img width="762" height="627" alt="image" src="https://github.com/user-attachments/assets/04c4a867-97a7-497a-b1a1-b4a5aa81f7b5" /><br>
Como en el resultado de nmap veo que el usuario anónimo en FTP está habilitado accedo, veo dos archivos, los cuales me deja descargar
<img width="597" height="482" alt="image" src="https://github.com/user-attachments/assets/42a66dca-e196-47d0-bc7e-796ee817fcb3" /><br>
uno de los archivos contiene un texto poco relevante pero que contiene un nombre, el cual podria ser un nombre de usuario, el otro archivo es una imagen relacionada con el texto, pero no voy a realizar esteganografia ya que no parece relevante<br>
<img width="1256" height="75" alt="image" src="https://github.com/user-attachments/assets/c33c444e-bb39-4502-8e09-ec4bb86ce8d9" /><br>
Busco posibles directorios ocultos en la página web con dirb, solo encuentro la misma dirección donde se ubicaba el usuario anónimo al hacer login por FTP<br>
<img width="545" height="459" alt="image" src="https://github.com/user-attachments/assets/4019f10d-6f4a-4828-bb04-1f934bd1e66e" /><br>
como veo que se puede acceder por web, subo a la carpeta FTP una shell reversa para ejecutarla desde la web<br>
<img width="378" height="358" alt="image" src="https://github.com/user-attachments/assets/76dd2eda-eb72-46a6-83a4-264f60adbf71" /><br>
Tras ejecutar la shell reversa obtengo la shell en mi máquina<br>
<img width="716" height="500" alt="image" src="https://github.com/user-attachments/assets/ffd60d43-28c8-455e-937b-6781cc4702da" /><br>
Tras buscar posibles archivos importantes en el equipo, en la carpeta incidents encuentro un archivo pcapng, asique lo envio a mi máquina para analizarlo<br>
<img width="660" height="78" alt="image" src="https://github.com/user-attachments/assets/e08b8209-f677-490d-988c-5843fdf9a8fa" /><br>
Abro el archivo con Wireshark y sobre una conexión que parece importante realizo un follow TCP stream, tras buscar un poco encuentro que se han intentado listar permisos de sudo con la contraseña que aparece en la imagen, asique apunto esa contraseña<br>
<img width="1250" height="757" alt="image" src="https://github.com/user-attachments/assets/653952f0-20c5-47d0-ba78-6d02aabb3c15" /><br>

Pruebo a iniciar sesión como lennie con la contraseña descubierta anteriormente y consigo acceder<br>
<img width="327" height="137" alt="image" src="https://github.com/user-attachments/assets/2bbfe724-89f2-4450-9c1f-a2686416757e" /><br>

Encuentro un archivo con la receta que se solicitaba, la cual es "love"<br>
<img width="1094" height="172" alt="image" src="https://github.com/user-attachments/assets/11051222-949d-4db0-9ff5-e799e14656ae" /><br>

Voy a la carpeta de lennie y veo la flag de usuario<br>
<img width="305" height="115" alt="image" src="https://github.com/user-attachments/assets/eb5afdf6-4ad2-490e-8599-627b6c4da2ee" /><br>
Veo que en la carpeta scripts dentro del directorio de lennie hay un script, el cual ejecuta otro script ubicado en /etc , además exporta la variable $LIST al archivo startup_list.txt <br>
<img width="473" height="137" alt="image" src="https://github.com/user-attachments/assets/1a03815d-8257-4ba8-811a-5512ad101a1f" /><br>
Haciendo ls -la , veo que el archivo startup_list.txt se actualiza cada minuto, asique el script que lo modifica debe de estar ejecutandose de manera automática probablemente con permisos elevados, por lo que modifico el script de /etc para que ejecute una reverse shell, de esta manera cuando se ejecute el script ubicado en /home/lennie/scripts ejecutará también este y obtendré la shell <br>
<img width="436" height="96" alt="image" src="https://github.com/user-attachments/assets/711003be-79d1-4921-b92e-38c59a366e6d" /><br>

pongo mi máquina a la escucha con netcat y al ejecutarse el script, recibo una shell como root, ya que efectivamente este script se ejecuta con privilegios de root, en el directorio de root encuentro la flag de root<br>
<img width="637" height="302" alt="image" src="https://github.com/user-attachments/assets/3dfbee03-a47b-4d73-bd0e-f7c954419ed2" />
