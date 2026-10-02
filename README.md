# Black Cobra Academy

Statična prezentacija za Black Cobra Academy.

## Postavljanje na server

Iz glavnog foldera projekta kopirati sve HTML stranice, `robots.txt`, `sitemap.xml` i foldere sa slikama:

```bash
mkdir -p /home/krle/html/blackcobraacademy
cp -r *.html robots.txt sitemap.xml slike 'Rekreativna setnja' /home/krle/html/blackcobraacademy/
```

Ako su menjane samo stranice (bez novih slika i videa):

```bash
cp *.html robots.txt sitemap.xml /home/krle/html/blackcobraacademy/
```

Čitanje metrike (važno!):

```bash
curl -s http://localhost:9105/metrics | grep blackcobraacademy
```

Nakon kopiranja struktura na serveru treba da bude:

```text
/home/krle/html/blackcobraacademy/
├── index.html
├── zumba-u-pirotu.html, tai-bo-u-pirotu.html, pilates-u-pirotu.html, ...
├── robots.txt
├── sitemap.xml
├── Rekreativna setnja/
│   └── slike/
└── slike/
    ├── logo-black-cobra-academy.jpg
    ├── pocetak/
    ├── Zumba/
    ├── Kangoo Jumps/
    ├── Tai Bo/
    ├── Pilates/
    ├── Funkcionalni trening/
    ├── Akva/
    └── Fit Fest/
```

Kada se doda nova stranica, dodati je i u `sitemap.xml`.

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
