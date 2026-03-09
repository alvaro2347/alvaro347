# Puerto 3306

En este caso hay un servicio Mysql en el puerto<br><img width="511" height="189" alt="image" src="https://github.com/user-attachments/assets/27f845b5-d0ba-4ede-9f1e-9420e80ec777" />

Desde metasploit utilizo el modulo de mysql_login para intentar descubrir si los usuarios que conocemos pueden conectarse a mysql<br>
<img width="352" height="227" alt="image" src="https://github.com/user-attachments/assets/77b3093e-7971-4caa-96a1-e7786667b1cc" />


Creo un fichero con los usuarios descubiertos anteriormente para probar la explotación con metasploit<br>
<img width="132" height="138" alt="image" src="https://github.com/user-attachments/assets/7b4dc618-709e-4e1f-b399-79104d140912" />

Realizo la explotación introduciendo el target, archivo de usuarios que hemos creado y el de contraseñas que va a ser Rockyou, el cual viene incluido en Kali linux, pero no es posible obtener ninguna información ya que Metasploit no logra realizar la fuerza bruta debido a que la versión de Mysql que usa el target es muy antigua y no es compatible con el exploit<br>
<img width="1246" height="489" alt="image" src="https://github.com/user-attachments/assets/14e5d13e-3132-4d35-8ac0-3802f451e2f3" />

