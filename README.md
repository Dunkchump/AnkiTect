# 🇩🇪 AnkiTect: Intelligent Anki Deck Generator

> Transform your vocabulary list into beautiful, multimedia-rich Anki decks in seconds. AnkiTect automates card generation, audio synthesis, and image fetching with adaptive performance optimization.

**Supported Languages:** English (EN), German (DE), Ukrainian (UK)

---

## ✨ Key Features

### 🎯 **Smart Card Generation**

- **Neural Text-to-Speech** - Microsoft Edge-TTS with 4+ voice options per language
- **4 Card Templates** - Recognition (flashcard), Production (cloze), Listening (audio-first), Context (sentence-based)
- **Rich Metadata Support** - Etymology, morphology, mnemonics, analogues, contextual examples
- **Multilingual** - Supports 14+ languages with per-language configuration

### ⚡ **Blazing Fast Performance**

- **Adaptive Parallelization** - Auto-adjusts worker threads based on server response (1-8 concurrent)
- **Smart Caching** - JSON cache eliminates re-downloading (2x faster on rebuild)
- **Intelligent Retry** - Exponential backoff with jitter avoids API rate limiting
- **Real-time Progress** - TQDM progress bar with ETA and per-item speed metrics
- **Benchmark:** 54 words in ~2 minutes with full audio + images (cached)

### 🎨 **Beautiful Card Design**

- **Glassmorphism CSS** - Modern frosted-glass effect with gradients
- **Gender-Color Coding** - der (blue), die (red), das (green), no-article (purple)
- **Responsive** - Works perfectly on Anki Desktop, AnkiDroid, AnkiWeb
- **High Contrast** - WCAG AAA compliant typography

### 💾 **Robust Data Management**

- **Auto-Backups** - Timestamped backups with automatic cleanup (keeps last 3)
- **Build Statistics** - Download success rates, file sizes, execution time
- **CSV Validation** - Detailed error messages for malformed input
- **Language Switching** - Change language with one config variable

---

## 📋 System Requirements

- **Python 3.11+** (tested on 3.13.1)
- **Anki 2.1+** (for desktop) or AnkiDroid (for mobile)
- **Internet connection** (for TTS generation and image fetching)
- **~50MB free disk space** (for typical 100-word deck)

---

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/ankitect.git
cd ankitect
```

### 2. Create Virtual Environment (Recommended)

```bash
python -m venv .venv

# Windows
.venv\Scripts\activate

# macOS/Linux
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 📖 Quick Start (5 Minutes)

### Step 1: Prepare Data

Create `vocabulary.csv` (pipe-separated, UTF-8 encoding):

```csv
TargetWord|Meaning|IPA|Part_of_Speech|Gender|Morphology|Nuance|ContextSentences|ContextTranslation|Etymology|Mnemonic|Analogues|Image|Tags
rustling|a soft whispering sound|/ˈrʌslɪŋ/|Noun|none|-|Sound of dry leaves or paper|1. He heard <b>rustling</b> in the bushes.<br>2. The <b>rustling</b> of papers.|1. Він почув шурхіт у кущах.<br>2. Шелест паперів.|From Proto-Germanic|Rhymes with "hustle" - both imply movement|EN: whisper, crinkle<br>DE: Rascheln|https://image.pollinations.ai/prompt/dry%20leaves%20wind?width=320&height=200|Noun B2
```

### Step 2: Install & Configure

```bash
# Clone repo
git clone https://github.com/yourusername/ankitect.git
cd ankitect

# Create virtual environment
python -m venv .venv
.venv\Scripts\activate  # Windows
# source .venv/bin/activate  # macOS/Linux

# Install dependencies
pip install -r requirements.txt
```

### Step 3: Run Build

```bash
python build_deck.py
```

**Output:**

```
🎤 Voice Selected: en-GB-SoniaNeural
📚 Processing 4 words...

Building deck: 100%|██████████| 4/4 [00:12<00:00, 3.12s/word]

💾 Backup: ankitect_en_20251225_151159.apkg

============================================================
✨ BUILD STATISTICS
============================================================
✅ Words processed:        4
📸 Images downloaded:      4/4 (100%)
🎵 Word audio:             4/4 (100%)
🎧 Sentence audio:         12/12 (100%)
⏱️  Total time:            12.5 sec
📦 Media size:             1.2 MB
💾 Deck file:              ankitect_en.apkg
============================================================
```

### Step 4: Import to Anki

**Desktop Anki:**

1. File → Import... → Select `ankitect_en.apkg`

**AnkiDroid (Mobile):**

1. Menu → Import → Select file
   | Etymology | ❌ | Word origin |
   | Mnemonic | ✅ | Memory hook |
   | Analogues | ❌ | Similar words (EN: word / DE: wort) |
   | Image | ❌ | Image URL or prompt |
   | Tags | ❌ | Space-separated tags |

### 2. Run the Build Script

```bash
python build_deck.py
```

**Output Example:**

```
🎤 Voice Selected: de-DE-ConradNeural
🌍 Mode: DE
🎲 Shuffling words...
📚 Processing 54 words...

Building deck: 100%|██████████████████| 54/54 [01:56<00:00, 2.15s/word]

💾 Резервна копія: system_zero_de_20251225_151159.apkg

============================================================
✨ СТАТИСТИКА ЗБИРАННЯ КОЛОДИ
============================================================
✅ Слова обрані:              54
📸 Зображення завантажені:   54/54 (100.0%)
🎵 Аудіо слів завантажені:   54/54 (100.0%)
🎧 Аудіо речень завант.:     162/162 (100.0%)
⏱️  Час виконання:            1м 59с
📦 Розмір медіа:              2.6 МБ
💾 Розмір файлу:             2.8 МБ
📝 Файл створено:            system_zero_de.apkg
============================================================
```

### 3. Import into Anki

**Desktop Anki:**

1. Open Anki → File → Import...
2. Select `ankitect_de.apkg`
3. Click "Import" button

**AnkiDroid (Mobile):**

1. Open AnkiDroid → Menu → Import
2. Select the `.apkg` file
3. Tap "Import"

---

## 📚 CSV Format Reference

**Required columns (must be present):**

| Column                 | Description                               | Example                            |
| ---------------------- | ----------------------------------------- | ---------------------------------- |
| **TargetWord**         | The word/phrase to learn                  | `rustling` or `der Baum`           |
| **Meaning**            | Short definition                          | `a soft whispering sound`          |
| **IPA**                | Pronunciation in IPA notation             | `/ˈrʌslɪŋ/`                        |
| **Part_of_Speech**     | Grammatical category                      | `Noun`, `Verb`, `Phrasal Verb`     |
| **Gender**             | (DE) `der`/`die`/`das`, (EN) `none`       | `der`, `die`, `das`, `none`        |
| **ContextSentences**   | 3 example sentences (separated by `<br>`) | `1. Text<br>2. Text<br>3. Text`    |
| **ContextTranslation** | Translations of sentences                 | `1. Текст<br>2. Текст<br>3. Текст` |

**Optional columns (nice to have):**

| Column     | Description                         | Example                                         |
| ---------- | ----------------------------------- | ----------------------------------------------- |
| Morphology | Grammar inflections                 | `Pl: -e`, `Past: -ed`                           |
| Nuance     | Usage context/connotation           | `Archaic`, `Formal`, `Slang`                    |
| Etymology  | Word origin story                   | `From Proto-Germanic *wurdiz`                   |
| Mnemonic   | Memory aid/trick                    | `Think of "hustle" - both suggest movement`     |
| Analogues  | Similar words in multiple languages | `EN: whisper<br>DE: Rascheln<br>UA: шелестіння` |
| Image      | Image URL (PNG/JPG)                 | `https://image.pollinations.ai/...`             |
| Tags       | Space-separated Anki tags           | `Noun B2 Sound`                                 |

**Important notes:**

- Use `|` (pipe) as column separator, not commas
- Use UTF-8 encoding (save in VS Code with UTF-8 encoding)
- Use `<br>` to separate multiple sentences (not newlines)
- Wrap important words in `<b>text</b>` for bold
- Remove or leave empty optional columns (don't delete the column header)

---

## ⚙️ Configuration

Edit `build_deck.py` - look for the `Config` class:

```python
CURRENT_LANG = "EN"        # Switch between: EN, DE, UK (Ukrainian)
CONCURRENCY = 4            # Parallel workers (1-8, auto-adjusts)
RETRIES = 5                # Retry failed downloads
TIMEOUT = 60               # Request timeout (seconds)
IMAGE_TIMEOUT = 90         # Image generation timeout
REQUEST_DELAY_MIN = 0.5    # Minimum delay between requests
REQUEST_DELAY_MAX = 3.5    # Maximum delay between requests
```

**Recommended settings by use case:**

| Use Case                    | CONCURRENCY | RETRIES | TIMEOUT |
| --------------------------- | ----------- | ------- | ------- |
| Small test (< 10 words)     | 2           | 3       | 45s     |
| Normal build (10-100 words) | 4           | 5       | 60s     |
| Large build (> 100 words)   | 6-8         | 7       | 90s     |
| Unstable network            | 1           | 7       | 120s    |

```python
# Language selection
CURRENT_LANG = "DE"  # or "EN"

# Performance tuning
CONCURRENCY = 4                    # Parallel downloads (1-8 recommended)
RETRIES = 5                        # Retry attempts (3-7)
TIMEOUT = 60                       # General timeout in seconds
IMAGE_TIMEOUT = 90                 # Image generation timeout
REQUEST_DELAY_MIN = 0.5            # Min delay between requests
REQUEST_DELAY_MAX = 3.5            # Max delay between requests
```

---

## 📊 Performance Benchmarks

**Test environment:** Windows 11, Python 3.13, 54-word English vocabulary, average internet

| Scenario             | Time    | Speed            | Notes                                 |
| -------------------- | ------- | ---------------- | ------------------------------------- |
| **First build**      | ~23 min | Baseline         | Generates all audio + images          |
| **Rebuild (cached)** | ~2 min  | **11.5x faster** | Uses JSON cache + file system         |
| **Per-word speed**   | 2.15s   | -                | With adaptive parallelization enabled |
| **Success rate**     | 100%    | -                | All images + audio words + sentences  |
| **File size**        | 2.8 MB  | -                | For 54 words with full media          |

**What makes it fast:**

1. **Caching** - Checks if file already exists before downloading
2. **Parallelization** - Downloads multiple images/audio simultaneously
3. **Adaptive scaling** - Auto-reduces workers when server rate-limits
4. **Jitter** - Random delays prevent server blocking

System automatically optimizes concurrency:

- Detects HTTP 429 (too many requests) → reduces parallelization by 50%
- Detects 5+ successful requests → doubles parallelization
- Adapts to server capacity in real-time
- Progress bar shows current concurrency level

### Smart Caching

- Downloads cached in `build_cache.json`
- Prevents redundant API calls
- ~2x faster on re-runs
- Automatic cache validation

### Automatic Backups

- Timestamped backups: `system_zero_de_20251225_151159.apkg`
- Keeps last 3 versions automatically
- No data loss on script re-run
- Easy rollback to previous versions

---

## � How It Works (Under the Hood)

```
vocabulary.csv
    ↓ (pandas reads)
    ↓
Extract fields → Generate TTS → Download images
    ↓
Create 4 card templates (Recognition, Production, Listening, Context)
    ↓
Genanki packages everything → Anki .apkg file
    ↓
ankitect_en.apkg (ready to import)
```

**Processing per word:**

1. Read row from CSV
2. Generate audio (TTS) for word + 3 context sentences
3. Download image (from URL or generate)
4. Create 4 card variants with HTML/CSS
5. Add to Anki deck
6. Cache file hashes to skip on re-run

**Parallelization logic:**

- Default: 4 concurrent downloads
- Server returns 429? → Reduce to 2
- 5 successful requests? → Increase to 8
- Each worker processes one word until completion

---

## 📁 Generated Files

After running `python build_deck.py`:

```
.
├── ankitect_en.apkg              # Your deck (import this!)
├── ankitect_en_20251225_*.apkg   # Backups (auto-deleted after 3)
├── build_cache.json              # What's been downloaded
└── media/                        # Downloaded audio/images
    ├── _word_xxx.mp3            # Word pronunciation
    ├── _sent_xxx.mp3            # Sentence audio
    └── _img_xxx.jpg             # Word images
```

---

## 🐛 Troubleshooting

**Problem: "ModuleNotFoundError: No module named 'tqdm'"**

```bash
pip install tqdm
```

**Problem: "HTTP 429: Too Many Requests"**

This is normal! The system automatically:

- Detects 429 errors
- Reduces parallel workers
- Prints warning: `⚠️ 429 - Reducing concurrency`
- Retries with exponential backoff

Solution: Increase `REQUEST_DELAY_MAX` in config if persistent.

**Problem: Images not downloading**

- Verify image URL is complete in CSV
- Check internet connection
- Ensure `media/` folder has write permissions
- Look at error in console output

**Problem: "Timeout during image generation"**

- Pollinations AI might be slow
- Increase `IMAGE_TIMEOUT` in config (try 120 seconds)
- Try running at off-peak hours

**Problem: CSV file errors**

- Ensure pipe-separated: `|` not `,`
- Save as UTF-8 encoding (VS Code: bottom right corner)
- Check for missing required columns
- Validate 14 total columns match header

---

## 🤝 Contributing

Found a bug? Have ideas? We'd love your help!

**Report bugs:**

- Check [existing issues](../../issues) first
- Include: steps to reproduce, CSV sample, error output, Python version

**Suggest features:**

- Open a [discussion](../../discussions)
- Feature ideas: French support, web UI, database backend, mobile app

**Submit code:**

1. Fork the repo
2. `git checkout -b feature/my-feature`
3. Make changes
4. `git commit -am 'Add feature description'`
5. `git push origin feature/my-feature`
6. Open Pull Request

## 📜 License

MIT License - See [LICENSE](LICENSE) file for full text

```
MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files...
```

---

## 🙏 Credits & Acknowledgments

- **Genanki** - For Anki deck generation
- **Edge-TTS** - For neural text-to-speech
- **Pollinations AI** - For image generation
- **Anki Community** - For the learning platform
- **All contributors** - For feedback and improvements

---

## 📈 Roadmap

### v61.2 (Q1 2026)

- [ ] Multi-language UI (German, Ukrainian, Russian)
- [ ] Web dashboard
- [ ] Custom CSS themes
- [ ] French language pack

### v62.0 (Q2 2026)

- [ ] PostgreSQL database backend
- [ ] Cloud sync support
- [ ] Mobile companion app
- [ ] Spaced repetition analytics

---

## 💬 Support & Community

- **Issues & Bugs:** [GitHub Issues](../../issues)
- **Questions:** [GitHub Discussions](../../discussions)
- **Anki Forum:** [ankiweb.net](https://ankiweb.net)

---

**Built with ❤️ for language learners worldwide**

_Last updated: December 25, 2025_
