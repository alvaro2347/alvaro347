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
<img width="547" height="272" alt="image" src="https://github.com/user-attachments/assets/497be5ab-35d3-409f-917a-15b4dde8896c" />
