# Ripetizioni: L'Arte di Automatizzare le Azioni

Le ripetizioni, o cicli, rappresentano il terzo pilastro fondamentale del pensiero algoritmico. Sono lo strumento che ci permette di eseguire operazioni ripetitive in modo efficiente e controllato. Proprio come una lavatrice ripete il ciclo di lavaggio fino al completamento del programma, o come un cuoco ripete la stessa preparazione per ogni piatto da servire, le ripetizioni ci permettono di automatizzare sequenze di azioni che devono essere eseguite multiple volte.

## Comprendere le Ripetizioni

Una ripetizione è composta da tre elementi essenziali:
1. Una condizione di inizio
2. Le azioni da ripetere
3. Una condizione di termine

Questi elementi ci permettono di controllare:
- Quando iniziare la ripetizione
- Cosa ripetere
- Quando smettere

## Tipi di Ripetizioni

### 1. Ripetizione con Contatore (FOR)
Utile quando sappiamo in anticipo quante volte vogliamo ripetere un'azione.

Esempio - Preparare più sandwich:
```
PER ogni sandwich DA 1 A 5
    1. Prendi due fette di pane
    2. Aggiungi gli ingredienti
    3. Chiudi il sandwich
    4. Mettilo nel piatto
```

### 2. Ripetizione con Condizione (WHILE)
Utile quando non sappiamo quante ripetizioni saranno necessarie, ma sappiamo quando fermarci.

Esempio - Mescolare un impasto:
```
MENTRE l'impasto non è omogeneo
    1. Mescola per 30 secondi
    2. Controlla la consistenza
```

### 3. Ripetizione con Controllo Posteriore (DO-WHILE)
Simile al WHILE, ma garantisce che le azioni vengano eseguite almeno una volta.

Esempio - Chiedere input a un utente:
```
RIPETI
    1. Chiedi il numero
    2. Verifica se è valido
FINCHÉ il numero non è valido
```

## Pattern Comuni di Ripetizione

### Accumulazione
Utilizzato per costruire un risultato progressivamente:
```
totale = 0
PER ogni prodotto nel carrello
    aggiungi prezzo al totale
```

### Ricerca
Per trovare elementi che soddisfano certi criteri:
```
PER ogni libro nella biblioteca
    SE il titolo corrisponde alla ricerca
        aggiungi alla lista risultati
```

### Elaborazione in Batch
Per processare elementi in gruppi:
```
PER ogni gruppo di 10 documenti
    1. Carica il gruppo
    2. Elabora i documenti
    3. Salva i risultati
    4. Libera la memoria
```

## Tecniche di Ottimizzazione

### 1. Early Exit
Uscire dal ciclo appena possibile:
```
PER ogni elemento
    SE trovato elemento cercato
        ESCI dal ciclo
```

### 2. Skip Condition
Saltare iterazioni non necessarie:
```
PER ogni elemento
    SE elemento non valido
        PASSA al prossimo
    Elabora elemento
```

### 3. Batch Processing
Elaborare più elementi contemporaneamente:
```
PER ogni pagina di 25 elementi
    Elabora la pagina intera
```

## Gestione dei Casi Particolari

### 1. Infinite Loop Prevention
Assicurarsi che il ciclo termini:
```
contatore = 0
MENTRE condizione E contatore < max_tentativi
    elabora
    contatore += 1
```

### 2. Edge Cases
Gestire i casi limite:
```
SE lista è vuota
    termina
PER ogni elemento nella lista
    elabora
```

### 3. Resource Management
Gestire le risorse in modo efficiente:
```
PER ogni file
    1. Apri file
    2. Elabora
    3. Chiudi file (importante!)
```

## Esempi Pratici dalla Vita Quotidiana

### Esempio 1: Lavare i Piatti
```
MENTRE ci sono piatti sporchi
    1. Prendi un piatto
    2. SE molto sporco
        applica prelavaggio
    3. Lava il piatto
    4. Sciacqua
    5. Metti nello scolapiatti
```

### Esempio 2: Organizzare una Biblioteca
```
PER ogni scaffale
    PER ogni libro nello scaffale
        1. Prendi il libro
        2. Controlla la categoria
        3. Posiziona nella sezione corretta
```

### Esempio 3: Gestione Email
```
PER ogni email nella casella
    SE è spam
        sposta nel cestino
    ALTRIMENTI SE è importante
        marca come prioritaria
    ALTRIMENTI
        archivia normalmente
```

## Errori Comuni da Evitare

### 1. Loop Infiniti
```
// Pericoloso!
MENTRE c'è lavoro da fare
    fai qualcosa
    // Dimenticato di aggiornare la condizione!

// Corretto
MENTRE c'è lavoro da fare
    fai qualcosa
    marca lavoro come completato
```

### 2. Off-by-One Errors
```
// Errato: salta l'ultimo elemento
PER contatore DA 1 A lunghezza-1
    elabora elemento

// Corretto
PER contatore DA 1 A lunghezza
    elabora elemento
```

### 3. Condizioni di Uscita Mal Definite
```
// Ambiguo
MENTRE il compito non è finito
    lavora

// Meglio
MENTRE ci sono elementi da processare O tempo_rimasto > 0
    lavora
```

## Esercizi Pratici

### 1. Routine Mattutina
Scrivi un algoritmo per prepararti al mattino, considerando:
- Diverse attività da ripetere ogni giorno
- Variazioni basate sul giorno della settimana
- Gestione del tempo disponibile

### 2. Gestione Magazzino
Crea un algoritmo per:
- Contare l'inventario
- Organizzare prodotti per categoria
- Gestire prodotti in scadenza

### 3. Allenamento
Sviluppa un programma di allenamento che include:
- Ripetizioni di esercizi
- Serie multiple
- Periodi di riposo

## Tecniche Avanzate

### 1. Nested Loops (Cicli Annidati)
```
PER ogni piano dell'edificio
    PER ogni appartamento nel piano
        PER ogni stanza nell'appartamento
            controlla i rilevatori di fumo
```

### 2. Loop con Accumulatori Multipli
```
totale_vendite = 0
numero_clienti = 0
PER ogni transazione
    aggiorna totale_vendite
    aggiorna numero_clienti
```

### 3. Loop con State Machine
```
stato = INIZIALE
MENTRE stato != COMPLETATO
    SWITCH stato
        CASO INIZIALE:
            inizializza
            stato = ELABORAZIONE
        CASO ELABORAZIONE:
            processa
            SE tutto_ok
                stato = COMPLETATO
            ALTRIMENTI
                stato = ERRORE
```

## Conclusione

Le ripetizioni sono uno strumento potente che ci permette di:
- Automatizzare operazioni ripetitive
- Processare grandi quantità di dati
- Gestire situazioni complesse in modo sistematico

La chiave per utilizzare efficacemente le ripetizioni è:
1. Identificare chiaramente cosa deve essere ripetuto
2. Definire condizioni di inizio e fine precise
3. Assicurarsi che il ciclo termini sempre
4. Gestire i casi particolari
5. Ottimizzare quando possibile

Con sequenze, selezioni e ripetizioni, abbiamo ora tutti gli strumenti fondamentali del pensiero algoritmico. La vera sfida sta nel combinarli in modo efficace per risolvere problemi complessi del mondo reale.