# 🎛️ Musica Applicata — Advanced Audio Engineering & DSP Suite

Workspace master contenente la suite integrata di software per la produzione musicale, la diagnostica elettroacustica, l'elaborazione del segnale digitale (DSP), l'analisi forense e la conformità broadcast.

Ogni sottoprogetto è mantenuto in un repository GitHub indipendente collegato a questo repository master tramite **Git Submodules**.

---

## 📦 Panoramica dei Progetti

| Progetto | Tipologia / Formato | Stack Tecnologico | Repository GitHub |
| :--- | :--- | :--- | :--- |
| **PrecisionAudioLab** | Plugin VST3 & Standalone | C++20, JUCE 8 | [muccio/PrecisionAudioLab](https://github.com/muccio/PrecisionAudioLab) |
| **SpectraCross** | Plugin AU & VST3 | C++20, JUCE 8 | [muccio/spectracross](https://github.com/muccio/spectracross) |
| **StudioSpec Pro** | Desktop App Standalone | Python, CoreAudio HAL, PySide6 | [muccio/StudioSpec-Pro](https://github.com/muccio/StudioSpec-Pro) |
| **AudioScope** | Desktop App Standalone | Python, PySide6, PyAV/FFmpeg | [muccio/AudioScope](https://github.com/muccio/AudioScope) |
| **FilterLab** | Desktop App Standalone | Python, PySide6, SciPy, PortAudio | [muccio/FilterLab](https://github.com/muccio/FilterLab) |

---

### 1. [PrecisionAudio Lab 🔬](https://github.com/muccio/PrecisionAudioLab)
*Suite di generazione segnali di test e analisi elettroacustica avanzata*
- **Generatore di Segnali di Precisione:** Oscillatori a sintesi anti-aliased (PolyBLEP & PolyBLAMP), sweep sinusoidale continuo di fase (lineare/logaritmico), sorgenti di rumore White (Gauss/Uniform), Pink (-3 dB/oct), Brown (-6 dB/oct), Grey (ISO 226), burst, delta di Dirac e toni per distorsione d'intermodulazione (IMD SMPTE / CCIF).
- **Architettura Real-Time:** Zero allocazioni dinamiche sul thread audio (`processBlock`), anelli di memoria SPSC lock-free e rendering vettoriale disaccoppiato a 60 fps.
- **Metriche e Misure:** True Peak oversampling 4x, ITU-R BS.1770 LUFS (Integrated, Short-Term, Momentary), goniometro lissajous vettoriale, calibrazione dBu/dBFS.

### 2. [SpectraCross 🎛️](https://github.com/muccio/spectracross)
*Surgical Multi-Instance Spectral Analyzer & Masking Engine*
- **Analisi Spettrale Multi-Traccia:** Visualizzazione simultanea e comparativa dello spettro di frequenza su più istanze di tracce nella DAW.
- **Motore di Unmasking Psicoacustico:** Mappatura su 24 bande critiche di Bark secondo il modello di Traunmüller con coefficiente di spreading spettrale per identificare mascheramenti frequenziali e conflitti timbrici.
- **DSP Engine:** Architettura lock-free a thread dedicato con FFT configurabile a 2048, 4096 e 8192 punti, curve di tilt EQ (Flat, +3 dB, +4.5 dB pinking, +6 dB) e balistica d'inviluppo d'attacco/rilascio regolabile.

### 3. [StudioSpec Pro 💻](https://github.com/muccio/StudioSpec-Pro)
*Audio Workstation Inspector, Driver Diagnostic & Kontakt DFD Benchmark*
- **Diagnostica CoreAudio HAL a Basso Livello (macOS):** Ispezione nativa via C/ctypes dei dispositivi audio, buffer ranges, frequenze di campionamento supportate, safety offsets e stima precisa della latenza Round-Trip (RTL).
- **Scansione Driver & Bundles:** Identificazione dei driver installati in `/Library/Audio/Plug-Ins/HAL` e determinazione del bus di trasporto (Thunderbolt, PCIe, USB Class 2.0, Dante/Ravenna AoIP).
- **Kontakt DFD Disk Benchmark:** Analisi ad alta precisione del throughput e dei tempi di accesso a blocchi casuali da 64 KB per la stima del numero massimo di voci/patch simultanee gestibili dal motore Direct-From-Disk di Native Instruments Kontakt.
- **Scoring Engine:** Algoritmo ponderato su 4 categorie con attribuzione punteggio in centesimi (0–100) e classificazione Tier (*Tier S+ Elite, Tier A Pro, Tier B Advanced, Tier C Home Studio*).

### 4. [AudioScope 🔍](https://github.com/muccio/AudioScope)
*Universal Audio File Inspector & Broadcast Loudness Analyzer*
- **Universal Container Demuxing & Decoding:** Decodifica e scomposizione di formati audio broadcast e standard (BWF, RF64, AIFF, FLAC, ALAC, MP3, OGG, Opus, AAC, CAF, DSD/DSF) tramite PyAV (librerie FFmpeg C-API).
- **Virtualized Zero-Copy Hex Viewer:** Lettore esadecimale virtualizzato basato su memoria mappata (`mmap`), capace di scorrere istantaneamente file di decine di gigabyte a zero consumo di RAM, con ricerca pattern binari/ASCII.
- **Parser Gerarchico dei Chunk:** Navigazione interattiva della struttura ad albero per RIFF (`fmt `, `bext`, `iXML`, `cart`, `data`), AIFF (`COMM`, `SSND`), metadati broadcast EBU Tech 3285 BEXT, iXML produzione cinematografica e box MPEG-4.
- **Broadcast Loudness Suite (ITU-R BS.1770-4 / EBU R128):** Misurazione True Peak con oversampling 4x (dBTP), Loudness Range (LRA, EBU Tech 3342), LUFS integrato con doppio gating (-70 LKFS assoluto e -10 LU relativo).

### 5. [FilterLab 🎛️](https://github.com/muccio/FilterLab)
*Digital Filter & EQ Didactic Lab — Laboratorio Interattivo sui Filtri Digitali per macOS & Windows*
- **Percorso Didattico Completo (10 Moduli + Quiz — Slide 1–18):** Spiegazione interattiva di filtri digitali come *blackbox* e campioni discreti ($\Delta t$), LowPass, HighPass, BandPass, BandReject (media geometrica $f_c = \sqrt{f_L \cdot f_H}$), Quality Factor ($Q$), *ringing* sui transienti, ordine/roll-off Butterworth (6/12/24 dB/oct), Moog Ladder, connessione in serie/parallelo, banchi modulati, EQ Grafica ISO (10/20/30 bande), Shelving/Peak/Notch/EQ Parametrico e Channel Strip (mandate Aux Pre/Post-Fader, Fader nominale, PFL, Pan-Pot).
- **Laboratorio Pratico Real-Time (4 Workbench):** *Singolo Filtro*, *Serie/Parallelo/Banco*, *EQ Grafica ISO* ed *EQ Parametrica* con grafico Bode interattivo a nodi trascinabili, spettro FFT Pre/Post live, risposta all'impulso $h[n]$, oscilloscopio e vista campioni Blackbox.
- **Sorgenti Interne ed Esterne:** Generatore multi-segnale (Rumore Bianco/Rosa, Impulsi, Saw/Square PolyBLEP, Sinusoide, Sweep Logaritmico, Accordo Synth), player file audio (`WAV`, `AIFF`, `FLAC`, `OGG`, `MP3`, `M4A`) con seek waveform e ingresso Microfono Live full-duplex.

---

## 🚀 Guida all'Utilizzo del Repository Master

### Clonazione con Submoduli

Per clonare questo repository master scaricando contemporaneamente tutto il codice sorgente di tutti i sottoprogetti:

```bash
git clone --recurse-submodules https://github.com/muccio/_MUSICA_APPLICATA.git
```

Se il repository è già stato clonato senza submoduli, inizializzarli ed aggiornarli con:

```bash
git submodule update --init --recursive
```

### Aggiornamento dei Submoduli alle Ultime Versioni

Per allineare tutti i submoduli all'ultimo commit dei rispettivi branch remoti:

```bash
git submodule update --remote --merge
```

---

## 📄 Licenze

Ogni sottoprogetto è regolato dalla propria licenza specifica consultabile nelle rispettive cartelle e repository dedicati.

