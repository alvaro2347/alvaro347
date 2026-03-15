# Simple CTF

Realizo un escaneo con nmap y veo que hay un FTP un servicio web y un SSH<br>
<img width="770" height="581" alt="Image" src="https://github.com/user-attachments/assets/b303cc72-9867-4faa-abe8-6723182fe34a" />

Me conecto al FTP como usuario anónimo y veo un archivo que dice que la contraseña del usuario es debil, pero no hay mas información que esa<br><img width="1324" height="683" alt="Image" src="https://github.com/user-attachments/assets/fd1eefcc-2542-4f5a-bd90-9d32ff93316a" />

Busco directorios ocultos y encuentro uno lamado simple
<img width="804" height="662" alt="Image" src="https://github.com/user-attachments/assets/c0647ac8-947d-45e6-bc67-500f5a0f92f3" />

Uso whatweb para ver que tecnologías utiliza la web y veo que usa CMS-made-simple[2.2.8]<br>
<img width="2335" height="68" alt="Image" src="https://github.com/user-attachments/assets/ede43947-5b7d-40f3-af2b-26aeb995fe94" />

Encuentro esta vulnerabilidad para esa versión del CMS, asique descargo el exploit correspondiente<br>
<img width="1643" height="286" alt="Image" src="https://github.com/user-attachments/assets/57cec972-724f-4e64-92f7-f9927433f7aa" />

Ejecuto el exploit y encuentra un usuario y una contraseña, aunque la contraseña no parece ser correcta<br>
<img width="456" height="79" alt="Image" src="https://github.com/user-attachments/assets/89cde357-ef0e-4841-bc19-3303d403903a" />

Utilizo hydra para realizar fuerza bruta sobre el SSH, utilizo el usuario encontrado anteriormente y la wordlist rockyou y encuentro la contraseña<br>
<img width="730" height="255" alt="Image" src="https://github.com/user-attachments/assets/1af21f27-268f-4ba3-9e80-1d76099790c4" />

Me conecto al SSH con las credenciales obtenidas y encuentro la primera flag<br>
<img width="744" height="419" alt="Image" src="https://github.com/user-attachments/assets/4057f0ad-bacf-4b55-b5a3-8ccdf753b502" />

Busco que comandos puedo ejecutar como administrador con el usuario mitch, en este caso puedo usar vim, asique ejecuto el siguiente comando y consigo escalar a root<br>
<img width="659" height="191" alt="Image" src="https://github.com/user-attachments/assets/c705ee8b-8167-44c1-8b87-6d378b4bd5fc" />

La flag de root está en el directorio del propio usuario root<br>
<img width="212" height="145" alt="Image" src="https://github.com/user-attachments/assets/62052e90-b630-4a96-84f8-50a47e91b0be" />
