# av-alused
# Esimene peatükk
Ping kontrollib kas sinu arvuti suudab sellelt aadressilt vastu võtta võrguliiklust. Edukas ping tähendab, et sinu arvutil on olemas võrguühendus ning sihtserveri arvutil samuti töötab. Samuti, meie võrk suudab suhelda sihtserveri võrguga.

HTTP - printf 'HEAD / HTTP/1.1\r\nHost: en.wikipedia.org\r\n\r\n' | nc en.wikipedia.org 80 - antud käsk annab meile infot Wikipedia serveri kohta, nt serveri, cookiede ning IP aadressi kohta. 

Printf request prindib järgnevat teksti, \n kirjutab teksti järgmisele reale. 
NC ehk netcatiga saab ühendada erinevate serveritega ning see saab samuti käituda nagu server. Vertical bar käitub kui ühendi, mis suunab esimese programmi outputi järgneva programmi inputi. NC seejärel näitab käsust tulenevat informatsiooni. 

Netcat ei saada HTTPi requesti, ta ühendab portiga ning serveri jaoks tundub see kui HTTP request seega ta vastab. 

HTTP, SSH olenevad TCPst. TCP ja UDP olenevad IPst. IP omakord oleneb WiFist, ethernetist või DSList. 

Netcatiga saab serverit kuulata nc -l (serveri number). See võimaldab kuulata ühte kindlat serverit. Kasutades nc localhost (serveri number) on võimalik serveri kuulajaga suhelda (TCP puhul).

Portid 1-1023 on enamjaolt süsteemiportid, ehk sinna ei ole alati ligipääs. Ligi saab pääseda sudo commandiga. Sama porti kaks arvutit samal ajal ei saa kuulata.
Server samas saab võtta vastu rohkem kui ühte connectionit korraga, kasutades child processe et vastata kõigile connection requestidele korraga. 

Kasutades sudo lsof -i saab infot mis programmid hetkel sind kuulavad. Minu arvutil:

node      1709 anntriksden_syld   19u  IPv4  54124      0t0  TCP *:3000 (LISTEN)

sshd      1280             root    3u  IPv4  55545      0t0  TCP *:ssh (LISTEN)

sshd      1280             root    4u  IPv6  55547      0t0  TCP *:ssh (LISTEN)

theia-pro 1520             root    6u  IPv6  53865      0t0  TCP *:970 (LISTEN)

nc        5290 anntriksden_syld    3u  IPv4 295190      0t0  TCP *:100 (LISTEN)

Porti 2345 kuulamine ning URLi reale trükkimine tulemit ei anna. Samuti ei toimi printf 'HTTP/1.1 302 Moved\r\nLocation: https://www.eff.org/' | nc -l 2345 ning minu IP + 2345 trükkimine URLi reale. 

Server käsitleb korraga mitut requesti, kas poolitades ennast või luues erinevaid protsesse või threade mis käsitlevad igat sissetulevat requesti. 

# Peatükk 2

Igal IP aadress tähistab erinevat sihtkohta internetis, enamasti masinat. Igal pingil, e-mailil jne on kirjas algne IP aadres ning sihtkohta IP aadress. Host on vaid masin internetis mis võib pakkuda hostiteenust. 

ping google.com - IP 142.250.145.139. IP aadress muudetakse URLiks kasutades DNSi (domain name system). Host raamatuvahetus.ee - 94.237.33.118
dig raamatuvahetus.ee annab täpsemat informatsiooni. 

CNAME - canonical name. AAAA - iPv 6 NS - DNS name server

SSL turvaeesmärgil krüpteerib võrguliiklust et takistada teistel võrkudel privaatsetele andmetele ligipääsu. Samuti aitab see kindlaks teha, et sait millelt infot saad on tõene ning kuulub saitile millele see peaks kuuluma. 

Ipv4 koosneb 4 numbrist, eraldatud punktidega. Iga number on 8 biti, väärtusega 0-255. 
