# Q170HX Optimized Update for HiveOS

Public beta update for Linux x86-64, HiveOS, and NVIDIA CMP 170HX.

## HiveOS installation

Create a Flight Sheet and choose **Custom miner**.

- Installation URL:
  `https://github.com/douyamv/q170hx-miner/releases/download/v0.15.2-beta/Q170HX-0.15.2_beta.tar.gz`
- Wallet and worker template: `%WAL%.%WORKER_NAME%`
- Pool URL: `https://wps.minerlab.io/`
- Hash algorithm: `qubic`

The wallet must be a 60-letter uppercase Qubic identity. Start with one test
worker and verify the pool dashboard before applying the update to a farm.

## Update

Keep the same Flight Sheet and installation URL. To force an immediate update
from the worker shell:

```bash
/hive/miners/custom/custom-get \
  https://github.com/douyamv/q170hx-miner/releases/download/v0.15.2-beta/Q170HX-0.15.2_beta.tar.gz \
  -f
miner restart
```

## Verification

Download the `.sha256` sidecar and verify:

```bash
sha256sum -c Q170HX-0.15.2_beta.tar.gz.sha256
```

This is a CMP 170HX-specific beta. Do not run another miner on the same GPUs.
