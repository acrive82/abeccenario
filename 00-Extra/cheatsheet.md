# Pattern Algoritmici: Cheatsheet

## 1. Pattern di Controllo Base

### Sequenza Semplice
```
PASSAGGIO 1
PASSAGGIO 2
PASSAGGIO 3
```
Utilizzato quando le azioni devono essere eseguite in ordine specifico, senza condizioni.
Esempio: Ricetta base per il caffè.

### Selezione Binaria (If/Else)
```
SE condizione
    ESEGUI azione A
ALTRIMENTI
    ESEGUI azione B
```
Utilizzato per decisioni semplici con due possibili percorsi.
Esempio: Decidere se prendere l'ombrello.

### Selezione Multipla
```
SE condizione1
    ESEGUI azione1
ALTRIMENTI SE condizione2
    ESEGUI azione2
ALTRIMENTI SE condizione3
    ESEGUI azione3
ALTRIMENTI
    ESEGUI azione_default
```
Utilizzato quando ci sono multiple possibili strade da seguire.
Esempio: Scegliere l'abbigliamento in base alla temperatura.

### Loop con Contatore
```
PER contatore DA inizio A fine
    ESEGUI azione
    incrementa contatore
```
Utilizzato quando sappiamo esattamente quante volte ripetere un'azione.
Esempio: Distribuire carte da gioco.

### Loop con Condizione
```
MENTRE condizione
    ESEGUI azione
    aggiorna condizione
```
Utilizzato quando non sappiamo in anticipo quante iterazioni serviranno.
Esempio: Mescolare fino a quando l'impasto è omogeneo.

## 2. Pattern di Gestione Risorse

### Acquisizione e Rilascio
```
ACQUISISCI risorsa
PROVA
    USA risorsa
ALLA FINE
    RILASCIA risorsa
```
Utilizzato quando si lavora con risorse limitate che devono essere rilasciate.
Esempio: Prenotazione tavolo al ristorante.

### Pool di Risorse
```
MENTRE ci sono richieste
    SE risorsa_disponibile NEL pool
        ASSEGNA risorsa
    ALTRIMENTI
        AGGIUNGI a coda_attesa
```
Utilizzato per gestire un numero limitato di risorse condivise.
Esempio: Gestione parcheggi.

## 3. Pattern di Accumulazione

### Accumulatore
```
inizializza accumulatore
PER OGNI elemento IN collezione
    elabora elemento
    aggiorna accumulatore
```
Utilizzato per calcolare totali o raccogliere risultati.
Esempio: Calcolare la media dei voti.

### Filtraggio
```
inizializza lista_risultati
PER OGNI elemento IN collezione
    SE elemento soddisfa criterio
        AGGIUNGI elemento a lista_risultati
```
Utilizzato per selezionare elementi che soddisfano certi criteri.
Esempio: Trovare tutti i prodotti in scadenza.

## 4. Pattern di Coordinazione

### Produttore-Consumatore
```
MENTRE ci sono prodotti da processare
    prodotto = PRODUCI_NUOVO()
    AGGIUNGI prodotto a coda
    
    SE coda NON vuota
        prodotto = PRELEVA da coda
        PROCESSA prodotto
```
Utilizzato quando abbiamo processi che generano dati e altri che li consumano.
Esempio: Sistema di ordini in cucina.

### Observer
```
PER OGNI osservatore IN lista_osservatori
    SE evento_rilevante
        NOTIFICA osservatore
```
Utilizzato per notificare parti del sistema quando succede qualcosa.
Esempio: Sistema di notifiche.

## 5. Pattern di Ottimizzazione

### Divide et Impera
```
SE problema è piccolo
    RISOLVI direttamente
ALTRIMENTI
    DIVIDI in sotto_problemi
    PER OGNI sotto_problema
        RISOLVI ricorsivamente
    COMBINA soluzioni
```
Utilizzato per scomporre problemi complessi in parti più gestibili.
Esempio: Organizzare un grande evento.

### Cache
```
SE risultato IN cache
    RETURN risultato_cached
ALTRIMENTI
    risultato = CALCOLA()
    SALVA risultato IN cache
    RETURN risultato
```
Utilizzato per memorizzare risultati di operazioni costose.
Esempio: Memorizzazione risultati di calcoli complessi.

## 6. Pattern di Gestione Errori

### Retry
```
tentativi = 0
MENTRE tentativi < max_tentativi
    PROVA
        ESEGUI operazione
        ESCI dal ciclo
    SE ERRORE
        tentativi += 1
        ATTENDI prima_di_riprovare
```
Utilizzato per operazioni che potrebbero fallire temporaneamente.
Esempio: Tentativo di connessione a un servizio.

### Fallback
```
PROVA
    ESEGUI strategia_principale
SE FALLISCE
    PROVA
        ESEGUI strategia_backup
    SE FALLISCE
        ESEGUI strategia_emergenza
```
Utilizzato per avere piani di backup in caso di fallimento.
Esempio: Sistema di pagamento con multiple opzioni.

## 7. Pattern di Sincronizzazione

### Semaforo
```
MENTRE ci sono richieste
    ATTENDI semaforo_verde
    ESEGUI operazione_critica
    SEGNALA semaforo_completato
```
Utilizzato per gestire accesso a risorse condivise.
Esempio: Gestione code in banca.

### Checkpoint
```
MENTRE elaborazione IN corso
    ESEGUI passo
    SE è_punto_controllo
        SALVA stato
        VERIFICA integrità
```
Utilizzato per salvare progressi in operazioni lunghe.
Esempio: Salvataggio automatico documenti.

## Note sull'Utilizzo

1. **Combinazione di Pattern**: I pattern possono e devono essere combinati per risolvere problemi complessi. Ad esempio, un sistema di prenotazioni potrebbe usare:
   - Semaforo per gestire accessi concorrenti
   - Cache per memorizzare disponibilità
   - Retry per gestire errori di comunicazione
   - Observer per notificare cambiamenti

2. **Scelta del Pattern**: La scelta dipende da:
   - Tipo di problema da risolvere
   - Risorse disponibili
   - Requisiti di performance
   - Necessità di manutenzione
   - Complessità accettabile

3. **Personalizzazione**: I pattern sono linee guida, non regole rigide. Adattali alle tue esigenze specifiche.

4. **Documentazione**: Quando usi un pattern, documentalo chiaramente nei commenti per facilitare la manutenzione futura.