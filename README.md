# LinkedIn Jobs Scraper 🤖

**Daily LinkedIn jobs scraper for Innovation Manager, Innovation Incubator Manager roles in Portugal.**

Automated web scraping with Playwright, email notifications, and Docker support.

## 📋 Features

- ✅ **Multi-term search**: Searches for "Gestor de Inovação", "Gestor de Incubadora", "Innovation Manager"
- ✅ **Portugal-focused**: Filters results for Portugal only
- ✅ **Daily automation**: APScheduler runs daily at configurable times
- ✅ **Email notifications**: Sends new jobs via email
- ✅ **JSON persistence**: Saves job data locally
- ✅ **Docker support**: Run anywhere with Docker/Docker Compose
- ✅ **No API key required**: Uses Playwright for web scraping
- ✅ **Duplicate detection**: Avoids notifying about jobs already seen

## 🚀 Quick Start

### Option 1: Docker Compose (Recommended)

```bash
git clone https://github.com/ramcses-ctrl/linkedin-jobs-scraper.git
cd linkedin-jobs-scraper

# Copy and edit .env
cp .env.example .env
# Edit .env with your email settings

# Run with Docker Compose
docker-compose up -d
```

### Option 2: Local Python

```bash
git clone https://github.com/ramcses-ctrl/linkedin-jobs-scraper.git
cd linkedin-jobs-scraper

pip install -r requirements.txt

# Copy and edit .env
cp .env.example .env

# Run
python main.py
```

## ⚙️ Configuration

Edit `.env` file:

```env
# Email Configuration
SMTP_SERVER=smtp.gmail.com
SMTP_PORT=587
EMAIL_FROM=your-email@gmail.com
EMAIL_PASSWORD=your-app-password  # Use app-specific password for Gmail
EMAIL_TO=recipient@example.com

# Search Parameters
SEARCH_TERMS=Gestor de Inovação,Gestor de Incubadora,Innovation Manager
LOCATION=Portugal

# Scheduler
SCHEDULE_TIME=09:00  # Daily run time (HH:MM format, 24h)
SCHEDULE_TIMEZONE=Europe/Lisbon

# Browser
HEADLESS=true  # Set to false to see browser
BROWSER_TIMEOUT=30000  # ms
```

## 📁 Project Structure

```
.
├── main.py                 # Entry point
├── scraper.py              # Playwright scraper logic
├── email_notifier.py       # Email sending
├── requirements.txt        # Python dependencies
├── Dockerfile              # Docker image
├── docker-compose.yml      # Docker Compose config
├── .env.example            # Example env file
├── README.md               # This file
└── data/
    └── jobs.json           # Saved jobs
```

## 🔍 How It Works

1. **Scraping**: Uses Playwright to access LinkedIn Jobs
2. **Filtering**: Searches for specified terms in Portugal
3. **Deduplication**: Checks if job URL already exists
4. **Email**: Sends new jobs via SMTP
5. **Storage**: Saves to JSON for tracking
6. **Scheduling**: Runs daily via APScheduler

## 📧 Email Setup (Gmail Example)

1. Enable 2-Factor Authentication on your Google Account
2. Generate an [App Password](https://myaccount.google.com/apppasswords)
3. Copy the 16-char password to `.env` as `EMAIL_PASSWORD`
4. Use `gmail.com` as `SMTP_SERVER`

## 🐳 Docker Usage

```bash
# Build image
docker build -t linkedin-scraper .

# Run container
docker run --env-file .env -v $(pwd)/data:/app/data linkedin-scraper

# With Docker Compose
docker-compose up --build
```

## 🛠️ Development

```bash
# Install dev dependencies
pip install -r requirements.txt

# Run with debug logging
export DEBUG=true
python main.py

# Test email sending
python -c "from email_notifier import test_email; test_email()"
```

## ⚠️ Important Notes

- **LinkedIn Rate Limiting**: Adds random delays to avoid detection
- **First Run**: May take 5-10 minutes for initial setup
- **Email Limits**: Gmail free tier has rate limits (check your account)
- **Data Persistence**: Jobs are saved in `data/jobs.json`

## 🔗 LinkedIn URL Format

Used to construct search URLs:
```
https://www.linkedin.com/jobs/search/?keywords={term}&location={location}&geoId=100364837
```

## 📊 Output Example

Email will contain:
- Job title
- Company name
- Location
- Job URL
- Posted date
- Brief description

## 🐛 Troubleshooting

**"No jobs found"**: Check if search terms are correct and LinkedIn structure hasn't changed

**Email not sending**: Verify SMTP credentials and that 2FA/App Password is set up

**Playwright timeout**: Increase `BROWSER_TIMEOUT` in .env

**Permission denied (data/)**: Ensure `data/` folder has write permissions

## 📝 Logs

Logs are printed to stdout/stderr. For Docker, view with:

```bash
docker-compose logs -f scraper
```

## 🔄 Scheduling Examples

```env
# Run every day at 9 AM
SCHEDULE_TIME=09:00

# Run every weekday at 8 AM
SCHEDULE_CRON=0 8 * * 1-5
```

## 📄 License

MIT - Feel free to modify and redistribute

## ⭐ Contributing

Contributions welcome! Submit PRs or issues on GitHub.

## 🤝 Support

For issues, suggestions, or questions, open an issue on GitHub.

---

**Made with ❤️ for innovation professionals in Portugal**
