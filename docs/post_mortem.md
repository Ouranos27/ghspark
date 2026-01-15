# GHSpark Post-Mortem ⚡️

**Date:** January 15, 2026
**Project:** GHSpark
**Duration:** 48 Hours

---

## 🚀 The Mission
The goal was to build a data-driven mini-tool for makers that solves a real problem: the noise and lag of GitHub's trending page. I wanted to create something that wasn't just useful, but also visually stunning and "shareable" to meet the TMAKER viral potential requirement.

## ✅ What Went Well

### 1. The "Spark Score" Algorithm
Developing the scoring logic was the most satisfying part. The goal was to identify repositories with high **velocity** — meaning rapid growth rate — rather than just absolute popularity.

**What is a "Spark"?**  
A spark is a repository that's quickly gaining momentum. Think of it as catching fire before it becomes a wildfire. These are newer projects (typically < 6 months old) experiencing explosive growth.

**What is "Velocity"?**  
Velocity measures the *rate* of growth over time. A repo gaining 100 stars per day has higher velocity than one that gained 10,000 stars over 5 years. By focusing on velocity, we surface emerging trends rather than established projects.

**The Formula:**  
`Score = (stars × 2 + forks) / days_live × activity_factor`

- **Stars × 2**: Community interest is weighted heavily (stars indicate endorsement)
- **Forks**: Developer engagement (people actively experimenting with the code)
- **days_live**: Normalizes for repository age — prevents old repos from dominating
- **activity_factor**: Boosts recent activity to prioritize currently trending projects

This balancing act worked better than expected, consistently surfacing genuine "sparks" rather than stale popular repos.

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
