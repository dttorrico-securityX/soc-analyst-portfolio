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

Crear listas:
echo "administrator" > users.txt
echo "P@ssw0rd" > passwords.txt

Comando:
hydra -L users.txt -P passwords.txt rdp://192.168.20.30 -V -f

## 3. Detección en Wazuh
- Event ID Windows: 4625 (Fallo) y 4624 (Éxito)
- En Wazuh Dashboard busca: rule.id: 60122 AND 192.168.10.10

Regla Custom Wazuh en /var/ossec/etc/rules/local_rules.xml:
<rule id="100200" level="10" frequency="8" timeframe="120">
<if_matched_sid>60122</if_matched_sid>
<same_source_ip />
<description>Possible RDP Brute Force</description>
</rule>

## 4. Triaje L1 - Informe

```
ID: SOC-2026-001
Host: PC Windows 192.168.20.30
IP Origen: 192.168.10.10 (Kali)
Verdicto: TRUE POSITIVE - Lab Controlado
Acción: Bloquear IP en FortiGate, habilitar Account Lockout.

Timeline:
- 21:10:01 - Primer fallo 4625
- 21:10:45 - 15 fallos desde misma IP
- 21:11:20 - Alerta Wazuh 100200 disparada
```

## 5. Evidencias
Ver carpeta screenshots/
