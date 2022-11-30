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

# Peatükk 3

IPv4 on 32 bitine aadress. IPv4 võib olla eri protokolli või näiteks sisemise eravõrgu aaddress, või address mida kasutatakse testimiseks või dokumenteerimiseks. Iga IPv4 addressi numbritest tähistab 1 oktetti. Address on punktidega eraldatud ainult et oleks inimestel lihtsam lugeda. 

IPv4 aadresse on maailmas üle miljardi. Võrk millel on 22 biti võrgu osa ning 10 biti hosti osa on /22 võrk. Igal serveril/hostil peab olema eraldiseisev IP aadress ning IPv4 addresse on maailmas vähem kui inimesi. 
IP address ei kuulu mitte masinale/arvutile, vaid liidesele, nt etherneti või loopback liidesele. 
Loopback liidese IP aaddress on peaaegu alati 127.0.0.1 hosti nimega localhost. 

Ruuter ühendab 2 erinevat IP võrku, käitudes kui värav. Igale majapidamisele on eraldatud 1 avalik IP aadress, mis jaotab isiklikud IP aadressid seadmetele mis võrguga ühendavad. 

Privaatseid IP aadresse tõlgendatakse avalikeks kasutades NAT - network address translation. Privaatne  IP tähendab, et seda saab kasutada ainult kohalikus võrgus. 

IP aadressite nappuse probleemi lahendab IPv6, mille aadress on märgatavalt pigem kui IPv4 - 16 oktetti. 

# Peatükk 4

Protokollid on kihilised ning iga kiht sõltub alusmisest kui mitte ülemisest. Kihid sama keelt ei mõista ning suhtlevad baitide edastamise teel. 

Flag on boolean, true või false:
The six basic TCP flags
The original TCP packet format has six flags. Two more optional flags have since been standardized, but they are much less important to the basic functioning of TCP. For each packet, tcpdump will show you which flags are set on that packet.

SYN (synchronize) [S] — This packet is opening a new TCP session and contains a new initial sequence number.
FIN (finish) [F] — This packet is used to close a TCP session normally. The sender is saying that they are finished sending, but they can still receive data from the other endpoint.
PSH (push) [P] — This packet is the end of a chunk of application data, such as an HTTP request.
RST (reset) [R] — This packet is a TCP error message; the sender has a problem and wants to reset (abandon) the session.
ACK (acknowledge) [.] — This packet acknowledges that its sender has received data from the other endpoint. Almost every packet except the first SYN will have the ACK flag set.
URG (urgent) [U] — This packet contains data that needs to be delivered to the application out-of-order. Not used in HTTP or most other current applications.

Andmepakettide0 kaotus saatmise ajal toimub enamasti vahevõrgu kiiruse (või selle puudumise tõttu). 

# Peatükk 5

Ping mõõdab roundtripi aega kuna ta ei tea millal ping jõuab sihtkohani, aga ta teab millal ta vastuse vastu saab. 
Et vältida igavesti ringiliikumist ruuterite vahel, tänu ruuteri rikkele, on igal andmepaketil TTL, ehk time to live. Iga kord kui ta liigub ruuterist läbi, väheneb TTL 1 võrra. Kui pakett peaks jääma ruuterite vahele ringi tiirlema, pakett aegub. 

Kiirus oleneb kas bandwidthi kiirusest või latencyst. Bandwidth oleneb otseselt kasutaja internetikiirusest, latency aga sellest kui mitme serveriga peab päring kontakti looma. 

Tulemüür filtreerib sissetulevaid päringuid ja andmepakette, võrguliiklust. Tulemüüre saab ka kasutada veebilehtedede või nende sisu blokeerimiseks või tsenseerimiseks. 
