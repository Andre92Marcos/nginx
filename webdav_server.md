# How to create a webdav server with nginx



Go to /etc/nginx/sites-available and create a file called webdav with:

    server{
            listen 8001 default_server;
            server_name webdav.server;
            location / {
                root /var/www/upload;
                dav_methods PUT;
            }
    }


Then create the /var/www/upload directory

    sudo mkdir /var/www/uploads
    sudo chmod 776 /var/www/uploads

Create a symbolic link in sites-enabled

    cd /etc/nginx/sites-enabled
    sudo ln -s /etc/nginx/sites-available/webdav

Restart nginx

    sudo systemctl restart nginx

Finally check if server is up and listening on port 8001

    ss -nltp