# Parcial 1 — Seguridad con FortiGate

**Estudiante:** Abdul Djalo
**Matrícula:** 2023-1600

## Video demostrativo

[Ver video en YouTube](PEGerAQUI-EL-ENLACE-DEL-VIDEO)

## Propósito

Implementar y demostrar una infraestructura de red segmentada y protegida con un firewall FortiGate, aplicando segmentación por VLANs, salida a Internet con NAT, control de acceso por SSH según la VLAN de origen y seguridad de puertos en el switch. Toda la configuración y demostración del FortiGate se realiza por su interfaz gráfica (GUI).

## Direccionamiento (basado en la matrícula 2023-1600)

| Red | VLAN | Uso | Gateway |
|---|---|---|---|
| 172.23.16.0/25 | 10 | Usuarios (DHCP) | 172.23.16.1 |
| 172.23.16.160/27 | 20 | Usuarios administrativos (DHCP) | 172.23.16.161 |
| 172.23.16.128/28 | 30 | Servidores (WEB .130, DB .131) | 172.23.16.129 |
| 200.23.16.0/30 | — | Enlace ISP – FortiGate | 200.23.16.1 |
| 200.23.16.4/30 | — | Enlace ISP – Sucursal | 200.23.16.5 |

## Equipos

| Equipo | Plataforma | Función |
|---|---|---|
| ISP | Cisco C2691 | Router del proveedor, IP públicas y NAT a Internet |
| FGT | FortiGate-VM 7.0.9 | Firewall: VLANs, DHCP, NAT y control de SSH |
| SW | Cisco IOSvL2 | Switch con VLANs, trunk 802.1Q y port-security |
| SUCURSAL | Cisco C2691 | Router de sucursal con su PC |
| PC10 | Alpine Linux | Usuario de la VLAN 10 |
| PC20 | Alpine Linux | Usuario administrativo de la VLAN 20 |
| WEB | Alpine Linux | Servidor web (HTTP) |
| DB | Alpine Linux | Servidor de base de datos (MariaDB, 3306) |

## Requisitos implementados

### 3. Salida a Internet
Ruta por defecto y NAT en el FortiGate. El PC de la VLAN 10 obtiene dirección por DHCP y tiene salida al ISP, verificada con `ping` y `traceroute` a Internet.

### 5. Direccionamiento y VLANs
Direccionamiento basado en la matrícula, VLAN 10 (usuarios con DHCP), VLAN 20 (administrativos) y servidores en una red /28. Trunk 802.1Q entre el switch y el FortiGate, y hostname configurado en todos los equipos.

### 7. Port-security en puertos de acceso
Port-security activado en los puertos de acceso del switch con un máximo de 2 direcciones MAC por puerto y acción de violación *shutdown*.

### 8. Servidores
Servidor web operativo por HTTP y servidor de base de datos con MariaDB escuchando en el puerto 3306.

### 4. SSH solo desde la VLAN 20
Políticas en el FortiGate que permiten el acceso SSH a los servidores únicamente desde la VLAN 20 y lo deniegan con registro desde la VLAN 10.

## Estructura del repositorio

```
Parcial1-FortiGate-2023-1600/
├── README.md
└── configuraciones/
    ├── FGT.txt
    ├── SW.txt
    ├── ISP.txt
    ├── SUCURSAL.txt
    ├── WEB.txt
    ├── DB.txt
    ├── PC10.txt
    └── PC20.txt
```
