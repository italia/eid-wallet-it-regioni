# Entra con IT-Wallet - Statistics API Template

Template OpenAPI per i servizi di monitoraggio e statistica dedicati al flusso di autenticazione **"Entra con IT-Wallet"**.

---
[⬅️ Torna al README principale](../README.md)

## 📌 Descrizione
Questa specifica OpenAPI `entra-con-it-wallet-statistics.yaml` è progettata per **Hub Regionali** e **Aggregatori Tecnici**. Stabilisce un'interfaccia standard per esporre i dati di autenticazione aggregati per più enti federati gestiti da un singolo ente.

## 🚀 Per Iniziare

### Sostituzione dei Placeholder
I placeholder all'interno della specifica YAML (es. domini degli enti, email di contatto e nomi dei servizi) sono gestiti e sostituiti automaticamente dalla **PDND (Piattaforma Digitale Nazionale Dati)** quando questo template viene implementato e pubblicato.

## 🛠 Principi di Progettazione dell'API

### 1. Interfaccia di Query Flessibile
Per gestire filtri complessi (temporali e per ente IPA) senza limitazioni sulla lunghezza degli URL, le statistiche vengono recuperate tramite metodi `POST`:
- `/auth-stats/summary`: Report aggregato globale per il periodo richiesto.
- `/auth-stats/breakdown`: Elenco dettagliato e paginato delle metriche (es. trend giornalieri o per singolo ente).

### 2. Anagrafica Amministrazioni Gestite
L'endpoint `GET /public-administrations` permette di recuperare l'elenco dei codici IPA e dei nomi degli enti federati gestiti dall'Hub o dall'Aggregatore. Questo è essenziale per popolare i filtri di ricerca granulari.

### 3. Intervallo Temporale e Granularità
- **Date Inclusive**: I filtri utilizzano `from` e `to` (ISO 8601), entrambi inclusivi.
- **Granularità Dinamica**: Supporto per le viste `daily`, `monthly` (default), `yearly` e `total`.
- **Periodo del Report**: La risposta include il periodo effettivo coperto dai dati, garantendo trasparenza se i dati non sono disponibili per determinati intervalli (es. date future).

### 4. Categorizzazione dei Fallimenti
I fallimenti sono categorizzati per facilitare la risoluzione dei problemi:
- **technical**: Problemi di infrastruttura, lato server o di connettività (responsabilità dell'Aggregatore).
- **business**: Scadenza del token, accesso non autorizzato o problemi a livello di logica applicativa (responsabilità dell'Utente/Client).

### 5. Paginazione dei Bucket Temporali
Nell'endpoint di breakdown, `limit` e `offset` paginano le **voci** (bucket) generate dalla query.
- **Limite massimo**: Il parametro `limit` è impostato a un massimo di **100** elementi per pagina.
- **Utilizzo**: Un client può usare `limit: 30` e `offset: 0` per recuperare, ad esempio, il primo mese di dati giornalieri.

## 📊 Esempi
Per un elenco dettagliato di esempi di richiesta e risposta che coprono vari scenari (Riepilogo Globale, breakdown giornaliero IPA, trend mensili Hub, periodi annuali personalizzati e paginazione), consultare la [Cartella degli Esempi](examples/README.md).

## 🔒 Compliance e Header

Per garantire l'interoperabilità e la sicurezza, sono implementati i seguenti header:

- **Cache-Control**: Policy rigorosa (`no-store`, `no-cache`, `private`, `max-age=0`) per prevenire l'uso di dati obsoleti o perdite di dati.
- **Rate-Limiting**: Utilizza gli header `X-RateLimit-*` per comunicare le quote.
- **Retry-After**: Fornito nelle risposte `429` (Too Many Requests) e `503` (Service Unavailable). Quando presente, gli header `X-RateLimit` vengono omessi per evitare ambiguità e rispettare le RFC.
- **Problem Details**: Le risposte di errore seguono la **RFC 7807** (`application/problem+json`).

## ⚖️ Licenza
Questo progetto è concesso in licenza secondo la **European Union Public Licence (EUPL-1.2)**. Consultare il file `LICENSE` per i dettagli.
