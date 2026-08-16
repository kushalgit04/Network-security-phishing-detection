# Network Security: Phishing URL Detection 🛡️

**Status:** Early Stage — Work in Progress

> **Learning project — early stage.** I built this while following an MLOps-style tutorial for structuring an ML pipeline (data → MongoDB → training → deployment), and I'm extending it further on my own as I go. This is an early-stage build, not a finished project yet — see [Project Status](#-project-status) below for what's built vs. what's next.

An MLOps pipeline that classifies whether a website URL is **phishing or legitimate**, based on 30 URL/domain-based features (SSL state, domain age, use of IP address instead of domain, presence of suspicious redirects, etc.). Raw data is pushed to MongoDB as the pipeline's data source, with the rest of the pipeline (ingestion → transformation → training → serving) being built out component by component.

---

## 📊 Dataset
- **11,055 rows** × **30 features** + 1 target column (`Result`)
- Features are derived from URL/website properties, e.g. `having_IP_Address`, `SSLfinal_State`, `age_of_domain`, `Abnormal_URL`, `Iframe`, `Google_Index`
- Target: `Result` → `1` = legitimate, `-1` = phishing (6,157 legitimate / 4,898 phishing — roughly balanced)

---

## Architecture (Planned)

```
phisingData.csv
      │
      ▼
push_data.py  →  loads CSV, converts to JSON records, pushes to MongoDB Atlas
      │
      ▼
[Data Ingestion]        ← reads from MongoDB, splits train/test        (in progress)
      │
      ▼
[Data Transformation]   ← cleaning, encoding, scaling                  (planned)
      │
      ▼
[Model Trainer]          ← trains + evaluates classification model      (planned)
      │
      ▼
[Deployment]              ← Docker container, API/web serving            (planned)
```

## 📁 Repository Structure

```
.
├── net_security/
│   ├── components/
│   │   └── data_ingestion.py       # (stub — not yet implemented)
│   ├── entity/
│   │   └── config_entity.py        # (stub — not yet implemented)
│   ├── constants/
│   ├── exception/
│   │   └── exception.py            # custom exception handling
│   ├── logging/
│   │   └── logger.py               # timestamped file logging
│   ├── cloud/
│   └── utils/
├── Network_data/
│   └── phisingData.csv             # raw dataset
├── push_data.py                    # ETL: CSV → MongoDB
├── test_mongo.py                   # MongoDB connection sanity check
├── Dockerfile                      # (empty — not yet implemented)
├── requirements.txt
├── setup.py
└── .env                            # MONGO_DB_URL (not committed)
```

---


## Setup

```bash
# 1. Clone the repo
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>

# 2. Create a virtual environment
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Add your MongoDB connection string
echo "MONGO_DB_URL=<your-mongodb-connection-string>" > .env

# 5. Push the dataset to MongoDB
python push_data.py
```

---

## 🧰 Tech Stack
`Python` · `Pandas` / `NumPy` · `MongoDB` (via `pymongo`) · `python-dotenv` · `Docker` (planned)

---


**Your Name** — learning MLOps, one pipeline stage at a time. Feel free to connect on [LinkedIn](#) or check out more projects on [GitHub](#).
