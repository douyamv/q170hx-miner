# Q170HX Miner for HiveOS

Encrypted public beta of the CMP 170HX Qubic Epoch-223 CUDA miner.

## Current release

- Version: `0.15.0-beta`
- Target: Linux x86-64, HiveOS, NVIDIA CMP 170HX / `sm_80`
- Measured development rig: about 47.35 MH/s on the experimental card and
  about 382-385 MH/s across eight cards, depending on clocks and thermals
- Unit: one MH/s is one million logical public-key/nonce candidates per second
- Release payload: AES-256-CTR encrypted, Ed25519 signed, binaries stripped
- Startup safety: free-VRAM preflight, guarded batch reduction, sequential
  512 MiB random2 host-pool loading, and immediate host-pool release

This is a beta release. Verify earnings and accepted work on your own pool
dashboard before scaling it to a large farm.

## HiveOS installation

Create a Flight Sheet and choose **Custom miner**.

- Installation URL:
  `https://github.com/douyamv/q170hx-miner/releases/download/v0.15.0-beta/Q170HX-0.15.0_beta.tar.gz`
- Wallet and worker template: `%WAL%.%WORKER_NAME%`
- Pool URL: `https://wps.minerlab.io/`
- Hash algorithm: `qubic`

The wallet must be a 60-letter uppercase Qubic identity. The package validates
the configuration before starting any CUDA process.

## Creator fee

The policy is disclosed in the miner log and is calculated only from measured
performance above the legacy CMP 170HX baseline:

```text
legacy total       = 35.6125 MH/s * number of cards
increment          = max(measured total - legacy total, 0)
creator equivalent = 70% * increment
runtime fraction   = creator equivalent / measured total
```

The legacy baseline is never charged. At 382.1 MH/s on eight cards, the
creator equivalent is 68.04 MH/s and the time fraction is about 17.8069%.
Long owner/creator WPS phases minimize task-switch and random2 rebuild overhead.

## Verification

Download the `.sha256` sidecar and verify:

```bash
sha256sum -c Q170HX-0.15.0_beta.tar.gz.sha256
```

The archive contains the Ed25519 public key, the signed encrypted-payload
manifest, and the verification performed by `h-run.sh` before decryption.
The signing private key is kept offline and is not included in this repository
or any release asset.

## Important limits

- Obfuscation and in-memory decryption raise the reverse-engineering cost but
  cannot make client-side GPU code impossible to recover.
- The release does not hide the creator-fee policy.
- Current optimization and live measurements are specific to CMP 170HX.
- Do not run a second miner on the same GPU; the free-VRAM guard will reduce
  the batch or refuse startup rather than overcommit.
