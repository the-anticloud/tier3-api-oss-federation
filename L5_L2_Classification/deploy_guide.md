# Deploy Guide — api-oss-federation
**Platform:** Anticloud sovereign infrastructure | Air-gap capable
**Stack:** Python 3.11, asyncio, zeroconf (mDNS), noise protocol, AIOSS_FORMAT

## Prerequisites
Python 3.11+. See stack: Python 3.11, asyncio, zeroconf (mDNS), noise protocol, AIOSS_FORMAT. AIOSS_FORMAT required. PAX 27B weights for AI-assisted features.

## AIOSS Integration
```bash
aioss init --module api-oss-federation --output ./api_oss_federation.aioss
aioss append --chain ./api_oss_federation.aioss --payload ./output.bin --module api-oss-federation
aioss verify --chain ./api_oss_federation.aioss
```

## Air-Gap Deployment
```bash
# On networked machine:
pip download -r requirements.txt -d ./wheels/
# Transfer wheels/ to air-gap host, then:
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX 27B Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(
    model_path="./pax-27b-q4.gguf",
    module="api-oss-federation",
    aioss_chain="./api_oss_federation.aioss",
    classification="L5_NARROW_L2_GENERAL"
)
result = harness.process(input_data)
```

## Verification
```bash
aioss verify --chain ./api_oss_federation.aioss --verbose
python -m api_oss_federation.tests.smoke
```
