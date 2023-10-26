## Ngnix
Ngnixda yangi server yaratib olishimz kerak.
```angular2html
sudo nano /etc/nginx/sites-available/myproject
```
Va Ngnix ning yangi yaralgan ``myproject`` file ga
```angular2html
server {
    listen 80;
    server_name server_domain_or_IP;

    location = /favicon.ico { access_log off; log_not_found off; }
    location /static/ {
        root /var/www ;
    }

    location / {
        include proxy_params;
        proxy_pass http://unix:/run/gunicorn.sock;
    }
}
```

Va Ngnixni enable qilishimiz mumkin `sites-enabled` filga ga

```angular2html
sudo ln -s /etc/nginx/sites-available/myproject /etc/nginx/sites-enabled
```
Ngnix ni test qilib olamiz
```angular2html
sudo nginx -t
```

Ngnixni restart qilamiz
```angular2html
sudo systemctl restart nginx
```
Ngnix serverimizga 80 porta ishlashga ruxsat berganimizdan keyin 8000 port ni olib tashlashimiz kerak bo'ladi.
```angular2html
sudo ufw delete allow 8000
sudo ufw allow 'Nginx Full'
```

### Loyhamiz domain yoki ip da ishlab turibdi agar ishlamasa error log ni ko'rishimiz va docs ga qaytib errorni tog'rilashimz mumkin.
```angular2html
sudo tail -F /var/log/nginx/error.log
```