# 🐳 Dock-To-Go — One-Command Docker & Compose Installer (Ubuntu)

 *"Ubuntu-ready Docker + Compose bootstrap with zero surprises."*


```
           __
       ___( o)         Dock-To-Go
    .-'     )          "Whale hello there!"
---'~~~---~~'--.
```

---


## 🚀 Quick start (Ubuntu)

> **Heads up:** Run this on **Ubuntu** with `sudo` privileges. The script enables the Docker daemon and adds your user to the `docker` group.

### Option A — Run the installer script
First install the script from the repo
```bash
bash install.sh
```

### Option B — Run each command manually

Use these **unaltered** commands (exactly as in `install.sh`).

```bash
sudo apt update && sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```bash
sudo apt update && sudo apt install -y docker-ce && sudo systemctl enable --now docker
```

```bash
sudo usermod -aG docker $USER && newgrp docker
```

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && sudo chmod +x /usr/local/bin/docker-compose
```

**Verify installation**

```bash
docker --version && docker-compose --version
```

---

## 🧰 What gets installed (and why)

* **Docker CE** via the official Docker APT repository (keeps you on trusted, up-to-date builds)
* **docker-compose** binary placed at `/usr/local/bin/docker-compose` and made executable
* **Systemd** is enabled for Docker so it starts right away and on boot
* **User group setup** lets you run `docker` without `sudo` after a fresh shell (we use `newgrp docker` to avoid logout/login)

---

## 🔍 Troubleshooting

* `newgrp docker` opens a new shell. If `docker` still needs sudo, try logging out/in.
* On non-AMD64 machines (e.g., ARM), adjust the APT arch in the repo line accordingly.
* If `jq` is missing for the Compose download line, install it: `sudo apt install -y jq`.
* Firewall/WSL notes: ensure your distro has `systemd` enabled and that Docker Desktop/WSL2 isn’t conflicting.

---

## 🧪 Sanity check

```bash
docker run hello-world
```

You should see Docker pull and run the test image successfully.

---

## 🤝 Contributing

Spotted a doc typo or want an emoji somewhere fun? PRs welcome! Please avoid changing the install commands — they’re intentionally **verbatim**.

---

## 📄 License

This project ships with **MIT** (see `LICENSE`). Feel free to re-license to match your org’s needs.

---
