# GeoSentinel - Setup Guide

## Complete Package & Dependency List

### Required Python Packages
All packages are listed in `requirements.txt`. Install them with:
```bash
pip install -r requirements.txt
```

**Key packages currently missing (based on error logs):**
- `beautifulsoup4` - Web scraping (bs4 module)
- `sentence_transformers` - ChromaDB embeddings

**To fix immediately:**
```bash
pip install beautifulsoup4 sentence_transformers python-dotenv
```

**Full package list:**
| Package | Purpose | Status |
|---------|---------|--------|
| Flask | Web framework | ✅ |
| Werkzeug | WSGI utilities | ✅ |
| requests | HTTP client | ✅ |
| feedparser | RSS/Atom feeds | ✅ |
| numpy | Numerical computing | ✅ |
| opencv-python-headless | Computer vision | ✅ |
| Pillow | Image processing | ✅ |
| ollama | Local LLM integration | ✅ |
| gTTS | Text-to-speech | ✅ |
| pysocks | SOCKS proxy support | ✅ |
| stem | Tor control | ✅ |
| ultralytics | YOLO object detection | ✅ |
| chromadb | Vector database | ✅ |
| sentence_transformers | Sentence embeddings | ⚠️ Missing |
| beautifulsoup4 | HTML parsing | ⚠️ Missing |
| python-dotenv | Environment variables | ⚠️ NEW - Added for security |

---

## Environment Variables & API Keys Setup

### Step 1: Copy Template File
```bash
cp .env.example .env
```

### Step 2: Edit `.env` File
Open `.env` in your editor and fill in your actual API keys:
```
NEWS_API_KEY=sk_...
TWITTER_API_KEY=your_key...
# etc.
```

### Step 3: Where to Get Keys

#### 📰 NewsAPI (News Headlines)
- **Website:** https://newsapi.org
- **Free Tier:** Yes (100 requests/day)
- **Key Format:** `sk_...`
- **Needed for:** `/news` endpoint, global/regional intelligence

#### 🔄 OpenRouter (LLM API)
- **Website:** https://openrouter.ai
- **Free Tier:** Trial credits available
- **Key Format:** `sk-or-...`
- **Needed for:** AI analysis, text processing

#### 🐦 Twitter/X API
- **Website:** https://developer.twitter.com
- **Requirements:** Apply for API access (elevated access required)
- **Keys Needed:**
  - API Key & Secret
  - Access Token & Secret  
  - Bearer Token
- **Needed for:** Social media monitoring, tweet search

#### 📍 OpenCellID (Cell Tower Data)
- **Website:** https://opencellid.org
- **Free Tier:** Limited requests
- **Key Format:** Long alphanumeric string
- **Needed for:** `/api/geo/towers` endpoint

#### 🤗 Hugging Face (ML Models)
- **Website:** https://huggingface.co/settings/tokens
- **Free Tier:** Yes
- **Key Format:** `hf_...`
- **Needed for:** Local model loading, embeddings

---

## Configuration Files

- **app.py** - Main Flask application (now loads from `.env`)
- **news_config.py** - News sources configuration
- **.env** - Your secret API keys (CREATE THIS)
- **.env.example** - Template for .env file
- **.gitignore** - Prevents committing sensitive files

---

## Quick Start After Setup

```bash
# 1. Install packages
pip install -r requirements.txt

# 2. Copy and configure .env
cp .env.example .env
# Edit .env with your keys

# 3. Run application
python app.py
```

Then access: `http://localhost:5000/earth`

---

## Architecture Overview

**GeoSentinel** is an intelligence platform with:

- **Earth Dashboard** (`/earth`) - Geospatial surveillance grid
- **News Analysis** (`/news`) - Global news intelligence  
- **Web Scanning** (`/api/tools/web_scan`) - Multi-engine scraping
- **Flight Tracking** (`/api/geo/flights`) - Real-time aircraft data (ADS-B)
- **Cell Towers** (`/api/geo/towers`) - Cellular infrastructure mapping
- **Market Data** (`/api/market/data`) - Cryptocurrency tracking
- **Vector Database** - ChromaDB with embeddings (sentence_transformers)

---

## Troubleshooting

**ChromaDB Init Error:**
```bash
pip install sentence_transformers
```

**No module 'bs4':**
```bash
pip install beautifulsoup4
```

**NewsAPI 401 Error:**
- Verify your `NEWS_API_KEY` in `.env` is correct
- Check key isn't expired

**Market Data Connection Error:**
- CoinGecko API requires internet connection
- May be blocked by firewall/proxy

**Scrapers failing (Ahmia/Google/Bing):**
- BeautifulSoup4 missing (see above)
- Requires internet connection
- Tor proxy unavailable (optional, clearnet fallback used)

---

## Security Notes

✅ **DO:**
- Store API keys in `.env` file only
- Add `.env` to `.gitignore` (already done)
- Use `.env.example` as template
- Rotate API keys regularly

❌ **DON'T:**
- Commit `.env` to git
- Hardcode API keys in code
- Share `.env` publicly
- Use placeholder keys in production

---

## Next Steps

1. ✅ Install missing packages
2. ✅ Create `.env` file with your keys
3. ✅ Test API connections
4. 🔧 Implement missing endpoints (`/api/username`, `/log-activity`, `/profiles`)
5. 📊 Configure market data APIs (CoinGecko, etc.)
