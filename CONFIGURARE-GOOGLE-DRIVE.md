# Configurare backup în Google Drive

Butonul **☁ Backup în Google Drive** (Setări → Backup date) are nevoie de un **ID de client OAuth** de la Google. Îl creezi o singură dată, în aproximativ 10 minute, cu contul tău Google.

Până când completezi ID-ul, backup-ul în Drive nu se face. Backup-ul local se face din butonul „Descarcă backup” (din Setări sau din mementoul de pe ecranul Evaluări). Restul aplicației funcționează normal.

## Cine face acești pași?

**Doar tu, o singură dată, de pe calculator.** ID-ul de client aparține aplicației, nu tabletei și nici utilizatorului. Toate tabletele care deschid aplicația de la aceeași adresă folosesc același ID.

Pe tableta unui alt evaluator **nu trebuie configurat nimic**. La prima evaluare finalizată (sau la primul „Backup în Google Drive”) apare fereastra Google: persoana își alege contul și apasă **Continuă / Permite**. Backup-urile ajung apoi în **Drive-ul ei**, nu în al tău.

Singura condiție: la Pasul 3 alege **Publish app**. Altfel trebuie să adaugi manual adresa Gmail a fiecărui evaluator la *Test users*.

---

## Ce îți trebuie înainte

- Un cont Google (poate fi chiar al evaluatorului).
- **Adresa exactă** de unde se deschide aplicația pe tabletă, de exemplu `https://numele-tau.github.io/evaluare-farmacii/`. Din ea îți trebuie doar **domeniul**: `https://numele-tau.github.io`.
  - Aplicația trebuie să fie servită prin **https**. Autentificarea Google nu funcționează pe `http` (excepție: `localhost`, pentru teste pe calculator).
- (Doar dacă nu publici aplicația la Pasul 3.6) Adresele Gmail ale evaluatorilor.

---

## Pasul 1 – Creează un proiect Google Cloud

1. Intră pe https://console.cloud.google.com
2. Sus, lângă logo, apasă selectorul de proiecte, apoi **New Project**.
3. Nume: `Evaluare Farmacii`. Apasă **Create**.
4. Verifică faptul că proiectul nou este selectat sus.

## Pasul 2 – Activează Google Drive API

1. Meniu (☰) → **APIs & Services → Library**.
2. Caută **Google Drive API**.
3. Deschide-l și apasă **Enable**.

## Pasul 3 – Ecranul de consimțământ (OAuth consent screen)

Meniu (☰) → **APIs & Services → OAuth consent screen**. În versiunile noi ale consolei se numește **Google Auth Platform**. Dacă îți cere, apasă **Get started**.

1. **App information**
   - App name: `Evaluare Farmacii`
   - User support email: adresa ta
2. **Audience**: alege **External**.
3. **Contact information**: adresa ta de email.
4. Acceptă termenii și apasă **Create**.
5. La **Audience → Test users**, apasă **Add users** și adaugă adresa Gmail a evaluatorului (și pe a ta, dacă vrei să testezi).
6. **(Recomandat, mai ales pentru mai mulți evaluatori)** Tot la **Audience**, apasă **Publish app**.
   - Aplicația folosește doar permisiunea `drive.file`, care vede **numai fișierele create de aplicație**, nu restul Drive-ului. Google o consideră nesensibilă, așa că nu cere verificarea aplicației.
   - Dacă nu publici, aplicația rămâne în modul „Testing” și funcționează doar pentru adresele adăugate la *Test users*.

## Pasul 4 – Creează ID-ul de client

1. Meniu (☰) → **APIs & Services → Credentials**. Poți ajunge și din **Google Auth Platform → Clients**.
2. **Create credentials → OAuth client ID**.
3. Application type: **Web application**.
4. Name: `Evaluare Farmacii – tabletă`.
5. La **Authorized JavaScript origins**, apasă **Add URI** și scrie domeniul aplicației:
   - `https://numele-tau.github.io` (**doar domeniul**: fără cale, fără `/` la final)
   - (opțional, pentru teste pe calculator) `http://localhost:8000`
6. Lasă **Authorized redirect URIs** gol.
7. Apasă **Create**.
8. Copiază **Client ID**. Arată așa: `123456789012-abcdefg....apps.googleusercontent.com`.
   - *Client secret* **nu** este necesar și nu se pune în aplicație.

## Pasul 5 – Pune ID-ul în aplicație

1. Deschide `index.html` și caută linia:
   ```js
   const GOOGLE_CLIENT_ID = "";
   ```
2. Pune ID-ul între ghilimele:
   ```js
   const GOOGLE_CLIENT_ID = "123456789012-abcdefg....apps.googleusercontent.com";
   ```
3. Salvează și urcă din nou fișierele pe server (`index.html` și `sw.js`).

## Pasul 6 – Testează pe tabletă

Backup-ul în Drive se face automat la **Finalizează evaluarea**. Copia locală (în Descărcări) nu se mai descarcă automat: o faci din Setări sau din mementoul de pe ecranul Evaluări. Butonul „Backup în Google Drive” din Setări rămâne disponibil pentru un backup manual.


1. Deschide aplicația pe tabletă, cu internet. Dacă vezi încă varianta veche, închide aplicația complet și redeschide-o.
2. **Setări → ☁ Backup în Google Drive**.
3. Prima dată apare fereastra Google: alege contul evaluatorului și aprobă accesul.
   - Dacă apare *„Google hasn't verified this app”*, apasă **Continue**. Mesajul e normal cât aplicația e în modul Testing.
4. Trebuie să apară mesajul **„Backup salvat în Google Drive”**, iar sub butoane data ultimului backup.
5. Verifică în Google Drive: folderul **„Evaluare Farmacii - backup”** trebuie să conțină fișierul `backup_evaluari_farmacii_AAAA-LL-ZZ.json`.

---

## Probleme frecvente

| Mesaj / simptom | Cauză probabilă | Rezolvare |
|---|---|---|
| „Backup-ul în Drive nu este configurat” | `GOOGLE_CLIENT_ID` e gol sau aplicația de pe tabletă e varianta veche | Verifică Pasul 5, urcă fișierele, redeschide aplicația |
| „Nu există conexiune la Google” | Tableta nu are internet | Conectează tableta la internet și reîncearcă |
| Eroare Google `redirect_uri_mismatch` / `origin_mismatch` | Domeniul din *Authorized JavaScript origins* nu corespunde exact | Adaugă domeniul exact din bara de adrese (cu `https://`, fără `/` la final) |
| Eroare `access_denied` / „app is blocked” | Contul nu este în *Test users*, iar aplicația nu e publicată | Pasul 3.5 sau 3.6 |
| „Eroare Google Drive (403)” | Google Drive API nu este activat | Pasul 2 |
| „Autentificare anulată” | Fereastra Google a fost închisă | Apasă din nou butonul |
| În Setări apare „⚠ Ultimul backup în Drive nu a reușit” | Evaluarea a fost finalizată fără internet sau fereastra Google a fost blocată | Datele sunt în siguranță pe tabletă. Când ai internet, apasă „Backup în Google Drive” |

## Restaurare din backup

**Setări → ⬆ Importă backup**, apoi alege **Drive** în selectorul de fișiere de pe Android, intră în folderul **„Evaluare Farmacii - backup”** și alege fișierul dorit.

⚠️ Importul **înlocuiește** toate datele de pe tabletă cu cele din fișier.
