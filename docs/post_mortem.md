# GHSpark Post-Mortem ⚡️

**Date:** January 15, 2026
**Project:** GHSpark
**Duration:** 48 Hours

---

## 🚀 The Mission
The goal was to build a data-driven mini-tool for makers that solves a real problem: the noise and lag of GitHub's trending page. I wanted to create something that wasn't just useful, but also visually stunning and "shareable" to meet the TMAKER viral potential requirement.

## ✅ What Went Well

### 1. The "Spark Score" Algorithm
Developing the scoring logic was the most satisfying part. Balancing stars, forks, and repository age to find true *velocity* (not just popularity) worked better than expected.
`Score = (stars × 2 + forks) / days_live × activity_factor`

### 2. UI/UX Fidelity
Using **Framer Motion** combined with a glassmorphism aesthetic allowed me to create a "premium" feel that stands out from typical developer tools. The search interface feels snappy and alive.

### 3. Caching & Resilience
Implementing a 3-layer caching strategy (In-memory -> Supabase -> Stale-while-revalidate) means the app can handle a viral spike without hitting GitHub's API rate limits or crashing.

---

## 🚧 Challenges & Solutions

### Rate Limiting
**Challenge:** GitHub's public search API is strict.
**Solution:** I implemented aggressive caching on the server side and added a "Stale-while-revalidate" pattern. If the API fails, the user still sees the last known good data with a subtle warning if needed.

### Data Aggregation
**Challenge:** Calculating growth over time requires historical data that GitHub doesn't provide in a single query.
**Solution:** I used the repo's creation date and current stats to calculate an "average daily velocity" and then applied a weight to recent activity (forks/stars) to simulate a trend.

---

## 💡 Key Learnings
- **Speed is a feature:** Getting the first version of the landing page up in 4 hours allowed for 44 hours of polish and algorithm tuning.
- **Constraints breed creativity:** Limiting the search to repos < 6 months old forced the app to focus on "sparks" rather than established giants.
- **Sharing is secondary to utility:** I spent more time making sure the data was *accurate* than making the share buttons look good, because nobody shares a tool that doesn't work.

---

## 🔭 Future Roadmap
1. **User Accounts:** Allow makers to save searches and follow specific repositories.
2. **Email Alerts:** Weekly "Spark Report" for specific topics.
3. **Advanced Filtering:** Filter by license type, number of contributors, or commit frequency.
4. **Enhanced Virality:** Add a "Copy to Clipboard" button for repo summaries (Implemented in final polish).

---

Built with 💛 for the TMAKER Challenge.
