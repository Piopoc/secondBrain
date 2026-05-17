# Protocollo Operativo: Second Brain Knowledge Base

Questo documento definisce il protocollo vincolante per ogni operazione di lettura, scrittura e sintesi all'interno della directory `secondBrain`. Ogni agente che opera in questo contesto DEVE attenersi rigorosamente a queste procedure per garantire l'integrità e la crescita compounding della base di conoscenza.

## 1. Architettura a Tre Livelli
- **Raw Layer (`/raw/`)**: Immutabile. Sola lettura. È vietato modificare o eliminare i file in questa cartella. Rappresentano la verità sorgente.
- **Wiki Layer (`/wiki/`)**: Proprietà dell'LLM. È lo spazio di sintesi, collegamento e distillazione della conoscenza.
- **Schema Layer (`SKILLS.md`)**: Le regole di ingaggio e il protocollo operativo.

## 2. Workflow Operativi

### A. Ingest Workflow (Nuove Fonti)
Quando una nuova fonte viene aggiunta a `/raw/`, seguire esattamente questa sequenza:

1. **Consultazione Strutturale**: 
   - Chiedere all'utente se la fonte appartiene a una nuova categoria.
   - Se sì: creare una nuova sottocartella in `/wiki/summaries/[Categoria]/`, inizializzare un file `Index.md` interno e aggiungere il link a tale indice in `wiki/index.md`.

2. **Analisi**: Leggere la fonte e identificare entità, concetti chiave e claim.
3. **Sintesi Primaria**: Creare o aggiornare una pagina in `/wiki/summaries/[Categoria]/` che condensi la fonte.
4. **Sintesi Atomica**:
    - Creare/aggiornare pagine in `/wiki/entities/` (chi/cosa) e `/wiki/concepts/` (idee/teorie).
    - Collegare queste pagine al sommario e tra di loro usando `[[Nome Pagina]]`.
    - **Gestione Conflitti**: Se la fonte contraddice conoscenze esistenti, loggare l'evento in `/wiki/contradictions.md`.
5. **Catalogazione**: Aggiornare l'indice di modulo (`summaries/[Categoria]/Index.md`) con i nuovi link e brevi descrizioni.
6. **Sintesi Narrativa (Compounding)**: Creare o aggiornare un documento in `/wiki/synthesis/` che colleghi i concetti atomici in un flusso discorsivo, spiegando l'evoluzione logica e le dipendenze.
7. **Audit Tecnico**: Verificare che ogni link `[[ ]]` punti a un file esistente e che non vi siano nuovi concetti orfani.
8. **Log**: Aggiungere un'entry al log. Se più file della stessa fonte sono processati in sessione, creare un'unica voce riassuntiva.

**✅ Checklist di Chiusura Ingest:**
- [ ] Sottocartella e Index di modulo creati/aggiornati?
- [ ] File in `/wiki/summaries/` creato/aggiornato?
- [ ] Entità e Concetti estratti, linkati e privi di orfani?
- [ ] Sintesi narrativa in `/wiki/synthesis/` aggiornata?
- [ ] Eventuali contraddizioni loggate in `/wiki/contradictions.md`?
- [ ] Entry batch aggiunta a `wiki/log.md`?

### B. Query Workflow (Risposte a Domande)
Quando l'utente pone una domanda sulla base di conoscenza:
1. **Scansione**: Leggere `wiki/index.md` e gli indici di modulo per identificare le pagine rilevanti.
2. **Sintesi**: Leggere le pagine identificate e generare una risposta con citazioni esplicite (es. `[[Sintesi di X]]`).
3. **Compounding**: Se la risposta rivela una nuova connessione o un'intuizione non presente, creare una nuova pagina in `/wiki/synthesis/` per preservare la scoperta.
4. **Gap Analysis**: Se la risposta evidenzia una mancanza di informazioni, aggiungere il task in `/wiki/todo.md`.

**✅ Checklist di Chiusura Query:**
- [ ] La risposta è basata su prove presenti nella Wiki?
- [ ] Sono presenti link `[[ ]]` alle fonti/sintesi utilizzate?
- [ ] Nuove intuizioni salvate in `/wiki/synthesis/`?
- [ ] Lacune informative aggiunte a `/wiki/todo.md`?

### C. Lint Workflow (Manutenzione)
Eseguire periodicamente o su richiesta un audit della salute della wiki:
1. **Orfani**: Identificare pagine senza link in entrata.
2. **Obsolescenza**: Identificare claim superati da fonti più recenti.
3. **Lacune**: Suggerire pagine per concetti menzionati frequentemente ma non definiti.

**✅ Checklist di Chiusura Lint:**
- [ ] Pagine orfane collegate o rimosse?
- [ ] Claim obsoleti aggiornati o contrassegnati?
- [ ] Nuovi suggerimenti di pagine aggiunti a `/wiki/todo.md`?

## 3. Convenzioni di Formattazione
- **Link**: Usare esclusivamente link interni stile Obsidian: `[[Nome Pagina]]`.
- **Naming File**:
    - `/wiki/concepts/` e `/wiki/entities/`: Usare **spazi**, mai underscore (es. `Sistemi di Recupero.md`).
    - `/wiki/summaries/[Categoria]/`: Non includere il nome della categoria nel filename (es. `Fondamenti.md` invece di `IR - Fondamenti.md`).
- **Frontmatter**: Ogni pagina della wiki deve iniziare con YAML:
  ```yaml
  ---
  date: YYYY-MM-DD
  source: [[Nome Fonte]]
  tags: [tag1, tag2]
  ---
  ```
- **Log Format**: Usare un elenco puntato. Formato: `- [YYYY-MM-DD] operazione | Descrizione sintetica (batch se applicabile)`.
- **Index Format**: Liste categorizzate con una riga di descrizione per ogni link.
