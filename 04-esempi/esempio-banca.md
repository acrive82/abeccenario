# Dal Pensiero al Software: Un Sistema Bancario Semplificato

Immaginiamo di dover creare un sistema bancario molto semplice. Prima di scrivere anche una sola riga di codice, dobbiamo pensare a come funziona una banca dal punto di vista logico. Questo esempio ci mostrerà come i concetti base che abbiamo imparato (sequenze, selezioni e ripetizioni) si combinano in un sistema reale.

## Il Nostro Mini-Sistema Bancario

Implementeremo tre operazioni fondamentali:
1. Apertura di un nuovo conto
2. Prelievo di denaro
3. Visualizzazione del saldo

## Prima Implementazione: Pseudocodice Base

### Strutture Dati di Base
```
STRUTTURA Conto
    numero_conto: testo
    titolare: testo
    saldo: numero
    pin: numero
    stato: testo (attivo/bloccato)
```

### 1. Apertura Nuovo Conto
```
SEQUENZA ApriConto:
    // Input e validazione
    1. Richiedi dati personali
    2. SE età < 18
        MOSTRA "Serve un genitore"
        TERMINA
    
    // Generazione numero conto
    3. numero = GENERA_NUMERO_CASUALE()
    4. MENTRE numero esiste nel sistema
        numero = GENERA_NUMERO_CASUALE()
    
    // Creazione PIN
    5. RIPETI
        pin = CHIEDI_PIN()
        conferma = CHIEDI_CONFERMA_PIN()
        SE pin != conferma
            MOSTRA "I PIN non corrispondono"
    FINCHÉ pin == conferma

    // Deposito iniziale
    6. RIPETI
        deposito = CHIEDI_DEPOSITO_INIZIALE()
        SE deposito < 100
            MOSTRA "Il deposito minimo è 100€"
    FINCHÉ deposito >= 100

    // Creazione effettiva del conto
    7. nuovo_conto = CREA_CONTO(numero, dati, pin, deposito)
    8. SALVA_CONTO(nuovo_conto)
    9. MOSTRA "Conto creato con successo"
```

### 2. Prelievo
```
SEQUENZA Prelievo:
    // Autenticazione
    1. numero_conto = CHIEDI_NUMERO_CONTO()
    2. SE NON ESISTE_CONTO(numero_conto)
        MOSTRA "Conto non trovato"
        TERMINA

    3. tentativi = 0
    4. RIPETI
        pin_inserito = CHIEDI_PIN()
        SE pin_inserito != conto.pin
            tentativi = tentativi + 1
            MOSTRA "PIN errato"
            SE tentativi >= 3
                BLOCCA_CONTO(numero_conto)
                MOSTRA "Conto bloccato per sicurezza"
                TERMINA
    FINCHÉ pin_inserito == conto.pin

    // Verifica disponibilità e prelievo
    5. importo = CHIEDI_IMPORTO()
    6. SE importo > conto.saldo
        MOSTRA "Saldo insufficiente"
        TERMINA
    
    7. SE importo > 1000
        MOSTRA "Limite giornaliero superato"
        TERMINA

    8. conto.saldo = conto.saldo - importo
    9. AGGIORNA_CONTO(conto)
    10. STAMPA_RICEVUTA(conto, importo)
```

### 3. Visualizzazione Saldo
```
SEQUENZA VisualizzaSaldo:
    // Autenticazione (riutilizziamo la logica del prelievo)
    [Stessi passi 1-4 del Prelievo]

    // Mostro il saldo e le ultime operazioni
    5. MOSTRA "Saldo attuale: " + conto.saldo
    6. PER OGNI operazione NELLE ultime_5_operazioni(conto)
        MOSTRA operazione.data + ": " + operazione.tipo + 
              " - " + operazione.importo
```

## Una Versione Più Realistica

Aggiungiamo alcune funzionalità per rendere il sistema più realistico.

### Sistema di Log
```
SEQUENZA RegistraOperazione:
    1. operazione = CREA_LOG(
        timestamp: ORA_ATTUALE(),
        tipo_operazione: tipo,
        numero_conto: conto,
        risultato: esito
    )
    2. SALVA_LOG(operazione)
    3. SE operazione.tipo == "errore_pin"
        NOTIFICA_SICUREZZA(operazione)
```

### Controlli di Sicurezza
```
SEQUENZA VerificaSicurezza:
    // Verifica pattern sospetti
    1. operazioni_recenti = ULTIME_OPERAZIONI(conto, 24_ore)
    
    2. totale_prelievi = 0
    3. PER OGNI op IN operazioni_recenti
        SE op.tipo == "prelievo"
            totale_prelievi += op.importo
    
    4. SE totale_prelievi > 3000
        SEGNALA_ATTIVITA_SOSPETTA(conto)
        RICHIEDI_VERIFICA_IDENTITA()
```

### Gestione Errori
```
SEQUENZA GestisciErrore:
    1. SE è_errore_di_sistema
        RIPRISTINA_STATO_PRECEDENTE(conto)
        NOTIFICA_AMMINISTRATORE()
        MOSTRA "Spiacenti, riprova più tardi"
    
    2. SE è_errore_utente
        REGISTRA_TENTATIVO()
        SE numero_tentativi > 3
            SUGGERISCI_ASSISTENZA()
    
    3. REGISTRA_LOG(errore)
```

## Implementazione Reale (JavaScript)

Vediamo come questo si traduce in codice reale:

```javascript
class ContoBancario {
    constructor(titolare, depositoIniziale) {
        this.numero = this.generaNumeroConto();
        this.titolare = titolare;
        this.saldo = depositoIniziale;
        this.pin = null;
        this.stato = 'attivo';
        this.operazioni = [];
    }

    // Metodi principali
    setPin(pin) {
        if (pin.length !== 4) {
            throw new Error('Il PIN deve essere di 4 cifre');
        }
        this.pin = pin;
    }

    verificaPin(pin) {
        return this.pin === pin;
    }

    preleva(importo, pin) {
        try {
            // Verifica PIN
            if (!this.verificaPin(pin)) {
                this.registraOperazione('errore_pin', 0);
                throw new Error('PIN non valido');
            }

            // Verifica disponibilità
            if (importo > this.saldo) {
                this.registraOperazione('errore_saldo', importo);
                throw new Error('Saldo insufficiente');
            }

            // Verifica limiti
            if (importo > 1000) {
                this.registraOperazione('errore_limite', importo);
                throw new Error('Limite giornaliero superato');
            }

            // Esegui prelievo
            this.saldo -= importo;
            this.registraOperazione('prelievo', importo);

            return {
                successo: true,
                nuovoSaldo: this.saldo
            };
        } catch (error) {
            console.error(`Errore nel prelievo: ${error.message}`);
            return {
                successo: false,
                errore: error.message
            };
        }
    }

    // Metodi di supporto
    registraOperazione(tipo, importo) {
        const operazione = {
            timestamp: new Date(),
            tipo: tipo,
            importo: importo,
            saldoPostOperazione: this.saldo
        };
        this.operazioni.push(operazione);

        // Verifica pattern sospetti
        if (this.operazioni.length >= 3) {
            this.verificaPatternSospetti();
        }
    }

    verificaPatternSospetti() {
        const ultimeTreOperazioni = this.operazioni.slice(-3);
        const tuttiPrelievi = ultimeTreOperazioni.every(
            op => op.tipo === 'errore_pin'
        );

        if (tuttiPrelievi) {
            this.stato = 'bloccato';
            console.log('Conto bloccato per motivi di sicurezza');
        }
    }

    generaNumeroConto() {
        return 'IT' + Math.random().toString().slice(2, 12);
    }
}

// Esempio di utilizzo
const gestisciNuovoConto = (datiCliente) => {
    try {
        // Validazione dati cliente
        if (!datiCliente.età || datiCliente.età < 18) {
            throw new Error('È richiesta la maggiore età');
        }

        // Creazione conto
        const conto = new ContoBancario(
            datiCliente.nome,
            datiCliente.depositoIniziale
        );

        // Impostazione PIN
        if (datiCliente.pin === datiCliente.confermaPin) {
            conto.setPin(datiCliente.pin);
        } else {
            throw new Error('I PIN non corrispondono');
        }

        console.log(`Conto creato con successo: ${conto.numero}`);
        return conto;

    } catch (error) {
        console.error(`Errore nella creazione del conto: ${error.message}`);
        return null;
    }
};
```

## Punti Chiave dell'Esempio

1. **Sequenze**: Ogni operazione segue una sequenza logica di passi (es: verifica PIN → verifica saldo → esegui prelievo)

2. **Selezioni**: Numerosi controlli condizionali per:
   - Validazione input
   - Verifica autorizzazioni
   - Gestione errori
   - Pattern sospetti

3. **Ripetizioni**: Usate per:
   - Tentativi di inserimento PIN
   - Verifica operazioni sospette
   - Log delle operazioni

4. **Gestione Errori**: Implementata a più livelli:
   - Validazione input
   - Controlli di sicurezza
   - Gestione stati anomali

5. **Sicurezza**: Incorporata in ogni operazione:
   - Verifica PIN
   - Limiti operazioni
   - Blocco automatico
   - Log delle attività

Questo esempio mostra come i concetti base che abbiamo imparato si combinino per creare un sistema reale, dove:
- La sicurezza è fondamentale
- Gli errori devono essere gestiti accuratamente
- Le operazioni devono essere tracciate
- Il sistema deve proteggere sia la banca che il cliente

È un esempio semplificato, ma illustra i principi fondamentali che si applicano in sistemi reali più complessi.