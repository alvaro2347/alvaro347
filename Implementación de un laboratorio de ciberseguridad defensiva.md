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

Para iniciar la implementación de la infraestructura defensiva, se procedió a la creación de una máquina virtual configurada con dos interfaces de red. La primera de ellas, establecida en modo adaptador puente, actúa como interfaz WAN para simular la conexión con la red externa, mientras que la segunda se configuró como red interna para dar soporte a la interfaz LAN donde se interconectarán el resto de equipos del laboratorio. Sobre esta base, se realizó la instalación y configuración de pfSense, estableciéndolo como el firewall perimetral encargado de gestionar el filtrado y el control del tráfico entre ambos segmentos de red<br>
<img width="590" height="369" alt="image" src="https://github.com/user-attachments/assets/e19bad38-ba25-4135-8c8a-7b6f12f07d62" /><br>
Una vez finalizada la instalación y configuración inicial de pfSense, el sistema dispone de direcciones IP específicas para las interfaces WAN y LAN. Para proceder con la configuración avanzada del firewall, la segmentación de red y el despliegue del sistema IDS/IPS (Suricata), es necesario acceder a la interfaz web de administración a través de la dirección IP de la LAN. Este acceso debe realizarse desde un equipo ubicado dentro de la misma red interna para gestionar de forma segura los diferentes segmentos de la infraestructura.<br>
<img width="594" height="368" alt="image" src="https://github.com/user-attachments/assets/a3dd3c08-0cfa-46d1-8fab-90b27cd80582" /><br>
Con el objetivo de reforzar la seguridad perimetral, se ha implementado una regla explícita para denegar todo el tráfico proveniente de la red externa hacia la red interna. Aunque el firewall pfSense bloquea por defecto cualquier conexión que no esté permitida por una regla previa, la creación de esta política de denegación garantiza que ningún flujo de datos no autorizado pueda cruzar desde la WAN hacia los segmentos protegidos de la infraestructura, Esta medida actúa como una capa de seguridad adicional para blindar la red de administración, la de empleados y la de invitados frente a posibles amenazas externas.<br>

<img width="599" height="431" alt="image" src="https://github.com/user-attachments/assets/97b524bc-68a1-4ee3-bcad-b825d55764dc" /><br>
Para facilitar la administración y asegurar la conectividad inicial, se mantienen de forma provisional las reglas que pfSense aplica por defecto en la interfaz LAN. Estas políticas permiten tanto el acceso a la gestión del firewall desde la red interna como la salida de tráfico hacia el exterior (WAN) y la comunicación entre dispositivos. No obstante, esta configuración se ajustará durante la fase de segmentación de la red; en ese punto, se implementarán reglas de filtrado más estrictas para cada segmento (Administración, Empleados e Invitados) con el objetivo de limitar el tráfico no esencial y prevenir el movimiento lateral de posibles amenazas.<br>
<img width="592" height="127" alt="image" src="https://github.com/user-attachments/assets/d66ad7a5-39cf-40c7-87f6-8b69984282eb" /><br>






