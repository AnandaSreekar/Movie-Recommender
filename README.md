# 🎬 Content-Based Movie Recommendation System

A simple yet effective movie recommendation engine that suggests similar movies based on genre, cast, and director using content-based filtering. This project lets users input a movie name and optionally apply filters like language and genre to receive personalized suggestions.

---

## 📂 Dataset

The dataset is a CSV file containing metadata about movies such as:
- `title`
- `genres`
- `director`
- `cast`
- `original_language`
- `vote_average`
- `overview`, `budget`, `runtime`, `release_date`, etc.

📝 **Note**: The dataset must be manually uploaded in the notebook environment (e.g., Colab) when prompted.

---

## 🧠 Concept Used

The project uses **Content-Based Filtering**, which recommends items (movies) similar to what the user likes, based on content features.

Key techniques:
- **TF-IDF (Term Frequency-Inverse Document Frequency)**: Converts text metadata into numerical feature vectors.
- **Cosine Similarity**: Measures similarity between movies based on those feature vectors.
- **Filtering**: Optional filtering by genre and language to personalize output.

---

## 🛠️ Tech Stack and Libraries

- **Python**
- **Pandas** – for data handling
- **Scikit-learn** – for TF-IDF and cosine similarity
- **difflib** – for fuzzy matching movie titles
- **Google Colab / Jupyter Notebook** – for interactive execution

---

## 🔁 Workflow

1. **Upload dataset** (`.csv` file)
2. **Preprocessing** – Handle missing data and combine features (`genre + cast + director`)
3. **Vectorization** – Apply TF-IDF to convert text into numbers
4. **Similarity Matrix** – Generate cosine similarity scores between movies
5. **User Input** – Accept movie title and optional filters (language & genre)
6. **Scoring** – Multiply similarity score by `vote_average` for quality weighting
7. **Ranking & Display** – Show top 30 most relevant recommendations

---

## 💻 Code Snippet

```python
vectorizer = TfidfVectorizer(stop_words='english')
feature_vectors = vectorizer.fit_transform(movies_data['combined'])

similarity = cosine_similarity(feature_vectors)

movie_index = movies_data[movies_data['title'] == close_match].index[0]
similarity_scores = list(enumerate(similarity[movie_index]))

scored_movies = [
    (i, score * float(movies_data.iloc[i]['vote_average']))
    for i, score in similarity_scores
]
sorted_movies = sorted(scored_movies, key=lambda x: x[1], reverse=True)


📤 Sample Output
yaml
Copy
Edit
🎬 Title: Inception
🎭 Cast: Leonardo DiCaprio, Joseph Gordon-Levitt...
🎬 Director: Christopher Nolan
⭐ Rating: 8.3 /10
🔥 Popularity: 150.43

🎯 TOP 30 SIMILAR MOVIES:
No.  Movie Title                 ⭐ Rating   🔥 Popularity
1    Interstellar                ⭐ 8.6      🔥 124.34
2    The Prestige                ⭐ 8.1      🔥 89.12
3    The Matrix                  ⭐ 8.7      🔥 112.56
...
✅ Done.



📝 Note
The system is fully interactive – users input a movie and optionally a preferred language/genre.

If no movies match the filters, the top 30 similar movies are shown instead.

Ideal for educational use to understand recommendation algorithms using content features.
