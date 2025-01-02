# Selezioni: Prendere Decisioni nel Pensiero Algoritmico

Le selezioni rappresentano il modo in cui gestiamo le decisioni nei nostri algoritmi. Così come nella vita quotidiana prendiamo continuamente decisioni basate su condizioni ("se piove, prendo l'ombrello"), nel pensiero algoritmico utilizziamo le selezioni per creare flussi di esecuzione che si adattano a diverse situazioni.

## Il Concetto di Selezione

Una selezione è essenzialmente una biforcazione nel nostro percorso algoritmico. È come trovarsi di fronte a un bivio: la strada che prenderemo dipende da una o più condizioni che valutiamo in quel momento.

### Anatomia di una Selezione

Una selezione è composta da tre elementi principali:

1. **Condizione**: La domanda a cui rispondiamo per prendere la decisione
2. **Azione Positiva**: Cosa facciamo se la condizione è vera
3. **Azione Negativa** (opzionale): Cosa facciamo se la condizione è falsa

## Le Forme della Selezione

### Selezione Semplice (IF)
```
SE condizione
    esegui azione
```

Esempio pratico - Attraversare la strada:
```
SE il semaforo è rosso
    attendi che diventi verde
```

### Selezione Binaria (IF-ELSE)
```
SE condizione
    esegui azione A
ALTRIMENTI
    esegui azione B
```

Esempio pratico - Uscire di casa:
```
SE sta piovendo
    prendi l'ombrello
ALTRIMENTI
    prendi gli occhiali da sole
```

### Selezione Multipla (IF-ELSE IF-ELSE)
```
SE condizione1
    esegui azione1
ALTRIMENTI SE condizione2
    esegui azione2
ALTRIMENTI SE condizione3
    esegui azione3
ALTRIMENTI
    esegui azione_default
```

Esempio pratico - Scegliere il mezzo di trasporto:
```
SE la distanza < 1 km
    vai a piedi
ALTRIMENTI SE la distanza < 5 km
    prendi la bicicletta
ALTRIMENTI SE c'è traffico intenso
    prendi la metropolitana
ALTRIMENTI
    prendi l'auto
```

## Condizioni Complesse

Le condizioni possono essere combinate usando operatori logici:

### AND (E)
Tutte le condizioni devono essere vere:
```
SE è weekend E fa bel tempo
    organizza una gita
```

### OR (O)
Almeno una condizione deve essere vera:
```
SE piove O sta nevicando
    resta a casa
```

### NOT (NON)
Inverte il valore della condizione:
```
SE NON c'è traffico
    prendi la strada principale
```

## Nidificazione delle Selezioni

Le selezioni possono essere nidificate l'una dentro l'altra:

```
SE è giorno lavorativo
    SE è ora di punta
        prendi la metropolitana
        SE la metropolitana è affollata
            aspetta la prossima
        ALTRIMENTI
            sali su questa
    ALTRIMENTI
        prendi l'auto
ALTRIMENTI
    dormi fino a tardi
```

## Pattern Comuni di Selezione

### Pattern Guard
Protegge l'esecuzione verificando precondizioni:
```
SE NON hai ingredienti sufficienti
    vai a fare la spesa
    SE il negozio è chiuso
        ordina online
    ALTRIMENTI
        compra gli ingredienti
ALTRIMENTI
    inizia a cucinare
```

### Pattern Default
Fornisce un comportamento di fallback:
```
SE file esiste
    leggi file
ALTRIMENTI
    usa configurazione default
```

### Pattern Catena di Responsabilità
Serie di controlli in sequenza:
```
SE hai contanti
    paga in contanti
ALTRIMENTI SE hai carta di credito
    paga con carta
ALTRIMENTI SE hai portafoglio digitale
    paga digitalmente
ALTRIMENTI
    rimanda l'acquisto
```

## Tecniche di Ottimizzazione

### 1. Ordine delle Condizioni
Mettere le condizioni più probabili o meno costose da verificare per prime:

```
// Meglio
SE è orario di apertura     // verifica veloce
    SE sistema funzionante  // verifica più lenta
        apri negozio

// Peggio
SE sistema funzionante      // verifica lenta sempre
    SE è orario di apertura // spesso non necessaria
        apri negozio
```

### 2. Consolidamento delle Condizioni
Unire condizioni simili quando possibile:

```
// Invece di
SE temperatura < 20
    metti la giacca
SE piove
    metti la giacca

// Meglio
SE temperatura < 20 O piove
    metti la giacca
```

### 3. Early Return
Uscire presto dalle condizioni quando possibile:

```
SE NON hai permessi
    termina
SE NON ci sono risorse
    termina
SE tutto ok
    procedi
```

## Errori Comuni da Evitare

1. **Condizioni Ridondanti**
```
// Ridondante
SE età >= 18
    sei maggiorenne
ALTRIMENTI SE età < 18
    sei minorenne

// Meglio
SE età >= 18
    sei maggiorenne
ALTRIMENTI
    sei minorenne
```

2. **Condizioni Ambigue**
```
// Ambiguo
SE temperatura è alta E umidità è elevata O c'è vento
    stai a casa

// Chiaro (con parentesi)
SE (temperatura è alta E umidità è elevata) O c'è vento
    stai a casa
```

3. **Nidificazione Eccessiva**
```
// Difficile da seguire
SE condizione1
    SE condizione2
        SE condizione3
            fai_qualcosa

// Meglio
SE NON condizione1
    termina
SE NON condizione2
    termina
SE NON condizione3
    termina
fai_qualcosa
```

## Esercizi Pratici

1. **Algoritmo Vestirsi**
   Crea un algoritmo per decidere cosa indossare basato su:
   - Temperatura
   - Previsioni meteo
   - Occasione (lavoro/casual/formale)
   - Vestiti disponibili

2. **Gestione Cucina**
   Sviluppa un algoritmo per decidere cosa cucinare basato su:
   - Ingredienti disponibili
   - Tempo disponibile
   - Numero di persone
   - Preferenze dietetiche

3. **Pianificazione Viaggio**
   Crea un algoritmo per scegliere il mezzo di trasporto considerando:
   - Distanza
   - Budget
   - Tempo disponibile
   - Condizioni meteo
   - Orari dei mezzi pubblici

## Conclusione

Le selezioni sono uno strumento potente che ci permette di creare algoritmi adattivi e intelligenti. La chiave per utilizzarle efficacemente è:
- Mantenere le condizioni chiare e non ambigue
- Organizzare le selezioni in modo logico e efficiente
- Evitare la complessità non necessaria
- Considerare tutti i possibili casi

Nel prossimo capitolo, esploreremo le ripetizioni, che ci permetteranno di eseguire azioni multiple volte in modo controllato e efficiente.