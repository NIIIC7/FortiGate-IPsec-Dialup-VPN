# 🚀 Implementación de VPN IPsec de Acceso Remoto (Dialup) en FortiGate

Guía técnica paso a paso y documentación de despliegue para una **VPN IPsec de Acceso Remoto (Modo Dialup)** sobre un firewall **FortiGate**, utilizando autenticación **XAUTH** con el cliente **FortiClient**.

---

## 📋 Resumen del Proyecto

Este repositorio documenta la configuración y verificación de un túnel VPN seguro para permitir que usuarios remotos accedan a los recursos de una red interna corporativa (`10.0.11.0/24`) a través de un canal cifrado[cite: 14].

* **Plataforma:** Fortinet FortiGate (VM)[cite: 14]
* **Cliente VPN:** FortiClient VPN[cite: 14]
* **Nombre del túnel:** `ravpn`[cite: 14]
* **Interfaz WAN:** `port1`[cite: 14]
* **Interfaz LAN de destino:** `port2` (red `10.0.11.0/24`)[cite: 14]
* **Rango de IP para clientes:** `192.168.100.10 – 192.168.100.250`[cite: 14]

---

## ⚙️ Parámetros de Configuración

| Componente | Parámetro / Valor |
| :--- | :--- |
| **Tipo de VPN** | IPsec Dialup (Acceso remoto)[cite: 14] |
| **Modo IKE** | Agresivo (Aggressive), IKEv1[cite: 14] |
| **Autenticación Fase 1** | Pre-shared Key + XAUTH (Auto server)[cite: 14] |
| **Cifrado / Hash (Fase 1 & 2)** | DES - SHA1, Grupo Diffie-Hellman 14[cite: 14] |
| **Split Tunnel** | Habilitado hacia `10.0.11.0/24`[cite: 14] |
| **Grupo de Autorización** | `VPN SSL GROUP`[cite: 14] |

---

## 🛠️ Pasos de Implementación Documentados

1. **Gestión de Usuarios y Grupos:** Creación de usuarios locales (`cristian`, `guest`, `nick`)[cite: 14] y asignación al grupo de autenticación `VPN SSL GROUP`[cite: 14].
2. **Configuración del Túnel IPsec (Fase 1 y Fase 2):** Establecimiento del modo Dialup[cite: 14], selectores de tráfico[cite: 14], asignación de IPs virtuales por rango y parámetros de seguridad.
3. **Políticas de Firewall:** Creación de la regla de control de acceso (`vpn_VPN_Lab_remote`) desde la interfaz del túnel (`ravpn`) hacia la red interna (`port2`) con inspección *Flow-based*[cite: 14].
4. **Verificación y Pruebas:** Comprobación de estado del túnel en el monitor de FortiGate[cite: 14], validación del adaptador virtual en el cliente (`ipconfig`)[cite: 14] y revisión de registros en los *VPN Events*[cite: 14].

---

## 🔒 Recomendaciones de Seguridad

* **Actualización de Cifrado:** Migrar de los algoritmos DES/SHA1 (empleados en este laboratorio académico/de pruebas) a **AES-256** y **SHA-256** para entornos de producción[cite: 14].
* **Modo IKE Principal:** Evaluar el uso de IKE Main Mode en lugar de Aggressive Mode para mayor protección de identidad[cite: 14].
* **Perfiles UTM:** Habilitar perfiles de seguridad avanzados (IPS, Antivirus) sobre la política de la VPN[cite: 14].
