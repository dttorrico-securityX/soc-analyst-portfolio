# Evidencias LAB-01 - RDP Brute Force

Aquí van las 4 capturas obligatorias del ataque:

### 1. Ataque en Kali
Archivo: `01-hydra-command.png`
Comando: hydra -L users.txt -P passwords.txt rdp://192.168.20.30 -V -f

### 2. Logs en Windows
Archivo: `02-windows-4625.png`
Ruta: Visor de eventos > Seguridad > Event ID 4625

### 3. Alerta en Wazuh
Archivo: `03-wazuh-dashboard.png`
Ruta: Wazuh Dashboard > Threat Hunting > Eventos 4625 desde 192.168.10.10

### 4. Tráfico en FortiGate
Archivo: `04-fortigate-log.png`
Ruta: FortiGate > Log & Report > Forward Traffic - Puerto 3389

---
**Instrucciones:** Arrastra tus 4 capturas PNG/JPG a esta carpeta usando "Agregar archivo > Cargar archivos"
