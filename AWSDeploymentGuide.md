### Make a new folder
```sh
mkdir <folder_name>
```
### Git clone your repo
```sh
git clone <your_repository_url>
```
### Create an ecosystem.config.js file with the following format
```js
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

### Install PM2 globally
```sh
sudo npm install -g pm2
```

### Start your server with PM2
```sh
pm2 start ecosystem.config.js
```

### Create an A record in the DNS and set the value to the server's IP address

### Install Nginx
```sh
sudo apt install nginx -y
```

### Navigate to Nginx sites-available directory
```sh
cd /etc/nginx/sites-available
```
### Create and edit the configuration file for your domain
```sh
nano <your_domain>
```

### Paste the following content in the file:
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
### Set necessary permissions for the configuration file
```sh
sudo chmod 644 /etc/nginx/sites-available/<your_domain>
```
### Create a symbolic link to enable the configuration
```sh
sudo ln -s /etc/nginx/sites-available/<your_domain> /etc/nginx/sites-enabled/
```
### Test Nginx configuration
```sh
sudo nginx -t
```
### Verify symbolic link
```sh
ls -l /etc/nginx/sites-enabled/
```
### Restart Nginx
```sh
sudo systemctl restart nginx
```
### Obtain SSL certificate using Certbot (ensure Certbot is installed)
```sh
sudo apt install certbot python3-certbot-nginx -y
```
### Run Certbot to configure SSL
```sh
sudo certbot --nginx -d <your_domain>
