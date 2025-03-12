# Launch an EC2 instance
# 1. Choose Ubuntu as the OS
# 2. Select an instance type
# 3. Download the PEM key
# 4. Allow inbound traffic for SSH (22), HTTPS (443), and HTTP (80)
# 5. Launch the instance
```

```sh
# SSH into your instance
# Open Git Bash in the folder where the PEM file is located
ssh -i <your-key.pem> ubuntu@<your-instance-ip>
```

```sh
# Update and install dependencies
sudo apt update && sudo apt upgrade -y
sudo apt install -y build-essential curl
```

```sh
# Install Node.js with NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install --lts
```

```sh
# Install Process Manager (PM2)
sudo npm install -g pm2
