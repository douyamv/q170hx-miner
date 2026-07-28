# Q170HX Optimized Update for HiveOS

Public beta update for Linux x86-64, HiveOS, and NVIDIA CMP 170HX.

## HiveOS installation

Create a Flight Sheet and choose **Custom miner**.

- Installation URL:
  `https://ghproxy.net/https://github.com/douyamv/q170hx-miner/releases/download/v0.15.5-beta/Q170HX-0.15.5_beta.tar.gz`
- Existing MinerLab account: keep the current username in the miner's extra
  configuration and keep the normal worker name
- Direct Qubic wallet: `%WAL%.%WORKER_NAME%`
- Pool URL: `https://wps.minerlab.io/`
- Hash algorithm: `qubic`

Start with one test worker and verify the pool dashboard before applying the
update to a farm.

## Update

Keep the same Flight Sheet and installation URL. To force an immediate update
from the worker shell:

```bash
/hive/miners/custom/custom-get \
  https://ghproxy.net/https://github.com/douyamv/q170hx-miner/releases/download/v0.15.5-beta/Q170HX-0.15.5_beta.tar.gz \
  -f
miner restart
```

If the accelerated route is temporarily unavailable, use the direct release
URL:

`https://github.com/douyamv/q170hx-miner/releases/download/v0.15.5-beta/Q170HX-0.15.5_beta.tar.gz`

## Verification

Download the `.sha256` sidecar and verify:

```bash
sha256sum -c Q170HX-0.15.5_beta.tar.gz.sha256
```

This is a CMP 170HX-specific beta. Do not run another miner on the same GPUs.
