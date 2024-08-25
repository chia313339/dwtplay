# dwtplay

# Build the Docker image
```
sudo docker build -t dwt_fishing .
sudo docker build -t dwt_jackpot .
sudo docker build -t dwt_poker .
```

# Run the Docker container on port 
```
sudo docker run -d -p 8701:80 --restart always dwt_fishing 
sudo docker run -d -p 8702:80 --restart always dwt_jackpot 
sudo docker run -d -p 8703:80 --restart always dwt_poker 
```

# setting nginx
sudo nano /etc/nginx/sites-available/default

```
server {
    listen 80;
    server_name domain.com;

    location / {
        proxy_pass http://localhost:8701;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```