# Launch an EC2 instance
### 1. Choose Ubuntu as the OS
### 2. Select an instance type
### 3. Download the PEM key
### 4. Allow inbound traffic for SSH (22), HTTPS (443), and HTTP (80)
### 5. Launch the instance

---

## SSH into your instance
```sh
# Open Git Bash in the folder where the PEM file is located
ssh -i <your-key.pem> ubuntu@<your-instance-ip>
```

## Update and install dependencies
```sh
sudo apt update && sudo apt upgrade -y
sudo apt install -y build-essential curl
```

## Install Node.js with NVM
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install --lts
```

## Install Process Manager (PM2)
```sh
sudo npm install -g pm2
