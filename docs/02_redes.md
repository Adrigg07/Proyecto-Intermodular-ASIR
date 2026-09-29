# Redes y Conectividad

## 2. Arquitectura de Red y Topología

Para garantizar el correcto funcionamiento de **Vibe & Feast**, la infraestructura de red debe soportar tanto la operativa administrativa diaria de la oficina central como los despliegues de red temporal o segmentada necesarios para la celebración de grandes eventos (conciertos, bodas y festivales de catering). 

### 2.1. Diseño Lógico y Segmentación (VLANs)
Con el fin de aislar el tráfico sensible, mejorar el rendimiento y aplicar políticas de seguridad estrictas, la red se divide en diferentes **VLANs (Virtual Local Area Networks)**:

- **VLAN 10 - Administración y Gestión (Datos):** Reservada para los equipos de la oficina central, sistemas de facturación, bases de datos de clientes y gestión interna de reservas.
- **VLAN 20 - Logística y Cocina:** Utilizada por los coordinadores de eventos y personal de almacén/catering para la comunicación en tiempo real y la actualización de agendas y stocks.
- **VLAN 30 - Invitados / Redes Públicas (Wi-Fi):** Zona aislada destinada a los asistentes a bodas, cumpleaños o conciertos para proporcionar acceso a Internet sin comprometer la red corporativa.
- **VLAN 40 - Servidores (DMZ / Red Interna):** Aloja los servidores locales de la empresa (servidor web, base de datos, sistema de reservas y copias de seguridad).

### 2.2. Esquema de Direccionamiento IP (IPv4)
Se ha diseñado un plan de direccionamiento estructurado utilizando subredes privadas (RFC 1918) para facilitar la gestión y el enrutamiento:

| VLAN | Nombre | Subred Asignada | Uso Principal |
| :--- | :--- | :--- | :--- |
| **VLAN 10** | Admin | `192.168.10.0/24` | Puestos de oficina y administración |
| **VLAN 20** | Logística | `192.168.20.0/24` | Dispositivos móviles y portátiles de campo |
| **VLAN 30** | Invitados | `10.0.30.0/24` | Red Wi-Fi para asistentes a eventos |
| **VLAN 40** | Servidores | `192.168.40.0/24` | Servidores corporativos y servicios internos |

### 2.3. Enrutamiento y Seguridad Perimetral
- **Router-on-a-Stick / Gateway:** Se emplea un enrutador central para permitir la comunicación controlada entre las diferentes VLANs mediante subinterfaces troncales conectadas al switch principal.
- **Listas de Control de Acceso (ACLs):** Se implementan reglas de filtrado para impedir que los usuarios de la red de invitados (VLAN 30) puedan acceder a los servidores de datos (VLAN 40) o a los equipos administrativos (VLAN 10).
