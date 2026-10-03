# Developer Cookbook — api-oss-federation
**Stack:** Python 3.11, asyncio, zeroconf (mDNS), noise protocol, AIOSS_FORMAT
**Domain:** Sovereign federation: peer-to-peer Anticloud node discovery and state sync (LAN only)
**License:** Apache-2.0 | **IP:** USPTO pending 2026, Anticloud FZ LLE

## Core Usage

```python
from api_oss_federation import FederationNode
node = FederationNode(node_id='hospital_node_01', aioss_chain='./federation.aioss')
node.start_discovery()  # mDNS on LAN only, no internet
peers = node.discovered_peers()
result = await node.federated_infer(peers[0], prompt='Analyze biosignal', max_tokens=256)
```

## AIOSS Chain Append

```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()

# After every api-oss-federation output:
chain_hash = aioss_append("./api_oss_federation.aioss",
                           result_bytes, "api-oss-federation")
```

## Performance & Integration

Performance: profile with api-oss-devtools. Benchmark with api-oss-analytics. Integration: all api-oss-federation operations are logged to api-oss-logging and audited by api-oss-compliance.
