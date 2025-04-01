# Gensyn Testnet Node Guide 
![Gensyn Logo Animation](https://cdn.prod.website-files.com/66bc6da8fe284e4693088ff7/67e9178ce812f9abbc62296c_Gensyn-logo-anim_2%202.gif)

## Hardware Requirements

| Component       | Requirement                                      | Notes                                      |
|-----------------|--------------------------------------------------|--------------------------------------------|
| **CPU**         | Minimum 16GB RAM                                 | More RAM (e.g., 32GB+) recommended for larger models or datasets |
| **GPU (Optional)** | CUDA-supported devices: <br> - NVIDIA RTX 3090 <br> - NVIDIA RTX 4090 <br> - NVIDIA A100 <br> - NVIDIA H100 | Optional; node can run in CPU-only mode without a GPU |

## Install

### 1. Install dependencies
1. Update VPS
```
sudo apt-get update && sudo apt-get upgrade -y
```
2. Install Nodejs
```
curl -sSL https://raw.githubusercontent.com/zunxbt/installation/main/node.sh | bash
```
3. Other dependencies
```
sudo apt update && sudo apt install -y python3 python3-venv python3-pip curl screen git yarn && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && sudo apt update && sudo apt install -y yarn
```
4. Install Docker
```
# Remove old Docker installations
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

# Add Docker repository
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Test Docker
sudo docker run hello-world
```
5. Add Python
```
sudo apt-get install python3 python3-pip
```
```
sudo apt install python3.10-venv
```
6. Install Yarn
```
curl -o- -L https://yarnpkg.com/install.sh | sh
```
```
export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"
```
```
source ~/.bashrc
```
7. Check Node JS, Yarn and Docker version before start
```
docker version
node -v
yarn -v
```
### 2. Install RL SWARM
1. Clone the repo
```
git clone https://github.com/gensyn-ai/rl-swarm/
cd rl-swarm
```
2. Run the swarm in background using screen
```
screen -S swarm
```
Install it
```
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```
3. Login the dashboard

Waiting for it shows to **`Waiting for userData.json to be created..`**

Log in to your dashboard on browser like Chrome/Edge with email and get OTP.

- VPS: http://YourVPSIP:3000/

4. Quit and Rejoin the screen 

Quit: Ctrl A+D
Rejoin: 
```
screen -r swarm
```

### 4. Get OTP with ngrok

1. Sign up: https://ngrok.com/
2. Go to authen token: https://dashboard.ngrok.com/get-started/your-authtoken - Click to show the key then do below step
3. Paste the token add to VPS
```
ngrok config add-authtoken $YOUR_AUTHTOKEN
```
4. Make the ngrok works 
```
ngrok http 3000
```
5. Copy redirect link to port 3000
6. Login and get OTP
