A rule-based movie recommendation system that scores items against user-stated genre interests using Jaccard similarity — no ML model or training data required.

Overview

This project builds a recommendation engine without any machine learning model or training data — instead it relies on Jaccard similarity, a simple set-overlap measure, to score how well each item's genre tags match a user's stated interests. The user types the genres they enjoy, the system compares that set against every item's genre tags in a small movie dataset (items.json), and returns the top matches ranked by similarity score.

How It Works

Jaccard similarity = (shared genres) / (total unique genres across both sets).

Example — user says scifi, comedy, and a movie is tagged scifi, comedy, romance:

Shared genres: {scifi, comedy} → 2
Union of genres: {scifi, comedy, romance} → 3
Score: 2 / 3 = 67% match

Every item in the dataset is scored this way, sorted highest-first, and the top N results are shown.

Setup
bash
pip install -r requirements.txt
cp .env.example .env   # adjust values if needed
python main.py

Then type genres separated by commas:

your interests: scifi, thriller

Type list to see all available genres, or quit to exit.

Configuration (.env)
Variable	Description	Default
TOP_N	How many recommendations to show	5
MIN_SCORE	Minimum similarity score required to appear in results (0.0 = show even weak matches)	0.0

.env is git-ignored — copy .env.example to .env locally and adjust as needed.

Project Structure
.
├── main.py             # Matching logic + interactive input loop
├── items.json           # Dataset: movie titles + genre tags
├── .env.example          # Template for local config
├── .env                   # Local config (git-ignored)
├── .gitignore
├── requirements.txt       # python-dotenv
└── README.md
Extending It

Add more items (or swap movies for books, songs, anything else) by editing items.json — each entry just needs a title and a list of genres. No code changes required.

Curriculum Context

Built as part of the DecodeLabs AI Engineering program — Project 4 shows that recommendation logic doesn't always require a trained model; well-designed similarity scoring on structured data can already produce useful, ranked suggestions.
