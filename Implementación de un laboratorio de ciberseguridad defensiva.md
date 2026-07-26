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

Una vez finalizada la segmentación y configuración del firewall, se procede a desplegar el sistema IDS/IPS Suricata para dotar a la red de capacidades de detección de amenazas en tiempo real. La instalación se realiza directamente sobre el nodo de pfSense a través de su gestor de paquetes (Package Manager), consolidando así el control del tráfico y la inspección profunda en un único punto central de la infraestructura defensiva.<br>
<img width="592" height="307" alt="image" src="https://github.com/user-attachments/assets/d40c2de5-3e7f-4534-a457-de6d9dc9b207" /><br>

Se ha configurado Suricata en la interfaz WAN para iniciar la inspección del tráfico externo, habilitando específicamente el registro de tráfico HTTP para obtener una mayor visibilidad sobre la actividad web.
En esta fase inicial, se ha mantenido desactivada la función de bloqueo automático de hosts, permitiendo que el sistema funcione exclusivamente como un IDS centrado en la detección de posibles amenazas. Esta configuración permite monitorizar y validar las alertas generadas antes de realizar la transición al modo IPS, punto en el cual el sistema podrá mitigar ataques de forma activa bloqueando el tráfico malicioso.<br>
<img width="592" height="620" alt="image" src="https://github.com/user-attachments/assets/a7b2d15d-769b-4cfc-8762-922a3e710f60" /><br>

Se ha activado Suricata en todas las interfaces (WAN, administración, empleados e invitados) para monitorizar todo el tráfico del laboratorio. El próximo paso será definir las alertas personalizadas para cada segmento de red.<br>
<img width="590" height="167" alt="image" src="https://github.com/user-attachments/assets/fc1b781c-f81b-4d4f-b242-1879d1842587" /><br>


Se han definido las primeras alertas en la interfaz WAN de Suricata, orientadas a identificar actividades sospechosas dirigidas tanto al firewall pfSense como a la infraestructura interna, cumpliendo con el objetivo de detectar amenazas en tiempo real.
Estas reglas permiten una monitorización detallada mediante los siguientes criterios:<br>
Protección del Firewall: Se han implementado alertas para detectar tráfico ICMP (ping) y accesos a la interfaz web de pfSense, lo cual es fundamental ya que es el único nodo expuesto directamente a la red externa.<br>
Detección de Reconocimiento: Mediante el uso de umbrales específicos (parámetro de 5 conexiones en 10 segundos), el sistema es capaz de identificar intentos de escaneo de puertos realizados con herramientas como nmap, alertando sobre fases de reconocimiento de posibles atacantes.<br>
Visibilidad de la Red Interna: A través de la variable $HOME_NET, se ha extendido la vigilancia para detectar pings o múltiples intentos de conexión hacia cualquiera de los segmentos internos (administración, empleados e invitados).<br>
Con esta configuración, el laboratorio cuenta ahora con la capacidad de registrar cualquier interacción no autorizada desde la WAN, proporcionando la visibilidad necesaria antes de realizar la transición al bloqueo activo de tráfico malicioso.<br>
<img width="596" height="403" alt="image" src="https://github.com/user-attachments/assets/025f1d22-0ab3-4f67-aed4-9f4836c876c7" /><br>


Se han configurado alertas en el segmento de empleados para detectar pings, accesos a la interfaz web de pfSense o ráfagas de más de cinco intentos de conexión hacia la red de administración. Estas reglas en Suricata permiten identificar movimientos laterales y tareas de reconocimiento hacia los activos críticos del laboratorio.<br>
<img width="594" height="406" alt="image" src="https://github.com/user-attachments/assets/156e202b-fd00-4526-9e6e-ce37459e0131" /><br>

Para la red de invitados, se han establecido alertas en Suricata que detectan pings o ráfagas de más de cinco intentos de conexión hacia los segmentos de administración y empleados, así como hacia el propio pfSense. Al igual que en las otras redes, se monitoriza específicamente cualquier intento de acceso a la interfaz web del firewall para garantizar el aislamiento total de esta zona de bajo nivel de confianza. Estas reglas permiten registrar comportamientos anómalos o intentos de reconocimiento interno, cumpliendo con el objetivo de detección de amenazas en tiempo real del laboratorio.<br>
<img width="598" height="404" alt="image" src="https://github.com/user-attachments/assets/6716ff78-3e0f-4082-9378-790db1b7d30e" /><br>
En el segmento de administración, no se han definido alertas para el tráfico saliente debido a su condición de zona de confianza con acceso total a la infraestructura. Al estar autorizada para interactuar con las redes de empleados, invitados y la gestión de pfSense, sus comunicaciones se consideran legítimas según la jerarquía de seguridad y el control de tráfico establecidos en el laboratorio.<br><br>

Se ha procedido a elevar las capacidades de la infraestructura defensiva mediante la transición de Suricata de un modo puramente IDS a uno IPS (Sistema de Prevención de Intrusiones). Para ello, se ha habilitado la opción "Block offenders" en todas las interfaces, a excepción del segmento de administración, garantizando así la protección activa y la detección de amenazas en tiempo real.
La elección del modo "legacy" y el bloqueo tanto de la IP de origen como de destino refuerza la estrategia de limitar el movimiento lateral entre redes. Esta configuración asegura que, ante una alerta, la comunicación se corte por completo, impidiendo que un posible atacante avance incluso si lograra acceder a un equipo de destino.
Para evitar interrupciones accidentales en la gestión de la infraestructura, se ha definido una pass list que incluye exclusivamente a la red de administración, el segmento destinado a los equipos críticos y servidores. Con este ajuste, el firewall (pfSense + Suricata) no solo monitoriza, sino que controla y mitiga activamente el tráfico malicioso entre la red interna y la externa.<br>
<img width="594" height="347" alt="image" src="https://github.com/user-attachments/assets/9f31b6e5-318c-4c77-a702-e0feb4141128" /><br>

Se ha integrado el servidor Wazuh en un entorno Ubuntu dentro del segmento de administración, cumpliendo con el objetivo de centralizar la monitorización y gestión de eventos de seguridad del laboratorio. Al ubicar el servidor en esta red, destinada a equipos críticos, se facilita la supervisión de la infraestructura.
La instalación del agente en la máquina Windows de administración permite que el sistema SIEM comience a recolectar registros específicos de ese nodo. El uso de una IP fija asignada desde pfSense es una medida técnica adecuada, ya que garantiza que el flujo de datos desde los agentes hacia el servidor no se interrumpa, permitiendo una detección de amenazas constante y una identificación clara de cada dispositivo en la consola de gestión.<br>
<img width="570" height="408" alt="image" src="https://github.com/user-attachments/assets/4212c74e-054c-4d02-8884-36b1015e0460" /><br>

Se ha activado el agente de Wazuh en el cliente Windows de la red de administración, permitiendo la monitorización centralizada de este equipo crítico. Con esto, el SIEM ya recibe telemetría en tiempo real para detectar amenazas en el segmento más restringido de la infraestructura.<br>
<img width="596" height="237" alt="image" src="https://github.com/user-attachments/assets/27201fd2-c84a-4294-bb5a-12f656b5864d" /><br>

Tras instalar el agente en el cliente ubicado en la red de empleados, esta red se integra en el sistema de monitorización centralizada de Wazuh. Una vez establecida la conexión, el SIEM permitirá supervisar la actividad y detectar amenazas en este segmento de usuarios habituales, reforzando la visibilidad global de la infraestructura.<br>
<img width="604" height="276" alt="image" src="https://github.com/user-attachments/assets/c68aa12f-3854-40fc-a73c-f97b9c45666a" /><br>

Las simulaciones de ataque desde la red externa validan el éxito de la arquitectura defensiva:<br>
Bloqueo Perimetral: La política de denegación total en pfSense impide pings y escaneos, haciendo que la red interna sea invisible desde la WAN.<br>
Prevención Activa: Cualquier intento de conexión sospechosa es detectado por Suricata (IPS), el cual bloquearía automáticamente la IP atacante al estar en modo "Block offenders".<br>
Protección de Activos: Los equipos críticos y el servidor Wazuh permanecen aislados y seguros, confirmando la eficacia de la segmentación implementada.<br>
<img width="593" height="546" alt="image" src="https://github.com/user-attachments/assets/b727c01a-ec9b-4877-babc-6254fb31ae5e" /><br>

La visualización de los registros en Suricata confirma la detección de amenazas en tiempo real, validando las alertas de red configuradas. Al estar activo el modo IPS, cada registro indica que el sistema ha bloqueado automáticamente las IPs atacantes, protegiendo con éxito los segmentos de administración, empleados e invitados.<br>
<img width="602" height="351" alt="image" src="https://github.com/user-attachments/assets/38c99e36-db42-45c2-8f9f-579a0674ebda" /><br>

Las pruebas en la red de invitados confirman el éxito del aislamiento: pfSense bloquea el movimiento lateral hacia administración y empleados, además de proteger su propia gestión contra escaneos. Al detectarse estas acciones, Suricata (IPS) mitiga la amenaza bloqueando automáticamente la IP del atacante, cumpliendo con los objetivos de seguridad del laboratorio.<br>
<img width="595" height="519" alt="image" src="https://github.com/user-attachments/assets/9971b82d-f6fc-447e-8f9a-5fcda106c61d" /><br>

La regla de cinco intentos en diez segundos identifica eficazmente patrones de escaneo sin saturar los registros, permitiendo una monitorización continua. Al operar en modo IPS, Suricata bloquea automáticamente la IP atacante, lo que neutraliza la amenaza de inmediato y previene el movimiento lateral hacia los segmentos de empleados o administración. Este proceso de seguridad se centraliza en Wazuh para su análisis, mientras que la lista de paso protege la operatividad de la red de administración, asegurando que los equipos críticos mantengan su conexión en todo momento.<br>
<img width="593" height="445" alt="image" src="https://github.com/user-attachments/assets/3b0b1424-6cd8-49a3-ad58-50499857f5a2" /><br>

Desde la plataforma Wazuh se centraliza la gestión de seguridad al detectar y categorizar las vulnerabilidades de los equipos en red según su nivel de criticidad. En este escenario, el SIEM identificó una vulnerabilidad crítica, 119 altas, 34 medias y una baja, proporcionando para cada una el identificador CVE, una descripción técnica y enlaces de investigación. Esta funcionalidad es clave para mejorar la visibilidad de la infraestructura y permitir la corrección proactiva de fallos, alineándose con los objetivos de protección y monitorización centralizada del laboratorio.<br>
<img width="598" height="485" alt="image" src="https://github.com/user-attachments/assets/db50379b-25b3-4161-a8dc-bc6e1f412a3f" /><br>

Es posible acceder a información detallada de la vulnerabilidad que afecta a la máquina, en la siguiente imagen es posible observar dicha información<br>
<img width="602" height="304" alt="image" src="https://github.com/user-attachments/assets/8070d524-4635-405c-a6a8-f845864e807c" /><br>

La monitorización de logs de eventos en Wazuh, como los inicios de sesión en Windows, es fundamental para cumplir el objetivo de centralizar la gestión de seguridad y detectar actividades sospechosas en tiempo real. Esta visibilidad permite supervisar los activos en las redes de administración y empleados, garantizando que el administrador tenga un control total sobre las acciones realizadas dentro de la infraestructura segmentada.<br>
<img width="609" height="426" alt="image" src="https://github.com/user-attachments/assets/d30f2719-07dd-4418-8ae4-77c6600f657b" /><br>

Esta capacidad de inspección profunda en los registros es lo que permite al servidor Wazuh cumplir su función de centralizar registros y generar alertas de seguridad con precisión. Al proporcionar datos específicos como el ID, la IP del equipo y el usuario involucrado, el sistema ofrece la trazabilidad necesaria para detectar amenazas en tiempo real y diferenciar actividades legítimas de posibles intrusiones.
Contar con este nivel de detalle es vital para proteger los activos de la red de administración, donde se encuentran los equipos críticos, asegurando que cualquier inicio de sesión inesperado pueda ser investigado y mitigado de inmediato para mantener la integridad de la infraestructura.<br>
<img width="606" height="764" alt="image" src="https://github.com/user-attachments/assets/feda13ea-aba9-4012-bddc-537485265a49" /><br>

Esta simulación confirma que Wazuh centraliza eficazmente registros críticos como conexiones SSH y escaladas de privilegios mediante sudo. Al alertar sobre un acceso root en el servidor de la red de administración, el sistema garantiza la visibilidad necesaria para detectar y responder de inmediato ante un compromiso total de la infraestructura defensiva.<br>
<img width="598" height="586" alt="image" src="https://github.com/user-attachments/assets/3b601a28-0e55-4748-9919-c40786b5310e" /><br>

Este hallazgo en los detalles del log confirma que el servidor Wazuh, ubicado en la red de administración destinada a equipos críticos, ha sufrido un compromiso de máxima gravedad. La capacidad del SIEM para registrar no solo la escalada de privilegios, sino el comando exacto de visualización de contraseñas, es fundamental para la detección de amenazas en tiempo real y para confirmar que el atacante ha obtenido control total sobre el sistema. Este nivel de visibilidad técnica valida el objetivo principal de centralizar la monitorización de eventos, permitiendo identificar y evaluar de forma precisa incidentes que comprometen la integridad de toda la infraestructura defensiva.<br>
<img width="600" height="284" alt="image" src="https://github.com/user-attachments/assets/bcf1a0ea-7889-42fe-99be-2264196e29d8" /><br>

<br>Las simulaciones realizadas confirman que la arquitectura defensiva diseñada ha transformado con éxito una infraestructura vulnerable en un entorno seguro, monitorizado y capaz de responder ante incidentes.
El éxito de este laboratorio se sustenta en tres capacidades críticas validadas por tus pruebas:<br>
Protección y Aislamiento: El firewall (pfSense) y la segmentación de red han demostrado ser eficaces al impedir el acceso no autorizado desde la WAN y restringir el movimiento lateral desde la red de invitados, protegiendo así los activos críticos en el segmento de administración.
Detección y Mitigación Activa: La integración de Suricata (IDS/IPS) permitió identificar patrones de ataque en tiempo real, como escaneos de puertos y pings, bloqueando automáticamente al atacante para neutralizar la amenaza antes de que progresara.
Visibilidad y Gestión Centralizada: El SIEM (Wazuh) cumplió su función de centralizar los registros, permitiendo no solo la detección de vulnerabilidades (CVE) para una remediación proactiva, sino también la monitorización detallada de eventos internos, como inicios de sesión y ejecuciones de comandos con privilegios de root (sudo).
En definitiva, las pruebas demuestran que la combinación de estas tecnologías permite pasar de una postura reactiva a una defensa proactiva, garantizando que cualquier acción sospechosa sea registrada y alertada para proteger la integridad de la pequeña empresa.
















