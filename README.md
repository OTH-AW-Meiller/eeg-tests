# EEG Tests

## Auswertung eine EEG-Usability-Test-Sesstion

## Bedeutung der Wellenformen

### Alpha-Wellen (hier: Blau)

* Entspannung, innere Ruhe

### Beta-Wellen (hier: Rot)

* geistige Aktivität, Konzentration bis Stress

Dieses Projekt besteht aus zwei Schritten:

1. `gen_report.ipynb` ausfuehren, um die EEG-Auswertung und die benoetigten Ausgabe-Dateien zu erzeugen.
2. `gen_movie.sh` ausfuehren, um den EEG-Streifen auf das Video zu legen.

## Voraussetzungen

Vor dem Start sollten diese Komponenten verfuegbar sein:

- [Anaconda](https://www.anaconda.com/products/distribution) fuer die Python-Umgebung
- Python-Paket `reportlab`
- `ffmpeg` inklusive `ffprobe` fuer das Zusammenbauen des Videos
- Jupyter oder VS Code, um das Notebook `gen_report.ipynb` auszufuehren

Falls `reportlab` fehlt, kann es zum Beispiel mit `conda` installiert werden:

```bash
conda install -c conda-forge reportlab
```

### ffmpeg installieren

`ffmpeg` wird fuer das Video-Skript benoetigt. Die Installation unterscheidet sich je nach Betriebssystem:

- macOS:

```bash
brew install ffmpeg
```

- Linux (Debian/Ubuntu):

```bash
sudo apt update
sudo apt install ffmpeg
```

- Linux (Fedora):

```bash
sudo dnf install ffmpeg
```

- Windows:
	- Mit Chocolatey:

```powershell
choco install ffmpeg
```

	- Mit Scoop:

```powershell
scoop install ffmpeg
```

Nach der Installation sollten `ffmpeg` und `ffprobe` im Terminal bzw. in PowerShell verfuegbar sein.

## Benoetigte Eingabedateien

Vor dem Start muessen diese Dateien im Projektverzeichnis liegen:

- `data/eeg_data.txt`
- `movie.mp4`

Die Ordnerstruktur sollte also so aussehen:

```text
eeg_tests/
├── data/
│   └── eeg_data.txt
├── output/
│   └── ...
├── gen_report.ipynb
├── gen_movie.sh
└── movie.mp4
```

## 1. Report-Notebook ausfuehren

Das Notebook heisst in diesem Workspace `gen_report.ipynb`.

Oeffne es in VS Code oder in Jupyter und fuehre alle Zellen aus.

Beispiel fuer die Ausfuehrung in einem Jupyter-Umfeld:

```bash
jupyter notebook gen_report.ipynb
```

Nach dem Lauf erzeugt das Notebook unter anderem diese Datei:

- `output/EEG_Liniengrafik_Streifen.png`

## 2. Video erzeugen

Wenn das Notebook fertig ist, das Skript ausfuehren:

```bash
./gen_movie.sh
```

Das Skript verwendet standardmaessig:

- Eingabevideo: `movie.mp4`
- EEG-Streifen: `output/EEG_Liniengrafik_Streifen.png`
- Ausgabevideo: `output/movie_with_eeg_strip.mp4`

## Optional: Eigene Dateinamen verwenden

Falls die Dateien anders heissen, koennen sie als Argumente uebergeben werden:

```bash
./gen_movie.sh <video-datei> <strip-png> <ausgabe-video>
```

Beispiel:

```bash
./gen_movie.sh film.mp4 output/EEG_Liniengrafik_Streifen.png output/mein_video.mp4
```

## Hinweise

- Das Skript bricht ab, wenn `movie.mp4` oder die PNG-Datei fehlt.
- Der Ordner `output/` wird bei Bedarf automatisch angelegt.
