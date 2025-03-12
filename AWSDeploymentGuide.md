# Make a new folder
mkdir <folder_name>
```

```sh
# Git clone your repo

git clone <your_repository_url>
```

```js
// Create an ecosystem.config.js file with the following format

module.exports = {
    apps: [
      {
        name: '<app_name>',
        script: '<server_script_path>',
        env: {      
            MONGO_URI: "<your_mongo_uri>",
            PORT: <your_port>,
            NODE_ENV: "production",
            ACCESS_TOKEN_SECRET: "<your_access_token_secret>",
            REFRESH_TOKEN_SECRET: "<your_refresh_token_secret>",
            ACCESS_TOKEN_EXPIRATION: 7200,  // 15 minutes    
            REFRESH_TOKEN_EXPIRATION: 604800, // 7 days
            // Add other environment variables here
        }
      }
    ]
};
```

```sh
# Install PM2 globally
sudo npm install -g pm2
```

```sh
# Start your server with PM2
pm2 start ecosystem.config.js
```

```sh
# Create an A record in the DNS and set the value to the server's IP address

# Install Nginx
sudo apt install nginx -y
```

```sh
# Navigate to Nginx sites-available directory
cd /etc/nginx/sites-available
```

```sh
# Create and edit the configuration file for your domain
nano <your_domain>
```

**Paste the following content in the file:**

```nginx
server {
    listen 80;
    server_name <your_domain>;

    location / {
        proxy_pass http://localhost:<your_app_port>; 
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

```sh
# Set necessary permissions for the configuration file
sudo chmod 644 /etc/nginx/sites-available/<your_domain>
```

```sh
# Create a symbolic link to enable the configuration
sudo ln -s /etc/nginx/sites-available/<your_domain> /etc/nginx/sites-enabled/
```

```sh
# Test Nginx configuration
sudo nginx -t
```

```sh
# Verify symbolic link
ls -l /etc/nginx/sites-enabled/
```

```sh
# Restart Nginx
sudo systemctl restart nginx
```

```sh
# Obtain SSL certificate using Certbot (ensure Certbot is installed)
sudo apt install certbot python3-certbot-nginx -y
```

```sh
# Run Certbot to configure SSL
sudo certbot --nginx -d <your_domain>
