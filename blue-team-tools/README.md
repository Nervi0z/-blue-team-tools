<div align="center">
  <img src="./assets/img/header.svg" alt="blue-team-tools" width="100%"/>
</div>

---

Índice operacional de herramientas para Blue Team: defensa, detección, respuesta a incidentes y análisis. Cubre SOC, DFIR, CTI, monitorización de red, endpoint, SIEM y criptografía.

Preferencia por herramientas open source, activamente mantenidas y con aplicación real en flujos defensivos.

> Todas las herramientas listadas aquí son para monitorización autorizada, análisis, respuesta a incidentes e investigación de seguridad. Usarlas contra sistemas que no son tuyos o sin permiso explícito es ilegal.

---

## Contenido

| # | Dominio | Herramientas destacadas |
|---|---------|------------------------|
| 01 | [Asset Discovery & Vulnerability Management](./tools/01-asset-discovery-vulnerability-management.md) | Nmap, Shodan, GVM/OpenVAS, Nessus, Amass |
| 02 | [Network Security Monitoring](./tools/02-network-security-monitoring.md) | Suricata, Zeek, Wireshark, tcpdump, Snort |
| 03 | [Phishing Analysis & Defense](./tools/03-phishing-analysis-defense.md) | urlscan.io, VirusTotal, Any.Run, GoPhish |
| 04 | [Digital Forensics & Incident Response](./tools/04-digital-forensics-incident-response.md) | Volatility, Autopsy, KAPE, FTK Imager |
| 05 | [Cyber Threat Intelligence](./tools/05-cyber-threat-intelligence.md) | MISP, OpenCTI, MITRE ATT&CK, AbuseIPDB |
| 06 | [Cryptography](./tools/06-cryptography.md) | OpenSSL, GnuPG, ccrypt |
| 07 | [Miscellaneous Defensive Tools](./tools/07-miscellaneous-defensive-tools.md) | Lynis, osquery, Sysinternals, Trivy, STIX/TAXII |
| 08 | [Endpoint Security & Analysis](./tools/08-endpoint-security-analysis.md) | Sysmon, Wazuh, Velociraptor, EDR/XDR concepts |
| 09 | [SIEM & Log Management](./tools/09-security-information-event-management.md) | Elastic Stack, Graylog, Security Onion, Splunk |

---

## Estructura de cada entrada

Cada herramienta documenta:

- Qué hace y por qué es útil en contexto defensivo
- Instalación con comandos reales
- Ejemplos de uso orientados a Blue Team
- Alternativas y notas de configuración

---

## Quick reference

Comandos frecuentes para orientarse rápido durante un turno SOC o una investigación.

**Captura y análisis de red**
```bash
# Captura rápida en eth0, sin resolución de nombres
sudo tcpdump -i eth0 -nn -w capture.pcap

# Extraer campos DNS de un pcap con zeek
zeek -r capture.pcap && cat dns.log | zeek-cut ts id.orig_h query answers

# Filtrar tráfico HTTP en Wireshark
http.request.method == "POST"
tls.handshake.type == 1
```

**Reconocimiento de activos propios**
```bash
# Inventario de hosts activos
sudo nmap -sn 192.168.1.0/24

# Scan detallado de servidor crítico
sudo nmap -sS -sV -O -sC -T4 192.168.1.100 -oN resultado.txt

# Superficie externa: subdominios propios
amass enum -passive -d example.com -o subdomains.txt

# Exposición en internet
shodan search net:203.0.113.0/24 --fields ip_str,port,org
```

**Análisis de endpoint (Windows)**
```bash
# Instalar Sysmon con config
sysmon64.exe -accepteula -i sysmon_config.xml

# Consultar procesos sin binario en disco (osqueryi)
SELECT pid, name, path FROM processes WHERE on_disk = 0;

# Conexiones activas con proceso propietario (osqueryi)
SELECT pid, name, local_address, local_port, remote_address, remote_port
FROM process_open_sockets WHERE family = 2;
```

**Verificación de integridad y certificados**
```bash
# Hash SHA-256 de un archivo
sha256sum archivo.zip

# Inspeccionar certificado TLS de un servidor
openssl s_client -connect example.com:443 2>/dev/null | openssl x509 -noout -dates -subject

# Verificar firma GPG de un release
gpg --verify archivo.sig archivo.tar.gz
```

**Análisis de correo sospechoso**
```bash
# Cabeceras: leer Received: de abajo a arriba
# Buscar Authentication-Results: spf=fail / dkim=fail / dmarc=fail
# Lookup del IP origen:
shodan host <IP-origen>
```

**Suricata / IDS**
```bash
# IDS mode en eth0
sudo suricata -c /etc/suricata/suricata.yaml -i eth0

# Actualizar reglas
sudo suricata-update

# Ver alertas en tiempo real
tail -f /var/log/suricata/fast.log
```

---

## Contribuciones

Falta una herramienta, un enlace está roto o una entrada está desactualizada — las contribuciones son bienvenidas. Ver [CONTRIBUTING.md](./CONTRIBUTING.md) para el proceso.

---

## Licencia

[MIT](./LICENSE)
