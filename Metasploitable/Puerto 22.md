# Puerto 22
Hay un servicio SSH en el puerto <br><img width="532" height="114" alt="image" src="https://github.com/user-attachments/assets/8041c583-8907-4f78-9e49-a07cbf7318ba" /><br>
Como con nmap no encuentro una vulnerabilidad en el puerto 22, utilizo la consola obtenida desde el puerto anterior para obtener los usuarios a traves del fichero /etc/passwd<br>
<img width="616" height="98" alt="image" src="https://github.com/user-attachments/assets/d9827992-67b8-44d2-ade2-d7bd92a857ac" />


Pruebo a acceder por SSH con esos usuarios, con root no lo logro, pero con msfadmin consigo acceder, adicionalmente he tenido que añadir la flag que se ve abajo ya que de lo contrario rechaza la conexión debido a que tiene una versión antigua de SSH
<img width="653" height="404" alt="image" src="https://github.com/user-attachments/assets/8810e525-2642-4efc-b4ea-d96d0e12fa7d" />

