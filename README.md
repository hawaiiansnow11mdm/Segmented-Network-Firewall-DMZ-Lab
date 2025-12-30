# Segmented-Network-Firewall-DMZ-Lab

Laboratorio di rete realizzato in Cisco Packet Tracer con focus su segmentazione, sicurezza e simulazione di traffico tra zone (LAN, DMZ, WAN) utilizzando firewall ASA.

## Obiettivo del progetto

Simulare una rete aziendale segmentata con firewall ASA, VLAN, ACL e routing per comprendere come isolare correttamente le reti interne e proteggere i server nella DMZ.

---

## Topologia di rete

- **LAN interna**:
  - PC0 (IT): 192.168.10.10
  - PC1 (Administration): 192.168.10.11
  - Gateway: ASA0 (192.168.10.1)

- **DMZ**:
  - Server DMZ: 192.168.30.100
  - PC Sales (client DMZ): 192.168.30.50
  - Gateway: ASA1 (192.168.30.1)

- **Firewall ASA**:
  - ASA0 (verso LAN e Router):
    - inside: 192.168.10.1 (VLAN 10)
    - outside: 192.168.0.2 (VLAN 2)
  - ASA1 (verso DMZ e Router):
    - inside: 192.168.30.1 (VLAN 30)
    - outside: 192.168.0.6 (VLAN 2)

- **Router**:
  - G0/0: 192.168.0.1 (verso ASA0)
  - G0/1: 192.168.0.5 (verso ASA1)

---

## Regole ACL configurate

### ASA0
- Permettere `icmp`, `http`, `https`, `dns` da LAN verso outside
- Access-list `INSIDE-OUT` associata all'interfaccia `inside`

### ASA1
- Permettere `icmp` e traffico in uscita da DMZ verso LAN
- Access-list `DMZ-OUT` associata all'interfaccia `inside`

---

## Routing

### ASA0
```bash
route outside 192.168.30.0 255.255.255.0 192.168.0.1
```

### ASA1
```bash
route outside 192.168.30.0 255.255.255.0 192.168.0.1
```
