

````md
# Auto Deploy Website via Git Push

Dette prosjektet lar deg enkelt publisere nettsider ved å pushe til en Git-repo på serveren. Når du pusher, sjekkes koden automatisk ut til webroot-mappen din og publiseres uten behov for FTP.

---

## Setup Guide

### 1. Opprett en Bare Git Repo på Serveren

Logg inn på serveren din og kjør:

```bash
mkdir -p ~/git/mywebsite.git
cd ~/git/mywebsite.git
git init --bare
````

Dette oppretter et “tomt” repo som fungerer som endepunkt for push.

---

### 2. Lag et Post-Receive Hook for Automatisk Deploy

Opprett filen `hooks/post-receive` i `mywebsite.git`-mappen med følgende innhold:

```bash
#!/bin/bash
GIT_WORK_TREE=/var/www/mywebsite git checkout -f
```

* Endre `/var/www/mywebsite` til din publiseringsmappe.
* Gi skriptet kjørbar tillatelse:

```bash
chmod +x ~/git/mywebsite.git/hooks/post-receive
```

---

### 3. Legg til Remote på Lokal Maskin

På din lokale maskin, i prosjektmappen, kjør:

```bash
git remote add live ssh://user@yourserver.com/home/user/git/mywebsite.git
```

Bytt ut `user`, `yourserver.com` og path med din info.

---

### 4. Pushe og Publisere

Push koden til serveren med:

```bash
git push live main
```

Etter push vil nettsiden automatisk oppdateres i publiseringsmappen.

---

### 5. (Valgfritt) SSH-nøkler for Passordfri Push

* Generer SSH-nøkkel hvis du ikke har en:

```bash
ssh-keygen -t ed25519
```

* Kopier nøkkelen til serverens `~/.ssh/authorized_keys`:

```bash
ssh-copy-id user@yourserver.com
```

---

## Tips & Tricks

* Pass på at webserveren har lese- og skrive-tillatelse til publiseringsmappen.
* Du kan tilpasse hook-skriptet for å kjøre build-kommandoer (f.eks. `npm run build`) før deploy.
* Sørg for å sikkerhetskopiere data og konfigurasjon før du prøver!

---

## License

MIT License © William

---

Kjør på, og gjør deploy til en lek! 🚀

```

---


```
