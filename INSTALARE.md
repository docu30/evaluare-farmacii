# Instalarea aplicației pe tabletă

Aplicația **Evaluare Farmacii** nu vine din Magazin Play. Instalarea are doi pași:

1. **Publici aplicația pe internet**, la o adresă `https`. Faci asta o singură dată, de pe calculator.
2. **Instalezi aplicația din Chrome** pe fiecare tabletă.

---

## Pasul 1 – Publicarea aplicației (o singură dată, de pe calculator)

Adresa trebuie să fie **https**. Altfel Chrome nu permite instalarea, iar backup-ul în Google Drive nu funcționează. Varianta recomandată este **GitHub Pages**: e gratuit, adresa e stabilă și actualizările sunt simple.

### 1.1 Cont GitHub
Îți faci un cont gratuit pe https://github.com.

### 1.2 Creezi un depozit (repository)
1. Sus în dreapta: **＋ → New repository**.
2. Repository name: `evaluare-farmacii`
3. Tip: **Public**.
4. Apeși **Create repository**.

### 1.3 Urci fișierele aplicației
1. În pagina depozitului apeși **Add file → Upload files** (sau linkul *uploading an existing file*).
2. Tragi în pagină aceste 6 fișiere:
   - `index.html`
   - `sw.js`
   - `manifest.json`
   - `icon-192.png`
   - `icon-512.png`
   - `logo-catena.png`

   Fișierele `.md` (ghidurile) și folderul `docs` **nu** sunt necesare.
3. Jos apeși **Commit changes**.

### 1.4 Activezi GitHub Pages
1. În depozit: **Settings → Pages**.
2. La **Build and deployment → Source** alegi **Deploy from a branch**.
3. La **Branch** alegi `main` și folderul `/ (root)`, apoi apeși **Save**.
4. După 1-2 minute, în aceeași pagină apare adresa aplicației:

   ```
   https://numele-tau.github.io/evaluare-farmacii/
   ```

   (`numele-tau` este numele tău de utilizator GitHub.)

5. Deschide adresa pe calculator ca să verifici că aplicația se încarcă.

> 💡 Pentru configurarea Google Drive (vezi `CONFIGURARE-GOOGLE-DRIVE.md`), la *Authorized JavaScript origins* treci **doar domeniul**: `https://numele-tau.github.io`

---

## Pasul 2 – Instalarea pe tabletă (pe fiecare tabletă)

1. Tableta trebuie să fie conectată la internet.
2. Deschide **Chrome** și scrie adresa aplicației:
   `https://numele-tau.github.io/evaluare-farmacii/`
3. Apasă meniul **⋮** din dreapta sus.
4. Alege **Instalează aplicația**. Pe unele versiuni opțiunea apare ca **Adaugă pe ecranul de pornire**, urmată de **Instalează**.
5. Confirmă. Pe ecranul tabletei apare iconița **Evaluări**.

De acum:
- aplicația se deschide **din iconiță**, pe tot ecranul, ca o aplicație obișnuită;
- funcționează și **fără internet**. Internetul e necesar doar la prima deschidere, la actualizări și pentru backup-ul în Drive.

> 💡 Ca să nu tastezi adresa pe tabletă, trimite-o evaluatorului pe email sau WhatsApp. Persoana apasă pe link, apoi urmează pașii 3–5.

---

## Actualizarea aplicației

Când primești o versiune nouă a fișierelor:

1. Pe GitHub, în depozit: **Add file → Upload files**, tragi fișierele modificate (de obicei `index.html` și `sw.js`), apoi **Commit changes**. Fișierele vechi se înlocuiesc automat.
2. Aștepți 1-2 minute.
3. Pe tabletă, cu internet: închizi aplicația complet (din lista de aplicații recente) și o redeschizi. Versiunea nouă se încarcă singură.

**Datele (farmacii, evaluări) rămân neatinse la actualizare.**

---

## Backup-ul datelor

Datele stau pe tabletă. Un backup este un fișier `.json` cu toate farmaciile, angajații, criteriile și evaluările.

- **La „Finalizează evaluarea” nu se descarcă nimic pe tabletă.**
- **Google Drive:** dacă e configurat (vezi `CONFIGURARE-GOOGLE-DRIVE.md`), la fiecare evaluare finalizată se face automat un backup în Drive, în folderul „Evaluare Farmacii - backup”.
- **Mementoul:** pe ecranul **Evaluări** apare o casetă portocalie, **„⚠ E timpul pentru un backup”**, când:
  - nu s-a făcut încă niciun backup, sau
  - sunt **3 sau mai multe evaluări** fără backup, sau
  - ultimul backup e mai vechi de **7 zile** și între timp s-au făcut evaluări.
- **Ce faci când apare:** apeși **⬇ Descarcă backup acum**. Fișierul ajunge în **Descărcări** pe tabletă, iar caseta dispare. **Mai târziu** o ascunde până la următoarea deschidere a aplicației.
- **Oricând:** backup manual din *Setări → Backup date*, cu **⬇ Descarcă backup pe tabletă** sau **☁ Backup în Google Drive**. Tot acolo vezi data ultimului backup.

> 💡 Fișierele din Descărcări se pierd dacă tableta se strică sau e resetată. Din când în când, copiază ultimul backup și în altă parte: email, Drive sau calculator.

---

## De reținut

- ⚠️ **Nu schimba adresa aplicației după ce începi să lucrezi.** Datele sunt legate de adresă: o adresă nouă înseamnă o aplicație goală. Datele vechi se pot recupera doar din backup (*Setări → Importă backup*).
- ⚠️ **Nu dezinstala aplicația și nu șterge datele Chrome** fără un backup recent. Datele de pe tabletă s-ar pierde.
- **Nu deschide `index.html` direct ca fișier** pe tabletă (de exemplu din Descărcări sau dintr-un email). Așa nu se poate instala, nu merge offline și nu merge nici backup-ul în Drive.
- **Tabletă nouă sau a doua tabletă:** faci doar Pasul 2, cu aceeași adresă. Pentru a muta datele de pe o tabletă veche, importă ultimul backup: *Setări → Importă backup*.
- Depozitul fiind public, oricine poate vedea **codul** aplicației. **Datele evaluărilor nu ajung pe GitHub**, ele rămân doar pe tablete și în Google Drive.

---

## Probleme frecvente

| Problemă | Rezolvare |
|---|---|
| Nu apare „Instalează aplicația” în meniul Chrome | Verifică adresa: trebuie să înceapă cu `https://`. Reîncarcă pagina și așteaptă câteva secunde. Poți folosi și „Adaugă pe ecranul de pornire”. |
| Pagina GitHub arată „404” | GitHub Pages nu e încă activ (așteaptă câteva minute) sau `index.html` nu e în rădăcina depozitului. |
| După actualizare, pe tabletă apare încă varianta veche | Închide aplicația complet și redeschide-o cu internet. Dacă nu ajută, repetă o dată. |
| Apare mereu „E timpul pentru un backup” | Apasă „Descarcă backup acum”. Caseta dispare după backup și revine doar după alte 3 evaluări sau după 7 zile. |
| Aplicația s-a deschis „goală”, fără date | Probabil a fost deschisă de la altă adresă sau datele Chrome au fost șterse. Importă ultimul backup: *Setări → Importă backup*. |
