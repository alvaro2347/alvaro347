# Puertos 139 y 445

Ambos tienen un servicio de SMB<br><img width="781" height="334" alt="image" src="https://github.com/user-attachments/assets/e33dfe4d-6ca3-477f-8330-d20d65fa91bf" />

Utilizo la herramienta enum4linux sobre el target para enumerar posibles recursos compartidos de SMB
<img width="905" height="221" alt="image" src="https://github.com/user-attachments/assets/579f114a-16f4-46d8-9a7f-8711f0ec6580" /><br>
La herramienta encuentra estos shares de SMB
<img width="871" height="513" alt="image" src="https://github.com/user-attachments/assets/c59b16d6-bdf6-4a0b-a56d-b3992ab0f9ff" />

Con smbclient consigo conectarme al share “tmp” y listar su contenido<br><img width="592" height="230" alt="image" src="https://github.com/user-attachments/assets/a4426fe9-1561-4444-8816-ee5feb9a5a2b" />
