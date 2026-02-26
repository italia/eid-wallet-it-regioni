# **Dettagli implementativi per l’Avviso PA digitale 2026 per Regioni e Province Autonome**

## **MISURA 1.3.1 PNRR “PIATTAFORMA DIGITALE NAZIONALE DATI” - IT WALLET**

## **Indice dei contenuti**

- [Introduzione e contesto](#introduzione-e-contesto)
- [Scopo e ambito di applicazione](#scopo-e-ambito-di-applicazione)
- [Requisiti tecnici e di conformità](#requisiti-tecnici-e-di-conformità)
- [API raccomandate e specifiche operative](#api-raccomandate-e-specifiche-operative)
- [Possibili ambiti di interesse (non esaustivi)](#possibili-ambiti-di-interesse-non-esaustivi)
- [Domande frequenti e chiarimenti tecnici](#domande-frequenti-e-chiarimenti-tecnici)
- [Indicazioni finali](#indicazioni-finali)
- [Come contribuire](#come-contribuire)



## Introduzione e contesto

Il presente repository fornisce indicazioni e raccomandazioni tecniche
relative alla partecipazione all’[Avviso pubblico PNRR 1.3.1 - PDND / IT
Wallet](https://areariservata.padigitale2026.gov.it/Pa_digitale2026_dettagli_avviso?id=a01bU00000NTeWKQA1). 

Le disposizioni qui riportate costituiscono un quadro interpretativo
condiviso volto a garantire uniformità e coerenza nell’attuazione di
quanto previsto dall’avviso.

L’obiettivo dell’avviso è l’esposizione di API su PDND volte alla
creazione di **Attestati Elettronici di Attributi (EAA)**, fruibili
attraverso l’**IT-Wallet del cittadino** (ad eccezione dell’API
statistica).

Le API pubblicate da Regioni e Province Autonome costituiranno i dati
ufficiali utilizzati dal **Credential Issuer** per l’emissione degli
Attestati Elettronici di Attributi

## **Scopo e ambito di applicazione**

Il contenuto del repository ha lo scopo di:

- fornire una cornice tecnica e metodologica per la progettazione e
  pubblicazione di API destinate all’IT-Wallet;

- individuare le API raccomandate e altri possibili ambiti di interesse;

- proporre dei modelli dati per le API raccomandate ai fini della
  pubblicazione nel Catalogo PDND.

**Il repository è inteso come strumento di condivisione e aperto alla
collaborazione tra tutti gli Enti coinvolti.**

## **Requisiti tecnici e di conformità**

### Requisiti di conformità

Le API dovranno seguire le informazioni presenti nel [Manuale Operativo
di
PDND](https://developer.pagopa.it/pdnd-interoperabilita/guides/pdnd-manuale-operativo)
(con particolare riferimento alla sezione “e-service”) ed essere
conformi alle **Specifiche Tecniche del Sistema IT-Wallet**, disponibili
presso il [repository
ufficiale](https://italia.github.io/eid-wallet-it-docs/versione-corrente/it/),
le cui sezioni di maggiore interesse sono:

- [**10.4 Fonti
  Autentiche**](https://italia.github.io/eid-wallet-it-docs/versione-corrente/it/authentic-sources.html)

- [**20.2. e-service
  PDND**](https://italia.github.io/eid-wallet-it-docs/versione-corrente/it/e-service-pdnd.html)

### **Requisiti tecnici**

1.  **Identificativo univoco** - Il Codice Fiscale (CF) rappresenta
    l’identificativo univoco da utilizzare per le chiamate alle API (ad
    eccezione dell’API statistica)

2.  **Risposta sincrona** - Le API devono rispondere in modalità
    sincrona

3.  **Pubblicazione nel Catalogo PDND** - Ogni API dovrà esporre un set
    di dati completo nel contenuto e negli attributi. È ammessa la
    pubblicazione di basi dati parziali relative a **periodi temporali
    limitati.**

### Titolarità dei dati 

Ai fini del presente Avviso, come definito nell'[Allegato 2](https://areariservata.padigitale2026.gov.it/sfc/servlet.shepherd/document/download/069bU000008dROjQAM?operationContext=S1), la Regione/Provincia Autonoma può operare
quale erogatore dell’e-service su PDND:

- **in qualità di Titolare di Fonte Autentica;**

- **a supporto del Titolare di Fonte autentica**, nei limiti dell’ambito
  regionale di competenza, ai fini dell’esposizione degli e-service
  necessari alla creazione, verifica, stato e revoca/sospensione degli
  attestati elettronici di attributi. I rapporti giuridici e
  organizzativi tra la Fonte Autentica e la Regione/Provincia Autonoma,
  inclusi quelli sul trattamento dei dati personali, sono disciplinati
  da specifici accordi o atti che la Regione/Provincia Autonoma deve
  tenere agli atti per la produzione al Dipartimento per la
  Trasformazione digitale. Tali accordi o atti devono includere le
  previsioni necessarie ad assicurare la disponibilità di tutto quanto
  richiesto per eseguire sul progetto verifiche tecniche, controlli
  formali e sostanziali da parte del DTD e audit e indagini da parte
  delle Autorità nazionali ed europee competenti, compresa, ove
  richiesto, l’esecuzione di attività ispettive presso le Fonti
  Autentiche, legate alla verifica del corretto funzionamento dei
  progetti finanziati a valere sul presente Avviso. Si ricorda infatti
  che la Regione/Provincia Autonoma è il Soggetto Attuatore responsabile
  nei confronti del Dipartimento per la trasformazione digitale della
  corretta attuazione dell’intero progetto finanziato e degli obblighi
  derivanti dal finanziamento con fondi PNRR in relazione alla Misura
  1.3.1.

## **API raccomandate e specifiche operative**

### **A. API Statistica Autenticazioni IT-Wallet**

**Obiettivo:** rendere possibile il monitoraggio anonimo del numero di
autenticazioni avvenute sulle piattaforme delle Regioni e delle Province
Autonome tramite IT-Wallet.

Il servizio espone metriche aggregate relative ai flussi di
autenticazione, supportando filtri temporali e per ente (IPA).

Per i dettagli tecnici completi, la specifica OpenAPI e gli esempi di
integrazione, si rimanda alla documentazione dedicata:  
👉 [**Documentazione API Statistica (auth-stats)**](./auth-stats/)

**Endpoint principali:**
- `POST /auth-stats/summary`: Report aggregato globale per il periodo richiesto.
- `POST /auth-stats/breakdown`: Elenco dettagliato e paginato delle metriche (es. per giorno o per IPA).
- `GET /public-administrations`: Elenco IPA delle amministrazioni gestite (necessario per filtri granulari).

**Esempio richiesta Breakdown (Daily con Paginazione):**
````json
{
  "period": {
    "from": "2025-03-01",
    "to": "2025-03-31"
  },
  "granularity": "daily",
  "limit": 5,
  "offset": 10
}
````

**Esempio risposta Breakdown (200):**
````json
{
  "period": { "from": "2025-03-01", "to": "2025-03-31" },
  "pagination": { "limit": 5, "offset": 10, "totalItems": 31 },
  "breakdown": [
    {
      "label": "2025-03-11",
      "granularity": "daily",
      "stats": { 
        "total": 140, 
        "success": 135,
        "failure": { "total": 5, "technical": 1, "business": 4 }
      }
    },
    {
      "label": "2025-03-12",
      "granularity": "daily",
      "stats": { 
        "total": 135, 
        "success": 130,
        "failure": { "total": 5, "technical": 2, "business": 3 }
      }
    },
    { "label": "2025-03-13", "granularity": "daily", "stats": { "total": 150, "success": 145 } },
    { "label": "2025-03-14", "granularity": "daily", "stats": { "total": 155, "success": 150 } },
    { "label": "2025-03-15", "granularity": "daily", "stats": { "total": 130, "success": 125 } }
  ]
}
````

Per maggiori dettagli sull’implementazione dell’autenticazione, si
rimanda alle sezioni delle Specifiche Tecniche ["Flusso
remoto"](https://italia.github.io/eid-wallet-it-docs/versione-corrente/it/remote-flow.html)
e
“[Autenticazione](https://italia.github.io/eid-wallet-it-docs/versione-corrente/it/functionalities.html#authentication)”.
### **B. API Badge Impiegato Regionale**

**Obiettivo:** mettere a disposizione i dati necessari al Credential
Issuer per generare Attestati Elettronici relativi al personale
regionale.

**Schema dati proposto:**

| **Parametro** | **Descrizione** | **Standard** | **Obbligatorio** |
|----|----|----|----|
| legalName | Stringa. Nome dell’Organizzazione. | [Organization - Schema.org Type](https://schema.org/Organization) | No |
| legalAddress | Stringa. Indirizzo postale dell’organizzazione. | [Organization - Schema.org Type](https://schema.org/Organization) | No |
| location | Stringa. Località o area geografica. | [Organization - Schema.org Type](https://schema.org/Organization) | No |
| logo | Stringa. URL del logo. | [Organization - Schema.org Type](https://schema.org/Organization) | No |
| vatID | Stringa. Partita IVA. | [Organization - Schema.org Type](https://schema.org/Organization) | No |
| telephone | Stringa. Numero di telefono dell’Organizzazione. | [Organization - Schema.org Type](https://schema.org/Organization) | No |
| identifier | Stringa. Identificativo univoco. | [Thing - Schema.org Type](https://schema.org/Thing) | No |
| validFrom | Stringa. Data di inizio validità. | [validFrom - Schema.org Property](https://schema.org/validFrom) | No |
| validThrough | Stringa. Data di fine validità. | [validThrough - Schema.org Property](https://schema.org/validThrough) | No |
| member | Oggetto JSON che contiene i claim del singolo individuo (PII) elencati nella tabella sottostante. | [Organization - Schema.org Type](https://schema.org/Organization) | No |
| employee | Oggetto JSON che contiene i claim del singolo individuo (PII) elencati nella tabella sottostante. | [Organization - Schema.org Type](https://schema.org/Organization) | No |

<table>
<colgroup>
<col style="width: 21%" />
<col style="width: 32%" />
<col style="width: 34%" />
<col style="width: 11%" />
</colgroup>
<thead>
<tr>
<th colspan="4" style="text-align: center;"><strong>PII
Claim</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>givenName</td>
<td>Stringa. Nome.</td>
<td><a href="https://schema.org/Person">Person - Schema.org
Type</a></td>
<td>No</td>
</tr>
<tr>
<td>familyName</td>
<td>Stringa. Cognome.</td>
<td><a href="https://schema.org/Person">Person - Schema.org
Type</a></td>
<td>No</td>
</tr>
<tr>
<td style="text-align: left;">birthDate</td>
<td>Data di nascita.</td>
<td><a href="https://schema.org/Person">Person - Schema.org
Type</a></td>
<td>No</td>
</tr>
<tr>
<td>address</td>
<td>Stringa. Indirizzo postale.</td>
<td><a href="https://schema.org/Person">Person - Schema.org
Type</a></td>
<td>No</td>
</tr>
<tr>
<td>email</td>
<td>Stringa. Indirizzo email.</td>
<td><a href="https://schema.org/Person">Person - Schema.org
Type</a></td>
<td>No</td>
</tr>
<tr>
<td>honorificPrefix</td>
<td>Stringa. Es: Dott./Sig./Sig.ra</td>
<td><a href="https://schema.org/Person">Person - Schema.org
Type</a></td>
<td>No</td>
</tr>
<tr>
<td>jobTitle</td>
<td>Stringa. Qualifica professionale.</td>
<td><a href="https://schema.org/Person">Person - Schema.org
Type</a></td>
<td>No</td>
</tr>
<tr>
<td>taxID</td>
<td>Stringa. Codice Fiscale.</td>
<td><a href="https://schema.org/Person">Person - Schema.org
Type</a></td>
<td>No</td>
</tr>
<tr>
<td>telephone</td>
<td>Stringa. Numero di telefono.</td>
<td><a href="https://schema.org/Person">Person - Schema.org
Type</a></td>
<td>No</td>
</tr>
<tr>
<td>image</td>
<td>Stringa  </td>
<td>Immagine codificata in Base64</td>
<td>No</td>
</tr>
</tbody>
</table>

Esempio:
````
{
  "iss": "https://authentic-source.example.it",
  "nbf": 1736846688,
  "exp": 1736846928,
  "iat": 1736846688,
  "aud": "82914b3f-60b2-4529-b4d6-3d4e67f0a933",
  "jti": "c8bd8a2f-e990-44fa-9013-1b353bfc5a0d",
  "userClaims": {
    "given_name": "Mario",
    "family_name": "Rossi",
    "birth_date": "1980-01-10",
    "birth_place": "Roma",
    "tax_id_code": "TINIT-RSSMRO75E05H501Z"
  },
  "attributeClaims": [
    {
      "object_id": "GUID-1234-5678",
      "status": "VALID",
      "last_updated": "2024-12-31T23:59:59Z",
      "legal_name": "Regione Lombardia",
      "vat_id": "01234567890",
      "employee_role": "Digital Project Manager",
      "employee_office": "Direzione Sistemi Informativi",
      "badge_code": "BADGE-001"
    }
  ],
  "metadataClaims": [
    {
      "object_id": "GUID-1234-5678",
      "issuance_date": "2024-01-01",
      "expiry_date": "2025-12-31"
    }
  ]
}
````

A [questo link](https://github.com/italia/eid-wallet-it-docs/issues/742)
si può consultare la proposta di data schema per la creazione
dell’Attestato Elettronico.

## **Possibili ambiti di interesse (non esaustivi)**

- **Sanità e Benessere** (esempio: attestato celiachia, tessere di
  invalidità, ecc)

<!-- -->

- **Tesserini Regionali** (esempio: tesserino venatorio, tesserino
  raccolta funghi, tesserino raccolta tartufi, ecc)

- **Qualifiche e Abilitazioni Professionali** (esempio: attestati di
  Istruzione e Formazione Professionale, attestati di Unità di
  Competenza - Formazione Professionale Continua, attestati di
  abilitazione per professioni regolamentate, ecc)

- ...

## **Domande frequenti e chiarimenti tecnici**
Tutte le domande sono gestite nella sezione [*Discussions*](https://github.com/italia/eid-wallet-it-regioni/discussions)


## **Indicazioni finali**

Le presenti raccomandazioni hanno lo scopo di assicurare un **approccio
uniforme, interoperabile e sostenibile** nella progettazione delle API
esposte.  
È pertanto raccomandato che ciascun Ente:

- garantisca la **qualità** del dato esposto;

- adotti **processi di validazione tecnica e funzionale** in linea con
  le regole PDND e IT-Wallet;

- promuova la **standardizzazione dei modelli dati** per favorirne il
  riuso e l’omogeneità di utilizzo.

## Come contribuire

Il presente repository è inteso come strumento di condivisione ed aperto
alla collaborazione tra tutti gli Enti coinvolti.

Qui è possibile iniziare o partecipare a discussioni, fare segnalazioni
o inviare dei contributi a beneficio delle Regioni / Province Autonome
interessate all’Avviso.

Si raccomanda di consultare il [Codice di
condotta](https://github.com/italia/bootstrap-italia/blob/main/CODE_OF_CONDUCT.md)
della community legata ai progetti dell'organizzazione Italia su GitHub,
strumento utile a mantenere un ambiente di collaborazione inclusivo e
propositivo.

Sono particolarmente benvenuti contributi relativi a:

- nuove API idonee alla generazione di Attestati Elettronici;
- nuovi cluster tematici;
- miglioramenti alle API esistenti;
- miglioramenti agli schema dati (aggiunta di nuovi attributi, revisione dei modelli esistenti, definizione di nuovi dataset, ecc);
- documentazione tecnica (ad esempio i casi d’uso);
- standardizzazione (convenzioni su naming, struttura API, semantica dei campi, ecc).

Quando aprire una **Issue**:
- per chiedere chiarimenti tecnici;
- segnalare errori o mancanze.

La sezione **Discussions** è il canale privilegiato per:
- confronto aperto tra Enti;
- proposte preliminari di API;
- valutazioni preliminari su possibili attributi;
- quesiti informali o generali;
- evidenziare casistiche particolari o casi limite.

