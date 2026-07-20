# Implementación de un laboratorio de ciberseguridad defensiva para una pequeña empresa

## Descripción

Este proyecto consiste en el diseño e implementación de un laboratorio que simula la infraestructura de una pequeña empresa sin medidas de seguridad previamente establecidas. El objetivo es identificar los principales riesgos de la organización e implementar una arquitectura defensiva capaz de proteger la red, detectar amenazas y centralizar la monitorización de eventos de seguridad.

La infraestructura propuesta incorpora un firewall perimetral, segmentación de red, un sistema IDS/IPS y una plataforma SIEM, permitiendo mejorar la visibilidad del tráfico, limitar el movimiento lateral entre redes y detectar posibles ataques en tiempo real.

## Objetivos

* Diseñar una arquitectura de red segura para una pequeña empresa.
* Implementar un firewall perimetral con **pfSense**.
* Segmentar la red en diferentes VLAN según el nivel de confianza.
* Desplegar un sistema **IDS/IPS** mediante **Suricata**.
* Centralizar la monitorización y gestión de eventos utilizando **Wazuh**.
* Validar las medidas de seguridad mediante simulaciones de ataque desde una máquina atacante.

## Tecnologías utilizadas

* VirtualBox
* pfSense (Firewall)
* Suricata (IDS/IPS)
* Wazuh (SIEM)
* Máquinas virtuales Linux y Windows
* Redes virtuales y segmentación mediante VLAN

## Arquitectura del laboratorio

El laboratorio está compuesto por cinco máquinas virtuales:

* **Firewall (pfSense + Suricata):** controla el tráfico entre la red interna y la externa y realiza funciones de filtrado e inspección.
* **Servidor Wazuh:** centraliza los registros y genera alertas de seguridad.
* **Cliente 1:** ubicado en la red de administración.
* **Cliente 2:** ubicado en la red de empleados.
* **Máquina atacante:** utilizada para realizar pruebas desde redes internas y externas.

La red interna se divide en tres segmentos:

* **Red de administración:** destinada a servidores y equipos críticos, con mayores restricciones de acceso.
* **Red de empleados:** utilizada por los equipos de trabajo habituales.
* **Red de invitados:** diseñada para accesos temporales con permisos limitados y aislamiento del resto de la infraestructura.

Este laboratorio reproduce un escenario realista en el que se implementan medidas de seguridad sobre la infraestructura de una empresa y permite, mediante la realización de ataques simulados, evaluar su eficacia frente a ciberataques reales.

## Implementación de los sistemas de seguridad

Para iniciar la implementación de la infraestructura defensiva, se procedió a la creación de una máquina virtual configurada con dos interfaces de red. La primera de ellas, establecida en modo adaptador puente, actúa como interfaz WAN para simular la conexión con la red externa, mientras que la segunda se configuró como red interna para dar soporte a la interfaz LAN donde se interconectarán el resto de equipos del laboratorio. Sobre esta base, se realizó la instalación y configuración de pfSense, estableciéndolo como el firewall perimetral encargado de gestionar el filtrado y el control del tráfico entre ambos segmentos de red.<br>
<img width="544" height="268" alt="image" src="https://github.com/user-attachments/assets/9ae96e36-953e-4479-b9a1-f9917f2cbf7e" /><br>

Una vez finalizada la instalación y configuración inicial de pfSense, el sistema dispone de direcciones IP específicas para las interfaces WAN y LAN. Para proceder con la configuración avanzada del firewall, la segmentación de red y el despliegue del sistema IDS/IPS (Suricata), es necesario acceder a la interfaz web de administración a través de la dirección IP de la LAN. Este acceso debe realizarse desde un equipo ubicado dentro de la misma red interna para gestionar de forma segura los diferentes segmentos de la infraestructura.<br>
<img width="594" height="368" alt="image" src="https://github.com/user-attachments/assets/a3dd3c08-0cfa-46d1-8fab-90b27cd80582" /><br>

Con el objetivo de reforzar la seguridad perimetral, se ha implementado una regla explícita para denegar todo el tráfico proveniente de la red externa hacia la red interna. Aunque el firewall pfSense bloquea por defecto cualquier conexión que no esté permitida por una regla previa, la creación de esta política de denegación garantiza que ningún flujo de datos no autorizado pueda cruzar desde la WAN hacia los segmentos protegidos de la infraestructura, Esta medida actúa como una capa de seguridad adicional para blindar la red de administración, la de empleados y la de invitados frente a posibles amenazas externas.<br>
<img width="599" height="431" alt="image" src="https://github.com/user-attachments/assets/97b524bc-68a1-4ee3-bcad-b825d55764dc" /><br>

Para facilitar la administración y asegurar la conectividad inicial, se mantienen de forma provisional las reglas que pfSense aplica por defecto en la interfaz LAN. Estas políticas permiten tanto el acceso a la gestión del firewall desde la red interna como la salida de tráfico hacia el exterior (WAN) y la comunicación entre dispositivos. No obstante, esta configuración se ajustará durante la fase de segmentación de la red; en ese punto, se implementarán reglas de filtrado más estrictas para cada segmento (Administración, Empleados e Invitados) con el objetivo de limitar el tráfico no esencial y prevenir el movimiento lateral de posibles amenazas.<br>
<img width="592" height="127" alt="image" src="https://github.com/user-attachments/assets/d66ad7a5-39cf-40c7-87f6-8b69984282eb" /><br>

El siguiente paso en el despliegue de la infraestructura es la segmentación de la red interna para limitar el movimiento lateral y mejorar la seguridad global del sistema. Para ello, se procede a la creación de diversas VLANs vinculadas a la interfaz LAN principal, definiendo segmentos específicos para Administración, Empleados e Invitados.
La configuración se realiza a través del apartado de VLANs dentro del menú de interfaces de pfSense. Como acción inicial, se ha definido la VLAN con el tag 10 para identificar el segmento de Administración, el cual está destinado a albergar los equipos críticos y servidores con mayores restricciones de acceso. Este proceso permite estructurar la red según el nivel de confianza de cada grupo, facilitando la aplicación de políticas de filtrado personalizadas en fases posteriores.<br>
<img width="595" height="190" alt="image" src="https://github.com/user-attachments/assets/81011405-3f78-4e9a-838e-3e0c537f7f36" /><br>

Asimismo, se han habilitado las VLAN 20 para el segmento de Empleados y la VLAN 30 para la red de Invitados.<br>
<img width="599" height="159" alt="image" src="https://github.com/user-attachments/assets/24d1438c-462b-4881-a17c-3b653bdabef6" /><br>
(NOTA: Debido a que no se dispone actualmente de un switch físico para gestionar las VLAN, la segmentación se ha implementado mediante la creación de tres interfaces de red independientes que simulan las VLANs de Administración, Empleados e Invitados. En pfSense, estas interfaces se han activado con la misma nomenclatura, asegurando que la gestión, el comportamiento del tráfico y las políticas de seguridad sean idénticos a los de una arquitectura de red segmentada convencional.)<br>

Para automatizar la gestión de red en la infraestructura segmentada, se ha procedido a habilitar el servicio DHCP en pfSense para cada segmento definido: Administración, Empleados e Invitados. En el segmento de Administración, destinado a equipos críticos, se ha establecido un rango de direcciones entre 192.168.10.10 y 192.168.10.100, mientras que para Empleados e Invitados se han configurado los rangos 192.168.20.10-100 y 192.168.30.10-100, respectivamente. La configuración se completa asignando la IP de pfSense de cada interfaz como gateway y DNS primario, junto con el DNS de Google como secundario, garantizando así el control del tráfico y la correcta resolución de nombres en cada nivel de confianza de la red.<br>
<img width="600" height="638" alt="image" src="https://github.com/user-attachments/assets/eeba998a-2a0b-4fc1-a22c-02d6fcd2c5fa" /><br>

Tras eliminar las políticas por defecto de pfSense para aplicar un control de tráfico más granular y adaptado al laboratorio, se ha procedido a configurar las reglas de firewall para el segmento de Administración,. Dado que este segmento alberga los equipos críticos de la infraestructura, se le ha otorgado una visibilidad completa sobre el resto de la red.
Para ello, se han implementado tres reglas que permiten el acceso desde Administración hacia cualquier destino, incluyendo la WAN, la propia interfaz de gestión de pfSense y el tráfico interno del segmento,. Aunque se ha habilitado una regla general de acceso total, se han añadido dos reglas específicas y redundantes para permitir el tráfico hacia las VLAN de Empleados e Invitados,. Esta configuración tiene como objetivo mejorar la claridad en la monitorización de eventos y asegurar que el personal administrativo pueda gestionar y supervisar todos los niveles de confianza de la infraestructura de forma efectiva.<br>
<img width="595" height="123" alt="image" src="https://github.com/user-attachments/assets/7ef757de-b16f-46b9-9188-d0fd3bbf3ca0" /><br>

En el segmento de empleados, se han establecido políticas que deniegan explícitamente el acceso a la red de administración y a la interfaz de gestión de pfSense para evitar movimientos laterales hacia activos críticos. No obstante, se permite la comunicación dentro de su propia red, el acceso al segmento de invitados y la salida hacia la WAN, garantizando así la operatividad necesaria bajo un entorno controlado.<br>
<img width="592" height="143" alt="image" src="https://github.com/user-attachments/assets/8b1f8e3b-8751-46b5-ae89-6492cc2c8d0c" /><br>

Para el segmento de invitados, se han configurado políticas de seguridad estrictas destinadas a garantizar su total aislamiento del resto de la infraestructura. Se han establecido reglas de bloqueo para impedir el acceso a las redes de administración y empleados, además de restringir la conexión con la interfaz de gestión de pfSense. Finalmente, se ha habilitado una regla de acceso general que permite exclusivamente la navegación hacia la WAN y la comunicación interna entre dispositivos del mismo segmento.<br>
<img width="580" height="138" alt="image" src="https://github.com/user-attachments/assets/1a695ab3-a760-4df4-8358-f2b20645d073" /><br>

Se ha bloqueado todo el tráfico entrante desde la WAN hacia la red interna a través de pfSense. Esta política impide conexiones externas no autorizadas, garantizando la seguridad de los segmentos de administración, empleados e invitados.<br>
<img width="599" height="149" alt="image" src="https://github.com/user-attachments/assets/7f5a57db-5e4a-42b4-9cbc-c131008a29f3" /><br>

Se confirma que un equipo en la red de administración dispone de acceso completo tanto a los segmentos de empleados e invitados como a la interfaz de gestión de pfSense y la red externa. Esta conectividad total valida la jerarquía de seguridad establecida, permitiendo que los equipos críticos mantengan visibilidad y control sobre todos los niveles de confianza de la infraestructura.<br>
<img width="599" height="657" alt="image" src="https://github.com/user-attachments/assets/97973e76-fff0-4ad7-9528-89f67662a49c" /><br>

Se valida que un equipo en la red de empleados no tiene acceso al segmento de administración ni a la interfaz de pfSense, garantizando el aislamiento de los activos críticos y evitando el movimiento lateral. Simultáneamente, se confirma su conectividad con la red de invitados y la salida a la red externa, lo que verifica la correcta implementación de las reglas de filtrado y la segmentación de la infraestructura.<br>
<img width="586" height="617" alt="image" src="https://github.com/user-attachments/assets/bdae5313-1e8c-4af0-acda-e05a6b685260" /><br>

Se comprueba que un equipo en el segmento de invitados carece de acceso a las redes de administración y empleados, así como a la interfaz de gestión de pfSense, garantizando el aislamiento total de esta zona. No obstante, se valida su capacidad de conexión con la red externa o WAN, lo que confirma que las reglas de firewall aplicadas aseguran la navegación de usuarios temporales sin comprometer la seguridad de los activos internos críticos del laboratorio.<br>
<img width="530" height="540" alt="image" src="https://github.com/user-attachments/assets/5329db91-9c12-4bfc-b477-042eab5488a0" /><br>

























