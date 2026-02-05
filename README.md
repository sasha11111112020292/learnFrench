<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Le Jardin de Mots – Your French Garden</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Crimson+Pro:wght@300;400;600&family=Outfit:wght@300;400;500;600&family=Caveat:wght@400;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- Header -->
    <header class="header">
        <div class="header-content">
            <div class="logo">
                <span class="logo-icon">🌿</span>
                <h1 class="logo-text">Le Jardin de Mots</h1>
            </div>
            <div class="quick-links">
                <a href="https://www.collinsdictionary.com/dictionary/french-english" target="_blank" class="dict-link">Collins</a>
                <a href="https://context.reverso.net/translation/" target="_blank" class="dict-link">Reverso</a>
                <a href="https://www.wordreference.com/fr/" target="_blank" class="dict-link">WordReference</a>
                <a href="https://forvo.com/" target="_blank" class="dict-link">Forvo</a>
            </div>
        </div>
    </header>

    <!-- Navigation -->
    <nav class="nav">
        <button class="nav-btn active" data-view="garden">
            <span class="nav-icon">🌱</span>
            <span class="nav-label">Garden</span>
        </button>
        <button class="nav-btn" data-view="media">
            <span class="nav-icon">📚</span>
            <span class="nav-label">Media</span>
        </button>
        <button class="nav-btn" data-view="practice">
            <span class="nav-icon">📝</span>
            <span class="nav-label">Practice</span>
        </button>
        <button class="nav-btn" data-view="prompts">
            <span class="nav-icon">💬</span>
            <span class="nav-label">Prompts</span>
        </button>
        <button class="nav-btn" data-view="progress">
            <span class="nav-icon">📊</span>
            <span class="nav-label">Progress</span>
        </button>
    </nav>

    <!-- Main Content -->
    <main class="main-content">
        <!-- Garden View -->
        <section class="view active" id="garden-view">
            <div class="view-header">
                <h2 class="view-title">Your Vocabulary Garden</h2>
                <div class="view-actions">
                    <select id="theme-filter" class="theme-filter">
                        <option value="all">All Themes</option>
                    </select>
                    <select id="mastery-filter" class="mastery-filter">
                        <option value="all">All Stages</option>
                        <option value="seed">🌱 Seeds</option>
                        <option value="sprout">🌿 Sprouts</option>
                        <option value="flower">🌸 Flowers</option>
                    </select>
                    <button class="btn-primary" id="add-word-btn">+ Add Word</button>
                </div>
            </div>

            <div class="garden-grid" id="garden-grid">
                <div class="empty-state">
                    <span class="empty-icon">🌱</span>
                    <p class="empty-text">Your garden awaits its first seed...</p>
                    <button class="btn-secondary" onclick="document.getElementById('add-word-btn').click()">Plant Your First Word</button>
                </div>
            </div>
        </section>

        <!-- Media Library View -->
        <section class="view" id="media-view">
            <div class="view-header">
                <h2 class="view-title">Media Library</h2>
                <div class="view-actions">
                    <select id="media-type-filter" class="media-filter">
                        <option value="all">All Types</option>
                        <option value="song">🎵 Songs</option>
                        <option value="movie">🎬 Movies</option>
                        <option value="video">📹 Videos</option>
                        <option value="book">📖 Books</option>
                        <option value="podcast">🎙️ Podcasts</option>
                        <option value="article">📰 Articles</option>
                    </select>
                    <button class="btn-primary" id="add-media-btn">+ Add Media</button>
                </div>
            </div>

            <div class="media-grid" id="media-grid">
                <div class="empty-state">
                    <span class="empty-icon">📚</span>
                    <p class="empty-text">No media yet. Start logging what you watch, read, and listen to!</p>
                    <button class="btn-secondary" onclick="document.getElementById('add-media-btn').click()">Add Your First Media</button>
                </div>
            </div>
        </section>

        <!-- Practice Log View -->
        <section class="view" id="practice-view">
            <div class="view-header">
                <h2 class="view-title">Practice Log</h2>
                <div class="view-actions">
                    <button class="btn-primary" id="add-journal-btn">+ Journal Entry</button>
                    <button class="btn-primary" id="add-speaking-btn">+ Speaking Practice</button>
                </div>
            </div>

            <div class="practice-grid" id="practice-grid">
                <div class="empty-state">
                    <span class="empty-icon">📝</span>
                    <p class="empty-text">No practice logged yet. Start journaling or recording yourself!</p>
                </div>
            </div>
        </section>

        <!-- Speaking Prompts View -->
        <section class="view" id="prompts-view">
            <div class="view-header">
                <h2 class="view-title">Speaking Prompts</h2>
                <button class="btn-primary" id="generate-prompt-btn">✨ Generate Prompt</button>
            </div>

            <div class="prompt-container" id="prompt-container">
                <div class="empty-state">
                    <span class="empty-icon">💬</span>
                    <p class="empty-text">Click "Generate Prompt" to get a speaking challenge using your vocabulary!</p>
                </div>
            </div>

            <div class="sentence-builder" id="sentence-builder">
                <h3 class="section-title">Sentence Builder Challenge</h3>
                <button class="btn-secondary" id="random-words-btn">🎲 Get Random Words</button>
                <div class="random-words" id="random-words"></div>
                <textarea class="sentence-input" id="sentence-input" placeholder="Build a sentence using these words..."></textarea>
                <button class="btn-primary" id="save-sentence-btn" style="display: none;">Save Sentence</button>
            </div>
        </section>

        <!-- Progress View -->
        <section class="view" id="progress-view">
            <div class="view-header">
                <h2 class="view-title">Your Progress</h2>
            </div>

            <div class="stats-grid">
                <div class="stat-card">
                    <span class="stat-icon">🌱</span>
                    <div class="stat-content">
                        <p class="stat-value" id="total-words">0</p>
                        <p class="stat-label">Total Words</p>
                    </div>
                </div>
                <div class="stat-card">
                    <span class="stat-icon">🌸</span>
                    <div class="stat-content">
                        <p class="stat-value" id="mastered-words">0</p>
                        <p class="stat-label">Mastered</p>
                    </div>
                </div>
                <div class="stat-card">
                    <span class="stat-icon">📚</span>
                    <div class="stat-content">
                        <p class="stat-value" id="total-media">0</p>
                        <p class="stat-label">Media Logged</p>
                    </div>
                </div>
                <div class="stat-card">
                    <span class="stat-icon">📝</span>
                    <div class="stat-content">
                        <p class="stat-value" id="practice-count">0</p>
                        <p class="stat-label">Practice Sessions</p>
                    </div>
                </div>
            </div>

            <div class="motivation-box" id="motivation-box">
                <p class="motivation-text">Welcome to your garden! 🌱</p>
            </div>

            <div class="mistakes-section">
                <h3 class="section-title">Words to Review</h3>
                <div class="mistakes-grid" id="mistakes-grid">
                    <p class="empty-small">No words marked for review yet.</p>
                </div>
            </div>

            <div class="export-section">
                <h3 class="section-title">Backup & Sync</h3>
                <div class="export-buttons">
                    <button class="btn-secondary" id="export-btn">📥 Export Data</button>
                    <button class="btn-secondary" id="import-btn">📤 Import Data</button>
                    <input type="file" id="import-file" accept=".json" style="display: none;">
                </div>
            </div>
        </section>
    </main>

    <!-- Modals -->
    <!-- Add Word Modal -->
    <div class="modal" id="word-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">Add New Word</h3>
                <button class="modal-close" onclick="closeModal('word-modal')">&times;</button>
            </div>
            <form id="word-form" class="modal-form">
                <div class="form-group">
                    <label>Word *</label>
                    <input type="text" id="word-input" required placeholder="maison">
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>Gender</label>
                        <select id="gender-input">
                            <option value="">None</option>
                            <option value="m">♂ Masculine (le)</option>
                            <option value="f">♀ Feminine (la)</option>
                            <option value="p">Plural (les)</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Article</label>
                        <input type="text" id="article-input" placeholder="la">
                    </div>
                </div>
                <div class="form-group">
                    <label>IPA (Pronunciation)</label>
                    <input type="text" id="ipa-input" placeholder="mɛ.zɔ̃">
                </div>
                <div class="form-group">
                    <label>Meaning *</label>
                    <input type="text" id="meaning-input" required placeholder="house, home">
                </div>
                <div class="form-group">
                    <label>Example Sentences</label>
                    <textarea id="examples-input" rows="3" placeholder="La maison est grande.&#10;J'habite dans une belle maison."></textarea>
                </div>
                <div class="form-group">
                    <label>Theme/Topic</label>
                    <input type="text" id="theme-input" list="theme-list" placeholder="housing, daily-life">
                    <datalist id="theme-list"></datalist>
                </div>
                <div class="form-group">
                    <label>Image URL (optional)</label>
                    <input type="url" id="image-input" placeholder="https://...">
                </div>
                <div class="form-actions">
                    <button type="button" class="btn-secondary" onclick="closeModal('word-modal')">Cancel</button>
                    <button type="submit" class="btn-primary">Add Word</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Add Media Modal -->
    <div class="modal" id="media-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">Add Media</h3>
                <button class="modal-close" onclick="closeModal('media-modal')">&times;</button>
            </div>
            <form id="media-form" class="modal-form">
                <div class="form-group">
                    <label>Type *</label>
                    <select id="media-type-input" required>
                        <option value="song">🎵 Song</option>
                        <option value="movie">🎬 Movie</option>
                        <option value="video">📹 Video</option>
                        <option value="book">📖 Book</option>
                        <option value="podcast">🎙️ Podcast</option>
                        <option value="article">📰 Article</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Title *</label>
                    <input type="text" id="media-title-input" required placeholder="La Vie en Rose">
                </div>
                <div class="form-group" id="artist-group">
                    <label>Artist</label>
                    <input type="text" id="artist-input" placeholder="Édith Piaf">
                </div>
                <div class="form-group" id="author-group" style="display: none;">
                    <label>Author</label>
                    <input type="text" id="author-input" placeholder="Antoine de Saint-Exupéry">
                </div>
                <div class="form-group">
                    <label>URL</label>
                    <input type="url" id="media-url-input" placeholder="https://music.youtube.com/...">
                </div>
                <div class="form-group">
                    <label>Words from this media (comma-separated)</label>
                    <input type="text" id="media-words-input" placeholder="rose, amour, yeux">
                </div>
                <div class="form-group">
                    <label>Notes</label>
                    <textarea id="media-notes-input" rows="3" placeholder="Beautiful slow song, good for pronunciation..."></textarea>
                </div>
                <div class="form-actions">
                    <button type="button" class="btn-secondary" onclick="closeModal('media-modal')">Cancel</button>
                    <button type="submit" class="btn-primary">Add Media</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Add Journal Modal -->
    <div class="modal" id="journal-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">Journal Entry</h3>
                <button class="modal-close" onclick="closeModal('journal-modal')">&times;</button>
            </div>
            <form id="journal-form" class="modal-form">
                <div class="form-group">
                    <label>Write in French</label>
                    <textarea id="journal-entry-input" rows="8" required placeholder="Aujourd'hui, j'ai regardé..."></textarea>
                </div>
                <div class="form-group">
                    <label>Reflection / What you learned</label>
                    <textarea id="journal-reflection-input" rows="3" placeholder="Struggled with past tense conjugations..."></textarea>
                </div>
                <div class="form-actions">
                    <button type="button" class="btn-secondary" onclick="closeModal('journal-modal')">Cancel</button>
                    <button type="submit" class="btn-primary">Save Entry</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Add Speaking Modal -->
    <div class="modal" id="speaking-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">Speaking Practice</h3>
                <button class="modal-close" onclick="closeModal('speaking-modal')">&times;</button>
            </div>
            <form id="speaking-form" class="modal-form">
                <div class="form-group">
                    <label>Prompt / Question</label>
                    <input type="text" id="speaking-prompt-input" required placeholder="Décris ta journée">
                </div>
                <div class="form-group">
                    <label>Duration (minutes)</label>
                    <input type="number" id="speaking-duration-input" min="0.5" step="0.5" placeholder="2">
                </div>
                <div class="form-group">
                    <label>Notes / What you struggled with</label>
                    <textarea id="speaking-notes-input" rows="4" placeholder="Got stuck on 'I went'—need to review passé composé..."></textarea>
                </div>
                <div class="form-group">
                    <label>Words attempted (comma-separated)</label>
                    <input type="text" id="speaking-words-input" placeholder="aller, manger, dormir">
                </div>
                <div class="form-actions">
                    <button type="button" class="btn-secondary" onclick="closeModal('speaking-modal')">Cancel</button>
                    <button type="submit" class="btn-primary">Save Practice</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Word Detail Modal -->
    <div class="modal" id="word-detail-modal">
        <div class="modal-content word-detail-content">
            <div class="modal-header">
                <h3 class="modal-title" id="detail-word-title"></h3>
                <button class="modal-close" onclick="closeModal('word-detail-modal')">&times;</button>
            </div>
            <div class="word-detail-body" id="word-detail-body">
                <!-- Populated dynamically -->
            </div>
            <div class="word-detail-actions">
                <button class="btn-action" id="review-word-btn">✓ Reviewed</button>
                <button class="btn-action mistake-btn" id="mistake-word-btn">⚠ Need to Review</button>
                <button class="btn-action delete-btn" id="delete-word-btn">Delete</button>
            </div>
        </div>
    </div>

    <script src="app.js"></script>
</body>
</html>
