# LDAP

LDAP è un protocollo applicativo che consente di gestire in modo centralizzato l’autenticazione di persone, macchine e software. Indirettamente, consente anche di effettuare l’autorizzazione.

LDAP viene tipicamente utilizzato come **fonte unica di verità** per identità e gruppi all’interno di un’organizzazione.


## Concetti fondamentali

LDAP organizza i dati in una **struttura gerarchica ad albero**, detta Directory Information Tree (DIT).

Ogni elemento della directory è chiamato **oggetto LDAP**.


## Distinguished Name (DN)

Ogni oggetto LDAP è identificato in modo univoco da un **Distinguished Name (DN)**.

Il DN rappresenta il **percorso completo** dell’oggetto all’interno dell’albero LDAP ed è composto dalla concatenazione dei nomi dei nodi, dal più specifico fino alla radice.

Esempio:


```bash
ou=Octopus,dc=example,dc=com
```


## Tipologie di oggetti

Gli oggetti LDAP si suddividono in due grandi categorie:

### Nodi intermedi

Sono oggetti **contenitore**, utilizzati esclusivamente per organizzare la gerarchia della directory. Non rappresentano dati di business.

Esempi tipici:
- unità organizzative
- contenitori logici

### Nodi foglia

Sono oggetti che **contengono dati effettivi**, come:
- utenti
- gruppi
- account di servizio


## Namespace e radice della directory

La base della gerarchia LDAP è definita dai **Domain Component (dc)**, che rappresentano il dominio DNS dell’organizzazione.

Esempio:

```bash
example.com → dc=example,dc=com
```


Questa parte definisce il **namespace globale** della directory.


## Radice applicativa

All’interno del namespace globale viene definita una **radice applicativa**, che rappresenta il punto di ingresso logico per tutti gli oggetti aziendali.

Esempio:

```bash
dn: ou=Octopus,dc=example,dc=com
objectClass: organizationalUnit
ou: Octopus
```

## Struttura tipica

A partire dalla radice applicativa, la directory viene organizzata in modo gerarchico:

```
dc=example,dc=com
└── ou=Octopus
    ├── ou=users
    ├── ou=groups
    └── ou=services
```


Ogni oggetto LDAP avrà un DN che riflette esattamente la sua posizione all’interno di questa struttura.

## Nodi foglia

In una directory LDAP, i nodi foglia sono tipicamente **utenti** o **account**, e costituiscono le **identità effettive** gestite dal sistema, come ad esempio:

```
dn: uid=user01,ou=users,ou=Octopus,dc=example,dc=com
objectClass: inetOrgPerson
cn: User 01
sn: User01
uid: user01
userPassword: password

dn: uid=user02,ou=users,ou=Octopus,dc=example,dc=com
objectClass: inetOrgPerson
cn: User 02
sn: User02
uid: user02
userPassword: password
```