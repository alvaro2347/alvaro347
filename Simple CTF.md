# Simple CTF

Se realiza un escaneo con nmap, descubriendo así que hay servicios FTP, web y SSH expuestos en la máquina<br>
<img width="770" height="581" alt="Image" src="https://github.com/user-attachments/assets/b303cc72-9867-4faa-abe8-6723182fe34a" />

Se realiza una conexión al FTP como usuario anónimo y se encuentra un archivo que dice que la contraseña del usuario es debil, pero no hay mas información que esa, por lo que se deja el FTP, al menos de momento, para pasar a relizar la explotación por otros medios<br><img width="1324" height="683" alt="Image" src="https://github.com/user-attachments/assets/fd1eefcc-2542-4f5a-bd90-9d32ff93316a" />

Se buscan directorios ocultos y se encuentra uno llamado simple
<img width="804" height="662" alt="Image" src="https://github.com/user-attachments/assets/c0647ac8-947d-45e6-bc67-500f5a0f92f3" />

Se utiliza la herramienta whatweb para ver que tecnologías utiliza la web descubriendo así que utiliza CMS-made-simple[2.2.8]<br>
<img width="2335" height="68" alt="Image" src="https://github.com/user-attachments/assets/ede43947-5b7d-40f3-af2b-26aeb995fe94" />

Se encuentra esta vulnerabilidad para esa versión del CMS, asique se descarga el exploit correspondiente<br>
<img width="1643" height="286" alt="Image" src="https://github.com/user-attachments/assets/57cec972-724f-4e64-92f7-f9927433f7aa" />

Se ejecuta el exploit encontrando así un usuario y una contraseña, aunque la contraseña no parece ser correcta<br>
<img width="456" height="79" alt="Image" src="https://github.com/user-attachments/assets/89cde357-ef0e-4841-bc19-3303d403903a" />

Se utiliza hydra para realizar fuerza bruta sobre el SSH, aprovechando el usuario encontrado anteriormente y la wordlist rockyou, con esto se descubre la contraseña correspondiente al usuario<br>
<img width="730" height="255" alt="Image" src="https://github.com/user-attachments/assets/1af21f27-268f-4ba3-9e80-1d76099790c4" />

Se realiza una conexión al SSH con las credenciales obtenidas descubriendo así la primera flag<br>
<img width="744" height="419" alt="Image" src="https://github.com/user-attachments/assets/4057f0ad-bacf-4b55-b5a3-8ccdf753b502" />

Tras investigar que comandos se pueden ejecutar como administrador con el usuario mitch, se descubre que se puede usar vim, asique aprovechando esto, se ejecuta el siguiente comando consiguiendo así escalar a root<br>
<img width="659" height="191" alt="Image" src="https://github.com/user-attachments/assets/c705ee8b-8167-44c1-8b87-6d378b4bd5fc" />

Finalmente, como usuario root, se descubre que la flag de root está en el directorio del propio usuario root<br>
<img width="212" height="145" alt="Image" src="https://github.com/user-attachments/assets/62052e90-b630-4a96-84f8-50a47e91b0be" />
