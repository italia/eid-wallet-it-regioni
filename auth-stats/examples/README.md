# Esempi Statistiche Entra con IT-Wallet

Questa cartella contiene esempi JSON di richieste e risposte per l'API delle statistiche di "Entra con IT-Wallet".

## Scenari

### 1. Riepilogo Globale
Recupera i conteggi totali delle autenticazioni per un determinato periodo per tutti gli enti gestiti.
- **Richiesta**: [summary_request.json](summary_request.json)
- **Risposta**: [summary_response.json](summary_response.json)

### 2. Breakdown Giornaliero per un Ente Specifico
Monitora un'amministrazione specifica (tramite codice IPA) con granularità giornaliera.
- **Richiesta**: [daily_ipa_request.json](daily_ipa_request.json)
- **Risposta**: [daily_ipa_response.json](daily_ipa_response.json)

### 3. Breakdown Mensile Regionale
Recupera i trend mensili aggregati per tutti gli enti gestiti da un Hub Regionale.
- **Richiesta**: [monthly_hub_request.json](monthly_hub_request.json)
- **Risposta**: [monthly_hub_response.json](monthly_hub_response.json)

### 4. Breakdown Annuale (Periodo Personalizzato)
Esempio di un breakdown annuale che richiede un periodo che attraversa più anni (giugno 2023 - settembre 2024).
- **Richiesta**: [yearly_custom_request.json](yearly_custom_request.json)
- **Risposta**: [yearly_custom_response.json](yearly_custom_response.json)

### 5. Paginazione Giornaliera
Esempio di paginazione dei risultati giornalieri (recupero della terza settimana di marzo).
- **Richiesta**: [daily_pagination_request.json](daily_pagination_request.json)
- **Risposta**: [daily_pagination_response.json](daily_pagination_response.json)

## Nota sulle Statistiche
Gli identificatori tecnici (percorsi, nomi degli schemi e chiavi JSON) utilizzano nomi generici (`total`, `success`, `failure`, ecc.) per semplicità e coerenza con i pattern di monitoraggio standard.

Seguendo lo schema, solo il campo `success` è strettamente obbligatorio negli oggetti statistici. Altri campi come `total`, `failure`, `technical` e `business` sono opzionali e possono essere omessi se i dati non sono disponibili.
