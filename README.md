# NMOSIS09Forge Pro (v1.0.0)

### AMWA NMOS IS-09 System Discovery & Zero-Configuration Node Bootstrapping Studio

---

## Overview

**NMOSIS09Forge Pro** is a high-precision broadcast engineering workbench and automation utility built for SMPTE ST 2110 IP facility engineers, broadcast system architects, OB van integrators, and equipment manufacturers. It provides global parameter synthesis, DHCP Option 114 URL encoding, DNS-SD `_nmos-system._tcp` service synthesis, multi-stage node bootstrapping emulation, and 10-point normative compliance verification across:

- **AMWA NMOS IS-09 v1.0.0**: System Parameters Specification  
- **AMWA BCP-002-01**: Natural Grouping & Discovery Best Current Practice  
- **RFC 8910 & RFC 2132**: DHCP Option 114 (Captive-Portal / Zero-Config URL)  
- **RFC 6763**: DNS-Based Service Discovery (DNS-SD `_nmos-system._tcp`)  
- **IEEE 1588-2008 / SMPTE ST 2059-2**: PTP Precision Time Protocol Domain & Announcement Intervals  
- **AMWA NMOS IS-04 v1.3**: Automatic Registration API Priority Failover

---

## Key Capabilities

1. **System Global Parameters Synthesizer (`/x-nmos/system/v1.0/global`)**:  
   - Generates compliant JSON payloads exposing system UUID, PTP timing configurations (SMPTE ST 2059-2 Domain 127 default), syslog telemetry targets, and prioritized IS-04 Registration APIs.  
2. **DHCP Option 114 Encoder**:  
   - Formats discovery URLs into standard DHCP Option 114 byte representations (raw string and colon-separated hexadecimal) for Cisco, Arista, and ISC-DHCP server configurations.  
3. **DNS-SD Service Generator**:  
   - Synthesizes RFC 6763 PTR, SRV, and TXT resource records for `_nmos-system._tcp` fallback discovery when DHCP Option 114 is unavailable.  
4. **Autonomous Node Bootstrapping Simulator**:  
   - Simulates complete zero-touch lifecycle: cold start \-\> DHCP Option 114 query \-\> DNS-SD fallback \-\> HTTP GET `/global` ingestion \-\> PTP lock \-\> IS-04 Registration failover sequence.  
5. **10-Point Normative Compliance Auditor**:  
   - Automated pass/fail verification validating system UUID format, PTP domain ranges (0..127), announcement/sync intervals, registration endpoint priorities, syslog syntax, and zero-conf determinism.  
6. **Production Python CLI (`is09-cli.py`)**:  
   - Headless CLI for broadcast DevOps pipelines, generating `/global` schemas, DHCP hex options, and DNS zone configurations.

---

## Getting Started

### Web Studio

Open `source-code/index.html` in any web browser. Runs 100% locally with zero external network or cloud dependencies.

### Command-Line Interface

\# Generate IS-09 /global configuration JSON

python3 build/is09-cli.py global \--domain 127 \--reg-primary "https\://reg1.prod.tv/x-nmos/registration/v1.3"

\# Encode DHCP Option 114 URL into hex

python3 build/is09-cli.py dhcp114 \--url "http\://is09.prod.tv/x-nmos/system/v1.0"

\# Generate DNS-SD Zone Configuration

python3 build/is09-cli.py dnssd \--host "is09.prod.tv" \--port 80

### Automated Testing

python3 test\_is09.py