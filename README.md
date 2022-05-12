# ACL
Découverte des Access Control List

### Qu'est-ce qu'une ACL?
Une ACL est une liste de règles permettant de filtrer ou d’autoriser du trafic sur un réseau en fonction de certains critères (IP source, IP destination, port source, port destination, protocole, …).

### Caractéristiques d'une ACL
* Une ACL permet de soit autoriser du trafic (permit) ou de le bloquer (deny).
* Il est possible d’appliquer au maximum une ACL par interface et par sens (input/output).
* Une ACL est analysée par l’IOS de manière séquentielle de haut en bas.
* Dès qu’une règle correspond au trafic, l’action définie est appliquée, le reste de l’ACL n’est pas analysé.
* Toute ACL par défaut bloque tout trafic. Donc tout trafic ne correspondant à aucune règle d’une ACL est rejeté.
* Une ACL peux être nommées, elle sera identifiée par un nom sous la forme d’une chaîne de caractères alphanumériques.

## ACL standard et ACL étendues
### ACL standard
Une ACL standard permet d’analyser du trafic en fonction de:
* Adresse IP source

#### Numérotation d'ACL standard 
* 1 à 99 : ACL Standard
* 1300 à 1999 : ACL Standard

### Configuration d’une ACL numérique standard
```
R1(config)#access-list 1 permit 192.168.0.0 0.0.0.255
R1(config)#access-list 1 permit 192.168.1.0 0.0.0.255
R1(config)#access-list 1 deny 192.168.0.0 0.0.3.255
R1(config)#access-list 1 permit any
```

### Configuration d’une ACL nommée standard
```
R1(config)#ip access-list standard monACL
R1(config-std-nacl)#permit 192.168.0.0 0.0.0.255
R1(config-std-nacl)#permit 192.168.1.0 0.0.0.255
R1(config-std-nacl)#deny 192.168.0.0 0.0.3.255
R1(config-std-nacl)#permit any
R1(config-std-nacl)#exit
```

### ACL étendues
Une ACL étendue permet d’analyser du trafic en fonction de:
* Adresse IP source
* Adresse IP destination
* Protocole (tcp, udp, icmp, …)
* Port source
* Port destination · Etc.

#### Numérotation d'ACL standard 
* 100 à 199 : ACL Etendue
* 2000 à 2699 : ACL Etendue

### Configuration d’une ACL numérique étendue
```
R1(config)#access-list 100 permit tcp any host 192.168.1.100 eq 80
R1(config)#access-list 100 permit icmp 192.168.0.0 0.0.0.255 host 192.168.1.100
```

### Configuration d’une ACL nommée étendue
```
R1(config)#ip access-list extended monACLextended
R1(config-ext-nacl)#permit tcp any host 192.168.1.100 eq 80
R1(config-ext-nacl)#permit icmp 192.168.0.0 0.0.0.255 host 192.168.1.100
R1(config-ext-nacl)#exit
```

## Directives de configuration d'ACL
* Une seule ACL par interface, par protocole, par direction est autorisé.
* Les listes de contrôle d'accès sont traitées de haut en bas ; les déclarations les plus spécifiques doivent figurer en haut de la liste. Une fois qu'un paquet répond aux critères ACL, le traitement ACL s'arrête et le paquet est autorisé ou refusé.
* Les ACL sont créés globalement puis appliquées aux interfaces.
* Une ACL peut filtrer le trafic passant par le routeur, ou le trafic vers et depuis le routeur.


## Vérification des ACLs
```
R1#show access-lists
Standard IP access list 1
10 permit 192.168.0.0, wildcard bits 0.0.0.255
20 permit 192.168.1.0, wildcard bits 0.0.0.255
30 deny 192.168.0.0, wildcard bits 0.0.3.255
40 permit any
Standard IP access list monACL
10 permit 192.168.0.0, wildcard bits 0.0.0.255
20 permit 192.168.1.0, wildcard bits 0.0.0.255
30 deny 192.168.0.0, wildcard bits 0.0.3.255
40 permit any
R1#
```

