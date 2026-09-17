# Black Cobra Academy

Statična prezentacija za Black Cobra Academy.

## Postavljanje na server

Iz glavnog foldera projekta kopirati početnu stranicu i folder sa slikama:

```bash
mkdir -p /home/krle/html/crnakobra
cp -r index.html slike 'Rekreativna setnja' /home/krle/html/blackcobraacademy/
cp -r index.html slike /home/krle/html/blackcobraacademy/

Nakon kopiranja struktura na serveru treba da bude:

```text
/home/krle/html/crnakobra/
├── index.html
└── slike/
    └── pocetak/
        └── fotografije
```

U Nginx konfiguraciji postaviti root folder sajta:

```nginx
server {
    listen 80;
    server_name blackcobraacademy.com www.blackcobraacademy.com;

    root /home/krle/html/crnakobra;
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
