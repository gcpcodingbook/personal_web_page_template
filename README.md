A personal website template that runs with Flask

#Requirements
flask
gunicorn
nginx

# steps

1. sudo apt-get update
2. sudo apt-get install software-properties-common
3. sudo add-apt-repository universe
4. sudo add-apt-repository ppa:certbot/certbot
5. sudo apt-get update
6. sudo apt-get install certbot python3-certbot-nginx
7. sudo apt-get -y install python3-pip
8. pip3 install flask gunicorn
9. sudo certbot --nginx
10. gunicorn app:app --reload-engine auto

# nginx stuff

Go to /etc/nginx/sites-enabled and create flask_settings and add the below code
server {
listen 80;
listen 443 ssl http2;
ssl_certificate /etc/letsencrypt/live/<your_email>/fullchain.pem;
ssl_certificate_key /etc/letsencrypt/live/<your_email>/privkey.pem;
location / {
proxy_pass http://127.0.0.1:8000;
proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
}
}

sudo nginx
