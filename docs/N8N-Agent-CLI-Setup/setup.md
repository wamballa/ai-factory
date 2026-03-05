# VM + Codex + n8n Setup

Local AI Factory Infrastructure guide for running Codex agents and n8n automation on an Ubuntu 22.04 VM.

## Purpose

This setup creates a local AI automation environment with:

- Ubuntu VM
- Codex CLI agents
- Git memory/history
- n8n automation server (Docker)

## 1. System Architecture

```text
Windows laptop
  -> VirtualBox
    -> Ubuntu VM (user: ai)
      -> Docker
        -> n8n automation server
          -> SSH Execute Command
            -> Codex CLI agents
```

## 2. Confirm Environment and VM IP

1. Host machine: Windows laptop.
2. Virtualization: Oracle VirtualBox.
3. VM: Ubuntu Server 22.04.
4. VM user: `ai`.
5. In VirtualBox, set network mode to `Bridged Adapter` using the host Wi-Fi adapter.
6. Inside the VM, get the VM IP:

```bash
ip addr
```

7. Example VM IP: `192.168.68.84`.
8. Use this VM IP for SSH, n8n SSH credentials, and n8n browser access.

## 3. Install Base Tools (Ubuntu 22.04)

1. Install required base packages:

```bash
sudo apt update
sudo apt install -y git python3-pip curl ca-certificates
```

2. Install Node.js 20 LTS (recommended for current Codex CLI):

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

3. Verify Node and npm:

```bash
node --version
npm --version
```

## 4. Install and Enable SSH Server

1. Install OpenSSH server:

```bash
sudo apt install -y openssh-server
```

2. Enable and start SSH:

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

3. Verify service status:

```bash
sudo systemctl status ssh
```

## 5. SSH Workflow

1. Start the VM in VirtualBox.
2. Open Windows Terminal.
3. Connect from Windows to the VM:

```bash
ssh ai@192.168.68.84
```

## 6. Install and Authenticate Codex CLI

1. Install Codex CLI globally:

```bash
sudo npm install -g @openai/codex
```

2. Verify installation:

```bash
codex --version
```

3. Start authentication flow:

```bash
codex
```

4. Choose `Sign in with ChatGPT` and complete browser login.

## 7. Set Workspace and Initialize Git Memory

1. Move to workspace:

```bash
cd ~/ai-factory
```

2. Initialize root monorepo history:

```bash
git init
git add .
git commit -m "initial ai-factory memory"
```

3. Add a root `.gitignore` before large commits:

```bash
cat > .gitignore <<'EOF'
.n8n/
node_modules/
__pycache__/
.venv/
.env
.env.*
*.log
EOF
git add .gitignore
git commit -m "add root gitignore"
```

## 8. Use the Project Template for New Micro-SaaS Work

1. Scaffold new projects from the shared template:

```bash
cp -r templates/project-template projects/<new-project-name>
```

2. Fill in project-specific details in:
- `projects/<new-project-name>/README.md`
- `projects/<new-project-name>/CONTEXT.md`

3. Track all tasks in root `TODO.md` (do not create project-specific task files).

## 9. Install Docker

1. Install Docker:

```bash
curl -fsSL https://get.docker.com | sh
```

2. Add current user to Docker group:

```bash
sudo usermod -aG docker $USER
```

3. Log out and back in to apply group membership.

## 10. Run n8n in Docker

1. Start n8n:

```bash
docker run -it --rm \
-p 5678:5678 \
-e N8N_SECURE_COOKIE=false \
-v ~/.n8n:/home/node/.n8n \
docker.n8n.io/n8nio/n8n
```

## 11. Access n8n Web UI

1. Open this URL on the Windows host browser:

```text
http://192.168.68.84:5678
```

2. Do not use `localhost`.
3. Create the n8n owner account.

## 12. Create SSH Credentials in n8n

1. In n8n, create SSH credentials with:
2. Host: `192.168.68.84`
3. Port: `22`
4. User: `ai`
5. Authentication: Password

## 13. Test SSH Execution in n8n

1. Add node: `SSH -> Execute Command`.
2. Run command:

```bash
pwd
```

3. Expected output:

```text
/home/ai
```

## 14. Correct n8n -> Codex Command

1. In the same `SSH -> Execute Command` node, use a non-interactive Codex command:

```bash
cd ~/ai-factory && codex exec "Review current files and suggest the next implementation task."
```

2. This is the correct pattern for n8n because `codex exec` is non-interactive.

## 15. Example n8n Workflow

1. Add `Manual Trigger`.
2. Add `Set` node with field `prompt`.
3. Add `SSH -> Execute Command` node.
4. Command example:

```bash
cd ~/ai-factory && codex exec "{{$json.prompt}}"
```

5. Connect nodes in order:

```text
Manual Trigger -> Set(prompt) -> SSH Execute Command
```

## 16. Troubleshooting

1. `ssh: connect to host ... port 22: Connection refused`
2. Fix:

```bash
sudo systemctl status ssh
sudo systemctl restart ssh
```

3. `docker: permission denied`
4. Fix:

```bash
sudo usermod -aG docker $USER
```

5. Then log out and log in again.

6. `codex: command not found`
7. Fix:

```bash
npm config get prefix
sudo npm install -g @openai/codex
codex --version
```

8. n8n UI not reachable from Windows
9. Check VM IP again:

```bash
ip addr
```

10. Open `http://<vm-ip>:5678` from Windows browser.

11. `git@github.com: Permission denied (publickey)`
12. Create and load an SSH key in the VM:

```bash
ssh-keygen -t ed25519 -C "your_github_email"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
```

13. Add the full public key line to GitHub:
14. `GitHub -> Settings -> SSH and GPG keys -> New SSH key`
15. Set remote and push:

```bash
git remote add origin git@github.com:<github-user>/<repo>.git
git branch -M main
ssh -T git@github.com
git push -u origin main
```

16. If you saved the key in a custom path by mistake, move and add it:

```bash
mv ~/ai-factory/<custom-key-name> ~/.ssh/
mv ~/ai-factory/<custom-key-name>.pub ~/.ssh/
chmod 600 ~/.ssh/<custom-key-name>
chmod 644 ~/.ssh/<custom-key-name>.pub
ssh-add ~/.ssh/<custom-key-name>
```
