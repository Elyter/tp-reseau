# TP1 - Premier pas réseau

# I. Exploration locale en solo

## 1. Affichage d'informations sur la pile TCP/IP locale

### En ligne de commande

**🌞 Affichez les infos des cartes réseau de votre PC**

```
❯ ifconfig
en0:
	ether 80:65:7c:e1:98:31 
	inet 10.33.17.16 netmask 0xfffffc00 broadcast 10.33.19.255
```

Aucune interface ethernet

**🌞 Affichez votre gateway**

```
❯ route -n get default
    gateway: 10.33.19.254
  interface: en0
```

**🌞 Déterminer la MAC de la passerelle**

```
❯ arp -a
? (10.33.19.254) at 0:c0:e7:e0:4:4e on en0 ifscope [ethernet]
```

### En graphique (GUI : Graphical User Interface)

**🌞 Trouvez comment afficher les informations sur une carte IP (change selon l'OS)**

```
Préférence system -> Reseau -> avancé -> TCP/IP
```

## 2. Modifications des informations

### A. Modification d'adresse IP (part 1)  

🌞 Utilisez l'interface graphique de votre OS pour **changer d'adresse IP** :

```
Préférence system -> Reseau -> avancé -> TCP/IP -> Configurer IPV4: manuellement -> Modifier l'adresse IPV4
```

🌞 **Il est possible que vous perdiez l'accès internet.** Que ce soit le cas ou non, expliquez pourquoi c'est possible de perdre son accès internet en faisant cette opération.

Il est possible de perde l'accés à intrenet si on utilise une IP déjà utilisé par quelqu'un d'autre.

# II. Exploration locale en duo ()
## 3. Modification d'adresse IP

🌞 **Modifiez l'IP des deux machines pour qu'elles soient dans le même réseau**
```
Adresse IPv4. . . . . . . . . . . . . .: 10.10.10.225(en double)
Masque de sous-réseau. . . . . . . . . : 255.255.255.0
```
🌞 **Vérifier à l'aide d'une commande que votre IP a bien été changée**
```
ipconfig /all
```

🌞 **Vérifier que les deux machines se joignent**
```
ping 10.10.10.213

Envoi d’une requête 'Ping'  10.10.10.213 avec 32 octets de données :
Réponse de 10.10.10.213 : octets=32 temps=1 ms TTL=128
Réponse de 10.10.10.213 : octets=32 temps=1 ms TTL=128
Réponse de 10.10.10.213 : octets=32 temps=3 ms TTL=128
Réponse de 10.10.10.213 : octets=32 temps=1 ms TTL=128
```

🌞 **Déterminer l'adresse MAC de votre correspondant**
```
 arp -a

Interface : 10.33.19.192 --- 0xb
  Adresse Internet      Adresse physique      Type
  10.33.17.98           24-ee-9a-5a-77-60     dynamique
  ```

## 4. Utilisation d'un des deux comme gateway

🌞**Tester l'accès internet**

```
Statistiques Ping pour 1.1.1.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%)
 ```

🌞 **Prouver que la connexion Internet passe bien par l'autre PC**
```
PS C:\Users\cedri> tracert 1.1.1.1

Détermination de l’itinéraire vers one.one.one.one [1.1.1.1]
avec un maximum de 30 sauts :

  1     1 ms     *        1 ms  LAPTOP-B0TVBCEU.mshome.net [192.168.137.1]
  2     *        *        *     Délai d’attente de la demande dépassé.
  3     7 ms     6 ms     6 ms  10.33.19.254
  4     2 ms     7 ms     8 ms  137.149.196.77.rev.sfr.net [77.196.149.137]
  5    14 ms    13 ms     9 ms  108.97.30.212.rev.sfr.net [212.30.97.108]
  6    22 ms    22 ms    22 ms  222.172.136.77.rev.sfr.net [77.136.172.222]
  7    21 ms    20 ms    28 ms  221.172.136.77.rev.sfr.net [77.136.172.221]
  8    22 ms    23 ms    22 ms  221.10.136.77.rev.sfr.net [77.136.10.221]
  9    24 ms    23 ms    21 ms  221.10.136.77.rev.sfr.net [77.136.10.221]
 10    27 ms    24 ms    49 ms  141.101.67.254
 11    23 ms    23 ms    26 ms  172.71.132.2
 12    24 ms    22 ms    22 ms  one.one.one.one [1.1.1.1]
```
## 5. Petit chat privé

🌞 **sur le PC *serveur*** 
```
ping 10.10.10.210

        Envoi d’une requête 'Ping'  10.10.10.210 avec 32 octets de données :
        Réponse de 10.10.10.210 : octets=32 temps<1ms TTL=128
        Réponse de 10.10.10.210 : octets=32 temps<1ms TTL=128
        Réponse de 10.10.10.210 : octets=32 temps<1ms TTL=128
        Réponse de 10.10.10.210 : octets=32 temps<1ms TTL=128

        Statistiques Ping pour 10.10.10.210:
        Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
        Durée approximative des boucles en millisecondes :
        Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
        PS C:\Users\pc\Downloads\netcat-1.11> .\nc.exe -l -p 8888
        mec
        ftg
        tg
        bouffon
        fdp
        chu mort ca marche
        c bi1
        
```
🌞 **sur le PC *client*** 

```
ping 10.10.10.213

Envoi d’une requête 'Ping'  10.10.10.213 avec 32 octets de données :
Réponse de 10.10.10.213 : octets=32 temps<1ms TTL=128
Réponse de 10.10.10.213 : octets=32 temps<1ms TTL=128
Réponse de 10.10.10.213 : octets=32 temps<1ms TTL=128
Réponse de 10.10.10.213 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 10.10.10.213:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
PS C:\Users\cedri\Desktop\netcat-1.11> ^C
PS C:\Users\cedri\Desktop\netcat-1.11> .\nc.exe 10.10.10.213 8888
ftg
mec
tg
bouffon
fdp
chu mort ca marche
c bi1
```

🌞 **Visualiser la connexion en cours**
```
netstat -a -n -b
TCP    10.10.10.210:54361     10.10.10.225:8888      ESTABLISHED
 [nc.exe]
 ```
🌞 **Pour aller un peu plus loin**

- si vous faites un `netstat` sur le serveur AVANT que le client `netcat` se connecte, vous devriez observer que votre serveur `netcat` écoute sur toutes vos interfaces
  - c'est à dire qu'on peut s'y connecter depuis la wifi par exemple :D
```
   netstat -a -n -b | select-string 8888

  TCP    0.0.0.0:8888           0.0.0.0:0       LISTENING

```

- il est possible d'indiquer à `netcat` une interface précise sur laquelle écouter
  - par exemple, on écoute sur l'interface Ethernet, mais pas sur la WiFI
```
  .\nc.exe -l -p 8888 -s 10.10.10.225

```

```
netstat -a -n -b | select-string 8888

  TCP    10.10.10.225:8888      0.0.0.0:0              LISTENING
```



## 6. Firewall

🌞 **Activez et configurez votre firewall**
```
Il faut ouvrir Pare-feu Windows Defender avec fonctions avancés de sécurité puis cliquer sur règles de trafic entrant, séléctionner Partage de fichier et d'imprimantes (Demande d'écho - Trafic entrant ICMPv4) et clique droit dessus et activer la règle
```
  
# III. Manipulations d'autres outils/protocoles côté client

## 1. DHCP

🌞**Exploration du DHCP, depuis votre PC**
```
PS C:\Users\Guillaume> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Killer(R) Wi-Fi 6 AX1650i 160MHz Wireless Network Adapter (201NGW)
   Adresse physique . . . . . . . . . . . : 4C-03-4F-E9-73-F7
   DHCP activé. . . . . . . . . . . . . . : Oui <---- 
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::b980:3214:57b0:7a1d%6(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.16.226(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.252.0
   Bail obtenu. . . . . . . . . . . . . . : mercredi 5 octobre 2022 09:05:38 <----------
   Bail expirant. . . . . . . . . . . . . : jeudi 6 octobre 2022 09:05:38 <----------
   Passerelle par défaut. . . . . . . . . : 10.33.19.254
   Serveur DHCP . . . . . . . . . . . . . : 10.33.19.254 <----------
   IAID DHCPv6 . . . . . . . . . . . : 88867663
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-29-C3-B8-56-08-8F-C3-51-69-8E
```
🌞** Trouver l'adresse IP du serveur DNS que connaît votre ordinateur**
```
PS C:\Users\cedric> ipconfig /all

   Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                       8.8.4.4
                                       1.1.1.1
````
🌞 Utiliser, en ligne de commande l'outil `nslookup` (Windows, MacOS) ou `dig` (GNU/Linux, MacOS) pour faire des requêtes DNS à la main
```
PS C:\Users\cedric> nslookup google.com
Serveur :   dns.google
Address:  8.8.8.8  <---- requête à cette adresse

Réponse ne faisant pas autorité :
Nom :    google.com
Addresses:  2a00:1450:4007:819::200e
          142.250.178.142
```
```
PS C:\Users\cedric> nslookup ynov.com
Serveur :   dns.google
Address:  8.8.8.8 <---- requête à cette adresse
Réponse ne faisant pas autorité :
Nom :    ynov.com
Addresses:  2606:4700:20::681a:ae9
          2606:4700:20::681a:be9
          2606:4700:20::ac43:4ae2
          172.67.74.226
          104.26.11.233
          104.26.10.233
```
Les deux utilises le même DNS, celui de google.

```
PS C:\Users\cedric> nslookup.exe 231.34.113.12
Serveur :   dns.google
Address:  8.8.8.8

*** dns.google ne parvient pas à trouver 231.34.113.12 : Non-existent domain

PS C:\Users\cedric> nslookup.exe 78.34.2.17
Serveur :   dns.google
Address:  8.8.8.8

Nom :    cable-78-34-2-17.nc.de <---- Domaine
Address:  78.34.2.17

```
```
Ici seulement une des deux adresses existes sur la première on voit que le premier n'a pas de domaine, `231.34.113.12 ` n'est donc pas présent dans le DNS de google.
```
