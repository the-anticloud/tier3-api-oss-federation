# L5 Narrow / L2 General Classification — api-oss-federation
**Platform:** Anticloud | **PAX:** 27B | **IP:** USPTO pending 2026, Anticloud FZ LLE
**Domain:** Sovereign federation: peer-to-peer Anticloud node discovery and state sync (LAN only)

## L5 Narrow
api-oss-federation specializes in sovereign federation: peer-to-peer anticloud node discovery and state sync (lan only) within the Anticloud sovereign deployment boundary. All operations stay local — no cloud services, no external APIs, no data exfiltration. The narrow scope ensures deterministic, auditable behavior that PAX 27B can reason about precisely.

## L2 General
L2 General means api-oss-federation is available to all 9 Anticloud tiers without per-tier configuration. The same API serves hospital, defense, robotics, and research deployments.

## PAX Integration
PAX 27B is used for federated inference: when a node's GPU is saturated, it can delegate inference to a peer node on the same LAN. AIOSS chains are synchronized between peers so audit trails remain consistent.

## AIOSS Audit Relevance
Every federation event (peer node ID + sync operation + state hash delta) is AIOSS-chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Tamper-evident, offline-verifiable, zero cloud dependency.

## Regulatory / Compliance
NIST SP 800-77 (IPsec VPN), IEC 62443-3-3 (secure communication)
