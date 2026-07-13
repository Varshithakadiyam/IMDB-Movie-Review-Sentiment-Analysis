# IMDB Sentiment Analysis - Streamlit Deployment Guide

## Local Development

### 1. Setup Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 2. Install Dependencies
```bash
pip install -r streamlit_requirements.txt
```

### 3. Run Locally
```bash
streamlit run app.py
```
The app will be available at `http://localhost:8501`

---

## Deployment Options

### Option 1: Streamlit Cloud (Recommended)
**Free, easiest deployment**

1. Push your repository to GitHub
2. Go to [Streamlit Cloud](https://streamlit.io/cloud)
3. Click "Deploy an app"
4. Connect your GitHub repository
5. Select the main branch and `app.py`
6. Deploy!

**Required files:**
- `app.py` ✓
- `requirements.txt` or `streamlit_requirements.txt` ✓
- `.streamlit/config.toml` ✓

### Option 2: Heroku (Free tier no longer available)
Use [Heroku alternative services](https://www.heroku.com/alternatives)

### Option 3: Railway.app
1. Sign up at [Railway.app](https://railway.app)
2. Connect GitHub repository
3. Railway auto-detects Python and runs `Procfile`
4. Add environment variables if needed
5. Deploy!

### Option 4: AWS EC2
1. Launch Ubuntu EC2 instance
2. SSH into instance
3. Clone repository
4. Install Python and dependencies
5. Run: `streamlit run app.py --server.port=80 --server.address=0.0.0.0`
6. Use screen/tmux to keep it running

### Option 5: Docker
```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY streamlit_requirements.txt .
RUN pip install -r streamlit_requirements.txt
COPY . .
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

---

## Important Notes

⚠️ **Data Files**: Ensure these files are in the repository:
- `IMDB Dataset.csv`
- `lstm_sentiment.keras` (trained model)
- `tokenizer.pkl`
- `label_encoder.pkl`

⚠️ **Large Files**: GitHub has a 100MB file size limit. If your model/data exceeds this:
- Use [Git LFS](https://git-lfs.com/)
- Or download files during app initialization from cloud storage

⚠️ **Secrets Management**: Never commit API keys. Use Streamlit secrets:
- Local: `.streamlit/secrets.toml`
- Cloud: Use Streamlit Cloud UI settings

---

## Troubleshooting

**Module not found errors:**
```bash
pip install -r streamlit_requirements.txt
```

**Port already in use:**
```bash
streamlit run app.py --server.port=8502
```

**Memory issues on deployment:**
- Reduce dataset size
- Use model quantization
- Implement lazy loading

**Slow predictions:**
- Enable GPU if available
- Cache model after first load
- Optimize input preprocessing
