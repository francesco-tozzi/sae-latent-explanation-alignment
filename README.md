# Sparse Autoencoder Latents Are Locally Aligned with Their Explanations

Questo codice è stato sviluppato come lavoro di tesi triennale di Francesco Tozzi sotto la supervisione del professor Alessandro Bondielli e per il paper associato: **"Sparse Autoencoder Latents Are Locally Aligned with Their Explanations"** (Tozzi & Bondielli, 2026). 

## Cosa fa e a cosa serve (Il Progetto)
Il progetto mira a esplorare l'organizzazione dello spazio latente degli Sparse Autoencoder (SAE) applicati ai Large Language Models (LLMs). I SAE sono strumenti fondamentali nella *Mechanistic Interpretability* per districare le rappresentazioni polisematiche dei neuroni di un LLM. 
Nello specifico, questa pipeline valuta se e in che misura la **vicinanza geometrica** (nello spazio latente del SAE) tra i vari concetti corrisponda a una **coerenza semantica** tra le spiegazioni in linguaggio naturale generate per quei concetti. 

## Perché è stato fatto (Il Contesto)
Come illustrato nel paper *"Sparse Autoencoder Latents Are Locally Aligned with Their Explanations"*, gli sforzi attuali nella *Mechanistic Interpretability* si sono concentrati molto sui modelli in lingua inglese. L'obiettivo di questo lavoro è dimostrare che, anche per modelli in altre lingue (in questo caso il modello italiano Minerva-1B), esiste un allineamento locale: i *neighborhoods* (vicinati) nello spazio latente contengono concetti semanticamente più simili tra loro di quanto prevedrebbe una baseline casuale. 

---

## Note sul Codice e Struttura
Il codice è stato ottimizzato per essere estremamente efficiente: **l'intera pipeline è eseguibile su un PC con appena 8GB di RAM**.

La repository è organizzata in modo rigorosamente sequenziale:
- Prima del nome di una cartella o di un file `.py` si trova l'indicazione numerica sull'ordine logico e di esecuzione (es. `1_benchmark.py`, `2a_dataset_filter.py`, ecc.). Questo permette una navigazione agevole della pipeline.
- Ogni fase è pensata come una sotto-analisi. Durante ogni step vengono usati i file presenti nella cartella `dataset` come input/elaborazione intermedia, mentre gli output finali vengono salvati nella cartella `results`.

### Fasi della Pipeline:
1. **Benchmark**: Calcolo della similarità e selezione del modello Sentence-Transformer.
2. **Generazione Embeddings**: Pulizia del dataset ed estrazione degli embeddings delle spiegazioni.
3. **Matrice di Similarità**: Creazione della mappatura e calcolo della *cosine similarity*.
4. **Analisi Quantitativa**: Riduzione dimensionale con UMAP, calcolo dei K-Nearest Neighbors (K-NN) spaziali e relative metriche.
5. **Dashboard Interattiva**: Generazione di una dashboard Plotly per l'esplorazione qualitativa.

---

## Come eseguire il codice

### 1. Requisiti e Dati Iniziali
**ATTENZIONE:** Il modello SAE e il dataset delle spiegazioni (sia quelle manuali che quelle generate da GPT-5) non sono inclusi nella repository[cite: 1]. Prima di avviare il codice, è necessario scaricarli da HuggingFace:
1. **SCARICA IL SAE**: [sae-Minerva-1B-32x](https://huggingface.co/alessandrobondielli/sae-Minerva-1B-32x)
2. **SCARICA IL DATASET**: [EXPLAINITA-task1](https://huggingface.co/datasets/colinglab/EXPLAINITA-task1)

*Nota per gli script `4a_umap.py` e `4b_quantitative_analysis.py`:* Ricorda di inserire all'interno degli script il tuo percorso locale assoluto alla cartella dei pesi del modello SAE nelle variabili `TENSOFILE_PATH` e `SAE_WEIGHTS_PATH`.

### 2. Esecuzione e Risultati Generati
Per eseguire il progetto, lancia gli script Python nel loro ordine numerico (da 1 a 5). 

**AVVISO IMPORTANTE SUI FILE DI OUTPUT:**
Le cartelle `results` degli step 2, 3 e 4 sono state caricate vuote per via dei limiti di peso imposti da GitHub. 

Come indicato nel paper, il file pesante con le parti della matrice di similarità è disponibile su richiesta agli autori.

Tuttavia, **il risultato finale dello Step 5 (la dashboard interattiva HTML) è stato caricato** nella cartella `results` e può essere consultato liberamente senza dover far girare l'intera pipeline.
