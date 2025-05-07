# 🎶 Smart Music Recommendation System for Emerging Artists

**Listen Differently: How we used Neo4j, MongoDB, and Redis to connect listeners to emerging artists**  
*By Mayadah Alhashem, Jinney Hong, Rachel Kalafos, and Clara Rhoades*  
*UC Berkeley — Master of Information and Data Science*  
*Course: DATASCI 205 - Fundamentals of Data Engineering*

---

## 📌 Overview

Mainstream music platforms reward popularity, making it difficult for new artists to get discovered. Our team tackled this imbalance by building a fair recommendation system that connects listeners to emerging artists—without compromising user experience. We leveraged a trio of NoSQL databases (Neo4j, MongoDB, and Redis) to analyze user behavior and musical similarity.

Read more about our project [on Medium.](https://medium.com/@clara.rhoades/a-smart-music-recommendation-system-for-emerging-artists-afe11b9ebdeb)

---

## 🎧 Dataset

We used a publicly available [Spotify Playlist dataset from Kaggle](https://www.kaggle.com/datasets/andrewmvd/spotify-playlist-dataset), featuring:

- **15,918** unique users
- **157,500** unique playlists
- **2M+** tracks
- **289,819** artists

The dataset contains four primary features:
- `User ID` (hashed)
- `Artist name`
- `Track title`
- `Playlist name`

### Repository Files:
| File | Description |
|------|-------------|
| `artists.csv` | List of artist nodes with labels |
| `tracks.csv` | List of track nodes with labels |
| `edges.csv` | Relationships between artists and tracks (e.g., `PERFORMED`) with weights |
| `neo4j_graph.ipynb` | Jupyter notebook used to preprocess data and load the graph into Neo4j |
| `final_slides` | PDF of our presentation slide deck |

---

## 🧠 Architecture Overview

### 1. **Neo4j**: Relationship Modeling and Graph Analytics

We modeled the music ecosystem with:
- `PERFORMED (Artist → Track)`
- `SIMILAR_TO (Artist ↔ Artist)`
- `APPEARS_IN (Track → Playlist)`

#### Algorithms:
- **PageRank** to identify influential artists
- **Louvain** for community detection
- **Cosine & Jaccard Similarity** to connect emerging and established artists

### 2. **MongoDB**: Rich Artist Metadata

Stored flexible artist data including:
- Collaboration history
- Genre tags
- Track-level features

MongoDB’s document model allows schema-less evolution and fast querying without complex joins.

(Theoretical usecase; not implemented in code)

### 3. **Redis**: Real-Time Recommendation Layer

Used Redis for:
- Storing recent user activity
- Tracking trending artists
- Returning instant recommendations

Its in-memory architecture ensures fast updates and sub-millisecond query times.

(Theoretical usecase; not implemented in code)

---

## 🔧 System Pipeline

1. **Data Preprocessing** in PostgreSQL for normalization and cleaning.
2. **Graph Construction** in Neo4j with `artists.csv`, `tracks.csv`, and `edges.csv`.
3. **Graph Analysis** using the Neo4j Python driver (see `neo4j_graph.ipynb`).
4. **Metadata Storage** using MongoDB for artist profiles and track features. (theoretical)
5. **Session Tracking** using Redis to serve real-time recommendations. (theoretical)

---

## 🔍 Visualizing the Graph

Our Neo4j visualization surfaced genre-like communities and surprising cross-genre links. For example:
- *Daft Punk* had strong cross-cluster influence.
- *"Intro"* by M83 appeared in over 6,600 playlists, highlighting its centrality.

---

## 🌎 Social Impact

This project goes beyond engineering: it demonstrates how thoughtful system design can rebalance cultural power. By prioritizing emerging artists using real listening patterns—not marketing budgets—we created a fairer discovery experience.

---

## 📂 Project Structure

```bash
├── artists.csv           # Artist node list for Neo4j
├── tracks.csv            # Track node list for Neo4j
├── edges.csv             # Graph edges (relationships)
├── neo4j_graph.ipynb     # Full pipeline from raw data to Neo4j graph
└── README.md             # You are here :)

