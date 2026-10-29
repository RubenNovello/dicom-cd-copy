# DICOM CD COPY

# 💿 dicom-cd-copy

**Copia in un solo comando il CD/DVD di un esame radiologico (TC, RM…) sul tuo PC Linux, pronto da aprire in [3D Slicer](https://www.slicer.org/).**

![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?logo=ubuntu&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?logo=gnubash&logoColor=white)
![DICOM](https://img.shields.io/badge/DICOM-3D%20Slicer-blue)

## Perché

I dischi che gli ospedali consegnano contengono i file DICOM e un visualizzatore per Windows o macOS. Su Linux leggerli direttamente dal lettore è lento e scomodo, e con l'**Apple USB SuperDrive** il disco spesso viene addirittura respinto.

`copia-dicom` monta il disco, copia tutto in una cartella sul PC con barra di avanzamento ed espelle il disco a fine copia.

## Requisiti

- Ubuntu o altra distribuzione Linux con `udisks2` (già presente su Ubuntu Desktop)
- `rsync` ed `eject`
- Un lettore ottico, anche l'Apple USB SuperDrive (vedi la sezione dedicata)

## Installazione

```bash
sudo apt install rsync eject
mkdir -p ~/.local/bin
curl -fsSL https://raw.githubusercontent.com/RubenNovello/dicom-cd-copy/main/copia-dicom \
  -o ~/.local/bin/copia-dicom
chmod +x ~/.local/bin/copia-dicom
```

Se il comando non viene trovato, riapri il terminale: `~/.local/bin` entra nel `PATH` al login.

## Uso

Inserisci il disco e scrivi:

```bash
copia-dicom
```

Lo script:

1. monta il disco, se non lo è già;
2. crea la cartella `~/dicom_<ETICHETTA>_<DATA>`;
3. copia tutto con `rsync`, mostrando percentuale e velocità;
4. sincronizza i dati ed espelle il disco.

Se la copia si interrompe, rilancia lo stesso comando: `rsync` salta i file già copiati.

> ⏱️ Un CD/DVD letto via USB va a circa 1 MB/s: per ~1 GB servono 15-25 minuti.

## Aprire l'esame in 3D Slicer

1. Apri 3D Slicer e vai nel modulo **DICOM** → **Import DICOM files**.
2. Scegli la cartella creata da `copia-dicom` e premi **Import**.
3. Seleziona la serie che ti interessa e clicca **Load**. Di solito è quella con più immagini e fetta più sottile.
4. Per il 3D apri **Volume Rendering**, attiva l'occhio e scegli un preset (ad esempio `CT-Cardiac3` o `CT-Bone`).

Avvisi
