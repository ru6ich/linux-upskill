# SSH Connection — Logbook / Cheat Sheet

### Goal
Be able to connect to a cloud Ubuntu server from Fedora safely, repeatably, and with minimal friction.

---

## Day 0 — Setup (Local: Fedora)
### Commands / Notes
- Generate a dedicated SSH key (recommended: one key per purpose):
```bash
  ssh-keygen -t ed25519 -a 64 -C "linuxupskill-yc" -f ~/.ssh/linuxupskill_yc
```

* `-t ed25519` — modern key type

* `-a 64` — more KDF rounds (harder to brute-force if key is stolen)

* `-f` — output file name (private key, public key will be .pub)

* Show the public key (this is what you paste into the cloud VM settings):
```bash
  cat ~/.ssh/linuxupskill_yc.pub
```
Public key format:
ssh-ed25519 <BASE64> <comment>

Secure permissions (important):
```bash
  chmod 700 ~/.ssh
  chmod 600 ~/.ssh/linuxupskill_yc
```
###Issues/Questions
* If passphrase is enabled, use ssh-agent to avoid typing it repeatedly: 
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/linuxupskill_yc
```
###Result
* Private key stored locally, public key ready to be installed on the server.

###Next
* Create a VM and install the public key into the VM user account.
