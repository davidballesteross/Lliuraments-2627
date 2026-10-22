# Diagrama E/R del videojoc en Mermaid

En aquesta activitat explico com he fet el pas a pas del diagrama amb l'aplicació de Nermind. Al final del document hi ha el diagrama sencer.

## Pas 1. Les entitats

Primer de tot vaig mirar el document pdf de la tasca i vaig analitzar les entitats que son les següents:

- **PERSONATGE**: el protagonista, el que controla el jugador.Una cosa que vaig tenir en compte és que moltes d'aquestes relacions són de molts a molts (`posseeix`, `equipa`, les dues d'`enfronta` i `combina amb`). Al diagrama no hi ha cap problema, perquè només és el dibuix del disseny. Però la guia del professor avisa que, en una base de dades real, cada relació de molts a molts s'haurà de convertir en una taula intermèdia.

---

## Pas 9. El diagrama final

- **HABILITAT**: els poders o tècniques que poden fer servir els personatges i els enemics.
- **ENEMIC**: els rivals als quals s'enfronta el personatge.
- **MASCOTA**: l'animal que va amb el personatge.
- **ITEM**: els objectes del joc, com ara armes o armadures.
  
I l'estructura quedaria així:

```mermaid
erDiagram
    PERSONATGE
    HABILITAT
    ENEMIC
    MASCOTA
    ITEM
```

---

## Pas 2. Els atributs del personatge

Ara que ja tenia les caixes principals, tocava dir com és cadascuna: quines dades en volem guardar. Això són els atributs, i es posen dins de les claus `{}`, indicant primer el tipus de dada (text, número, etc.) i després el nom.

Ho he fet entitat per entitat. Vaig començar pel personatge i ho vaig anar construint amb aquest codi:

```mermaid
erDiagram
    PERSONATGE {
        string DNI PK
    }
```

Després hi vaig afegir la resta de dades. El nom i el cognom són text (`string`) i la vida, la força, l'agilitat i el carisma són números (`int`).

I l'estructura quedaria així:

```mermaid
erDiagram
    PERSONATGE {
        string DNI PK
        string Nom
        string Cognom
        int Vida
        int Forca
        int Agilitat
        int Carisma
    }
```

Per últim, vaig marcar què no pot quedar buit. Un personatge sense nom no té sentit, així que li vaig posar `"NOT NULL"`, que és com ho demana la guia del professor.

```mermaid
erDiagram
    PERSONATGE {
        string DNI PK
        string Nom "NOT NULL"
        string Cognom
        int Vida
        int Forca
        int Agilitat
        int Carisma
    }
```

---

## Pas 3. Els atributs de l'enemic

Després del personatge, vaig seguir amb l'enemic. Vaig tornar a mirar el PDF i l'enemic té aquestes dades: nom, codi, tipus, nivell, vida, agilitat, força i carisma.

Igual que amb el personatge, vaig començar buscant la dada que identifica cada enemic sense que es pugui repetir. Aquí no tenim un DNI, així que vaig triar el **codi**, que és un número diferent per a cada enemic. Com que és un número, el tipus és `int`, i el marco com a clau primària amb `PK`:

I la estructura quedaria aixi:

```mermaid
erDiagram
    ENEMIC {
        int Codi PK
    }
```

Després hi vaig afegir la resta de dades. El nom i el tipus d'enemic són text (`string`) i el nivell, la vida, l'agilitat, la força i el carisma són números (`int`).

I l'estructura quedaria així:

```mermaid
erDiagram
    ENEMIC {
        int Codi PK
        string Nom
        string Tipus
        int Nivell
        int Vida
        int Força
        int Agilitat
        int Carisma
    }
```

Per últim, vaig marcar què no pot quedar buit. Un enemic ha de tenir sempre nom, tipus i nivell, perquè sense aquestes dades no sabríem quin enemic és ni com de fort és. Per això els vaig posar `"NOT NULL"`:

```mermaid
erDiagram
    ENEMIC {
        int Codi PK
        string Nom "NOT NULL"
        string Tipus "NOT NULL"
        int Nivell "NOT NULL"
        int Vida
        int Força
        int Agilitat
        int Carisma
    }
```

---

## Pas 4. Els atributs de Habilitats

Ara tocava l'habilitat. Al PDF té aquestes dades: nom, codi, cost, dany, cooldown i tipus.

Com amb l'enemic, vaig començar buscant la dada que identifica cada habilitat. Tampoc no hi ha res tan únic com un DNI, així que vaig triar el **codi**, que és un número diferent per a cada habilitat. És de tipus `int` i el marco com a clau primària amb `PK`:

I la estructura quedaria aixi:

```mermaid
erDiagram
    HABILITAT {
        int Codi PK
    }
```

Després hi vaig afegir la resta de dades. El nom i el tipus d'habilitat són text (`string`) i el cost, el dany i el cooldown (el temps d'espera abans de poder tornar-la a fer servir) són números (`int`).

I l'estructura quedaria així:

```mermaid
erDiagram
    HABILITAT {
        int Codi PK
        string Nom
        int Cost
        int Dany
        int Cooldown
        string Tipus
    }
```

Per últim, vaig marcar què no pot quedar buit. Una habilitat ha de tenir sempre nom i tipus, perquè sense aquestes dues dades no sabríem com es diu ni quin tipus d'habilitat és. Per això els vaig posar `"NOT NULL"`:

```mermaid
erDiagram
    HABILITAT {
        int Codi PK
        string Nom "NOT NULL"
        int Cost
        int Dany
        int Cooldown
        string Tipus "NOT NULL"
    }
```

---

## Pas 5. Els atributs de la mascota

Ara tocava la mascota, que és la més curta. Al PDF només té tres dades: número de xip, nom i motxilla.

Per trobar la clau primària aquí ho vaig tenir fàcil. Igual que passa amb les mascotes de veritat, el **número de xip** és únic per a cada una, així que és la dada perfecta per identificar-les. Com que és més un codi que no pas un número amb què es vulgui fer operacions, el vaig posar de tipus text (`string`) i el vaig marcar amb `PK`:

```mermaid
erDiagram
    MASCOTA {
        string Num_Chip PK
    }
```

Després hi vaig afegir la resta de dades. El nom és text (`string`) i la motxilla és un número (`int`).

I l'estructura quedaria així:

```mermaid
erDiagram
    MASCOTA {
        string Num_Chip PK
        string Nom
        int Motxilla
    }
```

Per últim, vaig marcar què no pot quedar buit. Una mascota ha de tenir sempre nom, així que li vaig posar `"NOT NULL"`:

```mermaid
erDiagram
    MASCOTA {
        string Num_Chip PK
        string Nom "NOT NULL"
        int Motxilla
    }
```

---

## Pas 6. Els atributs de l'ítem

Per acabar amb els atributs, tocava l'ítem, que és el que en té més. Al PDF té aquestes dades: nom, codi, equipable, comerciable, tipus, pes, qualitat i mesures (X, Y i Z).

Com sempre, vaig començar per la clau primària. L'ítem tampoc no té res tan únic com un DNI, així que vaig triar el **codi**, que és un número diferent per a cada ítem. És de tipus `int` i el marco amb `PK`:

```mermaid
erDiagram
    ITEM {
        int Codi PK
    }
```

Després hi vaig afegir la resta de dades. El nom, el tipus i la qualitat són text (`string`). `Equipable` i `Comerciable` només poden ser sí o no, així que són de tipus `boolean`. I el pes és un número amb decimals, per això és de tipus `float`.

Les **mesures** em van fer pensar una mica més. Al PDF apareixen com una sola cosa, però en realitat són tres valors: X, Y i Z. Mermaid no té una manera de fer un atribut que es divideixi en parts, i la guia del professor diu que en aquests casos s'han de posar les parts com a atributs separats. Per això vaig crear `Mesura_X`, `Mesura_Y` i `Mesura_Z`, que també són números amb decimals (`float`).

I l'estructura quedaria així:

```mermaid
erDiagram
    ITEM {
        int Codi PK
        string Nom
        boolean Equipable
        boolean Comerciable
        string Tipus
        float Pes
        string Qualitat
        float Mesura_X
        float Mesura_Y
        float Mesura_Z
    }
```

Per últim, vaig marcar què no pot quedar buit. Un ítem ha de tenir sempre nom, tipus, qualitat, pes i les tres mesures, perquè sense aquestes dades no el podríem descriure bé. També vaig marcar `Comerciable`, perquè el joc sempre ha de saber si un objecte es pot comprar i vendre o no. Per això a tots aquests els vaig posar `"NOT NULL"`. `Equipable` el vaig deixar sense marcar:

```mermaid
erDiagram
    ITEM {
        int Codi PK
        string Nom "NOT NULL"
        boolean Equipable
        boolean Comerciable "NOT NULL"
        string Tipus "NOT NULL"
        float Pes "NOT NULL"
        string Qualitat "NOT NULL"
        float Mesura_X "NOT NULL"
        float Mesura_Y "NOT NULL"
        float Mesura_Z "NOT NULL"
    }
```

---

## Pas 7. Les entitats amb tots els atributs

Arribats aquí, ja tenia creats tots els atributs de les cinc entitats. Abans de seguir, vaig voler ajuntar-ho tot en un sol codi per veure com quedava el conjunt i comprovar que no em deixava res del PDF.

Aquest és el codi amb les cinc entitats completes, cadascuna amb la seva clau primària (`PK`), les seves dades i els atributs que no poden quedar buits (`"NOT NULL"`):

I les estructures quedarien aixi si esta tot be: 

```mermaid
erDiagram
    PERSONATGE {
        string DNI PK
        string Nom "NOT NULL"
        string Cognom
        int Vida
        int Força
        int Agilitat
        int Carisma
    }
    HABILITAT {
        int Codi PK
        string Nom "NOT NULL"
        int Cost
        int Dany
        int Cooldown
        string Tipus "NOT NULL"
    }
    ENEMIC {
        int Codi PK
        string Nom "NOT NULL"
        string Tipus "NOT NULL"
        int Nivell "NOT NULL"
        int Vida
        int Forca
        int Agilitat
        int Carisma
    }
    MASCOTA {
        string Num_Chip PK
        string Nom "NOT NULL"
        int Motxilla
    }
    ITEM {
        int Codi PK
        string Nom "NOT NULL"
        boolean Equipable
        boolean Comerciable "NOT NULL"
        string Tipus "NOT NULL"
        float Pes "NOT NULL"
        string Qualitat "NOT NULL"
        float Mesura_X "NOT NULL"
        float Mesura_Y "NOT NULL"
        float Mesura_Z "NOT NULL"
    }
```

## Pas 8. Les relacions

Ara que ja tenia les cinc entitats amb tots els seus atributs, tocava connectar-les entre elles. Això són les relacions: una línia que uneix dues entitats i que porta un verb al mig que explica què fan, com ara "equipa" o "acompanya".

El més important és la **cardinalitat**, que vol dir quants elements hi pot haver a cada costat de la línia. Es marca amb uns símbols als extrems. Els que he fet servir són aquests:

- `||` vol dir exactament un.
- `|o` vol dir zero o un.
- `}o` o `o{` vol dir zero o molts.

Per decidir-los vaig tornar a mirar el PDF, on hi havia lletres com 1, M i N a les línies, i vaig pensar com funciona el joc de veritat. Ho vaig fer relació per relació.

### Personatge i habilitat: "posseeix"

Un personatge pot tenir moltes habilitats, i una mateixa habilitat la poden tenir molts personatges. A més, pot haver-hi un personatge sense cap habilitat i una habilitat que ningú no té. Per això és de zero o molts als dos costats (`}o--o{`). Aquesta relació és de **molts a molts**.

### Personatge i ítem: "equipa"

Un personatge pot equipar molts ítems, i un mateix ítem el poden equipar molts personatges. També és de molts a molts.

```mermaid
erDiagram
    PERSONATGE }o--o{ ITEM : equipa
```

### Personatge i enemic: "enfronta"

Un personatge es pot enfrontar a molts enemics, i un enemic pot ser enfrontat per molts personatges. Una altra vegada, de molts a molts.

```mermaid
erDiagram
    PERSONATGE }o--o{ ENEMIC : enfronta
```

### Enemic i habilitat: "enfronta"

Els enemics també fan servir habilitats per lluitar. Un enemic pot tenir moltes habilitats i una habilitat la poden fer servir molts enemics, així que també és de molts a molts.

```mermaid
erDiagram
    ENEMIC }o--o{ HABILITAT : enfronta
```

### Habilitat amb ella mateixa: "combina amb"

Aquesta va ser la més curiosa. Algunes habilitats es poden combinar amb altres habilitats, i això vol dir que l'entitat es relaciona **amb ella mateixa**. Això s'anomena relació reflexiva. Simplement poso la mateixa entitat als dos costats de la línia. Com que el nom de la relació té dues paraules, l'he posat entre cometes.

```mermaid
erDiagram
    HABILITAT }o--o{ HABILITAT : "combina amb"
```

### Personatge i mascota: "acompanya"

Aquesta és l'única relació d'**un a un** del joc. Cada personatge té una mascota que l'acompanya, i cada mascota va amb un sol personatge. Per això he fet servir `||` als dos costats.

```mermaid
erDiagram
    PERSONATGE ||--|| MASCOTA : acompanya
```

### Mascota i ítem: "carrega"

La mascota porta objectes a la motxilla. Una mascota pot carregar molts ítems (o cap), però un mateix ítem només pot anar a la motxilla d'una mascota, o de cap si ningú el porta. Per això a la banda de la mascota hi ha `|o` (zero o un) i a la de l'ítem hi ha `o{` (zero o molts).

```mermaid
erDiagram
    MASCOTA |o--o{ ITEM : carrega
```

### Totes les relacions juntes

Quan ja tenia les set relacions, les vaig ajuntar en un sol codi per veure-les totes alhora:

```mermaid
erDiagram
    PERSONATGE }o--o{ HABILITAT : posseeix
    PERSONATGE }o--o{ ITEM : equipa
    PERSONATGE }o--o{ ENEMIC : enfronta
    ENEMIC }o--o{ HABILITAT : enfronta
    HABILITAT }o--o{ HABILITAT : "combina amb"
    PERSONATGE ||--|| MASCOTA : acompanya
    MASCOTA |o--o{ ITEM : carrega
```

Una cosa que vaig tenir en compte és que moltes d'aquestes relacions són de molts a molts (`posseeix`, `equipa`, les dues d'`enfronta` i `combina amb`). Al diagrama no hi ha cap problema, perquè només és el dibuix del disseny. Però la guia del professor avisa que, en una base de dades real, cada relació de molts a molts s'haurà de convertir en una taula intermèdia.

---

## Pas 9. El diagrama final

Per acabar, vaig ajuntar les cinc entitats amb tots els seus atributs 

I aquest seria el diagrama sencer acabat:

```mermaid
---
config:
  theme: neutral
  look: classic
  layout: elk
---
erDiagram
    PERSONATGE {
        string DNI PK
        string Nom "NOT NULL"
        string Cognom
        int Vida
        int Forca
        int Agilitat
        int Carisma
    }
    HABILITAT {
        int Codi PK
        string Nom "NOT NULL"
        int Cost
        int Dany
        int Cooldown
        string Tipus "NOT NULL"
    }
    ENEMIC {
        int Codi PK
        string Nom "NOT NULL"
        string Tipus "NOT NULL"
        int Nivell "NOT NULL"
        int Vida
        int Forca
        int Agilitat
        int Carisma
    }
    MASCOTA {
        string Num_Chip PK
        string Nom "NOT NULL"
        int Motxilla
    }
    ITEM {
        int Codi PK
        string Nom "NOT NULL"
        boolean Equipable
        boolean Comerciable "NOT NULL"
        string Tipus "NOT NULL"
        float Pes "NOT NULL"
        string Qualitat "NOT NULL"
        float Mesura_X "NOT NULL"
        float Mesura_Y "NOT NULL"
        float Mesura_Z "NOT NULL"
    }

    PERSONATGE }o--o{ HABILITAT : posseeix
    PERSONATGE }o--o{ ITEM : equipa
    PERSONATGE }o--o{ ENEMIC : enfronta
    ENEMIC }o--o{ HABILITAT : enfronta
    HABILITAT }o--o{ HABILITAT : "combina amb"
    PERSONATGE ||--|| MASCOTA : acompanya
    MASCOTA |o--o{ ITEM : carrega
```
