# Black Cobra Academy

Statična prezentacija za Black Cobra Academy.

## Postavljanje na server

Iz glavnog foldera projekta kopirati početnu stranicu i folder sa slikama:

```bash
mkdir -p /home/krle/html/blackcobraacademy
cp -r index.html slike 'Rekreativna setnja' /home/krle/html/blackcobraacademy/
# Ako se kopiraju samo izmene za Zumba sekciju:
cp -r slike/Zumba /home/krle/html/blackcobraacademy/slike/
ovo je glavno
cp index.html /home/krle/html/blackcobraacademy/index.html
```
citanje metrike, vaznoo!!!
curl -s http://localhost:9105/metrics | grep blackcobraacademy

Nakon kopiranja struktura na serveru treba da bude:

```text
/home/krle/html/blackcobraacademy/
├── index.html
└── slike/
    ├── pocetak/
    │   └── fotografije
    └── Zumba/
        ├── fotografije
        └── video-snimci
```

Folder `slike/Zumba` je obavezan jer ga koristi nova Zumba sekcija na stranici.

U Nginx konfiguraciji postaviti root folder sajta:

```nginx
server {
    listen 80;
    server_name blackcobraacademy.com www.blackcobraacademy.com;

    root /home/krle/html/blackcobraacademy;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Zatim proveriti i učitati Nginx konfiguraciju:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

Ne prebacivati `.git` folder ni interni fajl `Za sajt osnovni podaci.txt`.
