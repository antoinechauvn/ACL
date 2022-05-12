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


## ACL standard et ACL étendues
### ACL standard
Une ACL standard permet d’analyser du trafic en fonction de:
* Adresse IP source

#### Numérotation d'ACL standard 
* 1 à 99 : ACL Standard
* 1300 à 1999 : ACL Standard

```
access-list access-list-number {permit|deny} {host|source source-wildcard|any}
```
*Note: Dans toutes les versions de logiciel, access-list-number peut être compris entre 1 et 99*

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

## Directives de configuration d'ACL
* Une seule ACL par interface, par protocole, par direction est autorisé.
* Les listes de contrôle d'accès sont traitées de haut en bas ; les déclarations les plus spécifiques doivent figurer en haut de la liste. Une fois qu'un paquet répond aux critères ACL, le traitement ACL s'arrête et le paquet est autorisé ou refusé.
* Les ACL sont créés globalement puis appliquées aux interfaces.
* Une ACL peut filtrer le trafic passant par le routeur, ou le trafic vers et depuis le routeur.
