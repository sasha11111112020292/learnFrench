<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ma Maison · French Sanctuary</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300;400;500;600&family=Work+Sans:wght@300;400;500&family=Allura&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <style>
        :root {
            --cream: #FBF9F4;
            --cream-dark: #F5F1E8;
            --crimson: #8B2635;
            --crimson-soft: #A64253;
            --navy: #1B2B3A;
            --navy-soft: #2C3E50;
            --gold: #C9A861;
            --gold-pale: #E5D4A6;
            --text: #2A2520;
            --text-soft: #6B615C;
            --whisper: rgba(42, 37, 32, 0.04);
            --shadow: rgba(27, 43, 58, 0.08);
            --shadow-strong: rgba(27, 43, 58, 0.15);
            --rosy: #D4A5A5;
            --sage: #A8B8A8;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: 'Work Sans', sans-serif;
            background: var(--cream);
            color: var(--text);
            line-height: 1.7;
            font-weight: 300;
            overflow-x: hidden;
        }

        /* Affirmation */
        .affirmation {
            position: fixed;
            top: 20%;
            right: 3rem;
            max-width: 280px;
            padding: 1.5rem;
            background: white;
            border-left: 2px solid var(--gold);
            box-shadow: 0 4px 20px var(--shadow);
            opacity: 0;
            transform: translateX(20px);
            pointer-events: none;
            z-index: 1000;
            transition: all 1s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .affirmation.visible {
            opacity: 1;
            transform: translateX(0);
        }

        .affirmation-text {
            font-family: 'Cormorant Garamond', serif;
            font-size: 1.1rem;
            font-weight: 400;
            color: var(--navy);
            margin-bottom: 0.5rem;
            font-style: italic;
        }

        .affirmation-translation {
            font-size: 0.85rem;
            color: var(--text-soft);
        }

        /* Floating Heart */
        .floating-heart {
            position: fixed;
            bottom: 2rem;
            right: 2rem;
            opacity: 0.2;
            z-index: 1;
            animation: heartPulse 4s ease-in-out infinite;
            pointer-events: none;
        }

        @keyframes heartPulse {
            0%, 100% { transform: scale(1); opacity: 0.2; }
            50% { transform: scale(1.08); opacity: 0.3; }
        }

        /* Header */
        .header {
            padding: 2rem 2rem 1rem;
            border-bottom: 1px solid var(--whisper);
            background: rgba(251, 249, 244, 0.95);
            backdrop-filter: blur(10px);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .header-inner {
            max-width: 1100px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            flex-direction: column;
        }

        .logo-main {
            font-family: 'Cormorant Garamond', serif;
            font-size: 1.75rem;
            font-weight: 400;
            color: var(--crimson);
            letter-spacing: 0.02em;
        }

        .logo-sub {
            font-size: 0.7rem;
            color: var(--text-soft);
            letter-spacing: 0.2em;
            text-transform: uppercase;
            margin-top: 0.25rem;
        }

        .signature {
            font-family: 'Allura', cursive;
            font-size: 2rem;
            color: var(--gold);
            opacity: 0.7;
            cursor: pointer;
            transition: all 0.5s ease;
        }

        .signature:hover {
            opacity: 0.9;
        }

        /* Navigation */
        .nav {
            max-width: 1100px;
            margin: 0 auto;
            padding: 2rem 2rem 1rem;
            display: flex;
            gap: 0.5rem;
            border-bottom: 1px solid var(--whisper);
            overflow-x: auto;
        }

        .nav-link {
            padding: 0.75rem 1.5rem;
            border: none;
            background: transparent;
            font-family: 'Work Sans', sans-serif;
            font-size: 0.9rem;
            font-weight: 400;
            color: var(--text-soft);
            cursor: pointer;
            border-bottom: 2px solid transparent;
            transition: all 0.3s;
            white-space: nowrap;
        }

        .nav-link:hover {
            color: var(--crimson);
        }

        .nav-link.active {
            color: var(--navy);
            border-bottom-color: var(--crimson);
        }

        /* Main */
        .main {
            max-width: 1100px;
            margin: 0 auto;
            padding: 3rem 2rem 5rem;
        }

        .room {
            display: none;
            animation: fadeIn 0.6s ease-out;
        }

        .room.active {
            display: block;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .room-intro {
            text-align: center;
            max-width: 650px;
            margin: 0 auto 3rem;
        }

        .room-title {
            font-family: 'Cormorant Garamond', serif;
            font-size: 2.5rem;
            font-weight: 400;
            color: var(--navy);
            margin-bottom: 1rem;
        }

        .room-description {
            font-size: 1rem;
            color: var(--text-soft);
            line-height: 1.8;
        }

        /* Cards */
        .entrance-card {
            background: white;
            padding: 3rem;
            border-radius: 2px;
            box-shadow: 0 4px 24px var(--shadow);
            margin-bottom: 2rem;
            border-top: 3px solid var(--gold);
        }

        .entrance-sentence {
            font-family: 'Cormorant Garamond', serif;
            font-size: 2.25rem;
            font-weight: 400;
            color: var(--navy);
            margin-bottom: 1rem;
            text-align: center;
        }

        .entrance-translation {
            font-size: 1.1rem;
            color: var(--text-soft);
            text-align: center;
            margin-bottom: 2rem;
        }

        .entrance-note {
            font-size: 0.95rem;
            line-height: 1.8;
            color: var(--text);
            padding: 1.5rem;
            background: var(--whisper);
            border-left: 2px solid var(--gold-pale);
        }

        /* Buttons */
        .data-actions {
            display: flex;
            gap: 1rem;
            justify-content: center;
            margin-top: 2rem;
        }

        .btn {
            padding: 0.875rem 2rem;
            border: none;
            border-radius: 2px;
            font-family: 'Work Sans', sans-serif;
            font-size: 0.9rem;
            font-weight: 400;
            cursor: pointer;
            transition: all 0.3s;
        }

        .btn-primary {
            background: var(--navy);
            color: white;
        }

        .btn-primary:hover {
            background: var(--navy-soft);
            transform: translateY(-1px);
            box-shadow: 0 4px 12px var(--shadow);
        }

        .btn-secondary {
            background: white;
            color: var(--navy);
            border: 1px solid var(--navy);
        }

        .btn-secondary:hover {
            background: var(--cream-dark);
        }

        .btn-danger {
            background: transparent;
            color: var(--crimson);
            border: 1px solid var(--crimson);
            font-size: 0.8rem;
        }

        .btn-danger:hover {
            background: var(--crimson);
            color: white;
        }

        .btn-drive {
            padding: 0.875rem;
            width: 48px;
            height: 48px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            background: white;
            color: var(--navy);
            border: 1px solid var(--navy);
            cursor: pointer;
            transition: all 0.3s;
        }

        .btn-drive:hover {
            background: var(--cream-dark);
            transform: translateY(-1px);
            box-shadow: 0 4px 12px var(--shadow);
        }

        /* Word Grid */
        .word-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 1.5rem;
        }

        .word-card {
            background: white;
            padding: 2rem;
            border-radius: 2px;
            box-shadow: 0 2px 12px var(--shadow);
            border-left: 3px solid var(--gold);
            position: relative;
        }

        .word-actions {
            position: absolute;
            top: 1rem;
            right: 1rem;
            display: flex;
            gap: 0.5rem;
            z-index: 10;
        }

        .icon-btn {
            background: white;
            border: none;
            cursor: pointer;
            font-size: 1.1rem;
            opacity: 0.6;
            transition: opacity 0.2s;
            padding: 0.25rem;
            border-radius: 2px;
        }

        .icon-btn:hover {
            opacity: 1;
        }

        .word-image {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-radius: 2px;
            margin-bottom: 1rem;
        }

        .word-french {
            font-family: 'Cormorant Garamond', serif;
            font-size: 1.75rem;
            color: var(--navy);
            margin-bottom: 0.5rem;
        }

        .word-meaning {
            font-size: 1rem;
            color: var(--navy-soft);
            margin-bottom: 1rem;
            font-weight: 400;
            font-style: italic;
        }

        .word-article {
            font-size: 0.85rem;
            color: var(--text-soft);
            margin-bottom: 1rem;
        }

        .word-contexts {
            margin: 1rem 0;
        }

        .context {
            margin-bottom: 1rem;
        }

        .context-label {
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            color: var(--gold);
            margin-bottom: 0.25rem;
        }

        .context-sentence {
            font-size: 0.95rem;
            color: var(--text);
            font-style: italic;
        }

        .word-note {
            margin-top: 1rem;
            padding-top: 1rem;
            border-top: 1px solid var(--whisper);
            font-size: 0.9rem;
            color: var(--text-soft);
        }

        /* Categories Grid */
        .category-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .category-tag {
            display: inline-block;
            background: var(--whisper);
            color: var(--text-soft);
            padding: 0.25rem 0.75rem;
            border-radius: 12px;
            font-size: 0.75rem;
            letter-spacing: 0.03em;
        }

        .category-tag.topic {
            background: var(--gold-pale);
            color: var(--navy);
        }

        .category-tag.time {
            background: var(--sage);
            color: white;
            font-size: 0.7rem;
        }

        .empty {
            grid-column: 1 / -1;
            text-align: center;
            padding: 4rem 2rem;
        }

        .empty-icon {
            font-size: 3rem;
            margin-bottom: 1rem;
        }

        .empty-text {
            font-size: 1rem;
            color: var(--text-soft);
            line-height: 1.8;
        }

        /* Game section */
        .game-section {
            background: white;
            padding: 2rem;
            border-radius: 2px;
            box-shadow: 0 2px 12px var(--shadow);
            margin-bottom: 2rem;
            text-align: center;
            border-top: 3px solid var(--crimson);
        }

        .game-result {
            margin-top: 1.5rem;
            min-height: 100px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .game-word {
            font-family: 'Cormorant Garamond', serif;
            font-size: 2rem;
            color: var(--navy);
            margin-bottom: 0.5rem;
        }

        .game-prompt {
            font-size: 0.95rem;
            color: var(--text-soft);
            font-style: italic;
        }

        /* Resource cards */
        .resource-grid {
            display: grid;
            gap: 1rem;
        }

        .resource-card {
            background: white;
            padding: 1.5rem;
            border-radius: 2px;
            box-shadow: 0 2px 8px var(--shadow);
            border-left: 3px solid var(--crimson);
            display: flex;
            justify-content: space-between;
            align-items: start;
            gap: 1rem;
        }

        .resource-info {
            flex: 1;
        }

        .resource-type {
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            color: var(--gold);
            margin-bottom: 0.5rem;
        }

        .resource-title {
            font-family: 'Cormorant Garamond', serif;
            font-size: 1.25rem;
            color: var(--navy);
            margin-bottom: 0.25rem;
        }

        .resource-link {
            font-size: 0.85rem;
            color: var(--text-soft);
            word-break: break-all;
            text-decoration: none;
            display: block;
            margin-bottom: 0.5rem;
        }

        .resource-link:hover {
            color: var(--crimson);
            text-decoration: underline;
        }

        .resource-note {
            margin-top: 0.5rem;
            font-size: 0.9rem;
            color: var(--text);
            font-style: italic;
        }

        .resource-status {
            font-size: 0.8rem;
            color: var(--text-soft);
            margin-top: 0.5rem;
        }

        /* PDF Save Button */
        .pdf-save-btn {
            position: fixed;
            bottom: 2rem;
            left: 2rem;
            width: 56px;
            height: 56px;
            border-radius: 50%;
            background: var(--crimson);
            color: white;
            border: none;
            box-shadow: 0 4px 12px var(--shadow-strong);
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 100;
        }

        .pdf-save-btn:hover {
            background: var(--crimson-soft);
            transform: translateY(-2px);
            box-shadow: 0 6px 16px var(--shadow-strong);
        }

        .pdf-save-btn svg {
            width: 24px;
            height: 24px;
        }

        /* Transcript/Lyrics Button */
        .transcript-btn {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--gold-pale);
            color: var(--navy);
            border: none;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
        }

        .transcript-btn:hover {
            background: var(--gold);
            transform: scale(1.05);
        }

        .transcript-btn svg {
            width: 20px;
            height: 20px;
        }

        .resource-actions {
            display: flex;
            gap: 0.5rem;
            align-items: center;
        }

        /* Speaking recordings */
        .recording-card {
            background: white;
            padding: 1.5rem;
            border-radius: 2px;
            box-shadow: 0 2px 8px var(--shadow);
            border-left: 3px solid var(--gold);
            margin-bottom: 1rem;
        }

        .recording-header {
            display: flex;
            justify-content: space-between;
            align-items: start;
            margin-bottom: 1rem;
        }

        .recording-date {
            font-size: 0.8rem;
            color: var(--text-soft);
        }

        .recording-transcript {
            font-family: 'Cormorant Garamond', serif;
            font-size: 1.25rem;
            color: var(--navy);
            margin-bottom: 0.75rem;
            font-style: italic;
        }

        .recording-note {
            font-size: 0.9rem;
            color: var(--text);
            padding: 1rem;
            background: var(--whisper);
            border-left: 2px solid var(--gold-pale);
        }

        /* Notes section */
        #notes-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 1.5rem;
        }

        .note-card {
            background: white;
            padding: 1.5rem;
            border-radius: 2px;
            box-shadow: 0 2px 8px var(--shadow);
            display: flex;
            flex-direction: column;
            gap: 1rem;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .note-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px var(--shadow-strong);
        }

        .note-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .note-category {
            padding: 0.35rem 0.75rem;
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            font-weight: 500;
            border-radius: 2px;
        }

        .note-title {
            font-family: 'Cormorant Garamond', serif;
            font-size: 1.4rem;
            font-weight: 500;
            color: var(--navy);
            line-height: 1.3;
        }

        .note-content {
            font-size: 0.95rem;
            color: var(--text);
            line-height: 1.6;
        }

        .note-link {
            display: inline-flex;
            align-items: center;
            gap: 0.35rem;
            font-size: 0.85rem;
            color: var(--gold);
            text-decoration: none;
            transition: color 0.2s;
        }

        .note-link:hover {
            color: var(--crimson);
        }

        .note-date {
            font-size: 0.75rem;
            color: var(--text-soft);
            margin-top: auto;
            padding-top: 1rem;
            border-top: 1px solid var(--whisper);
        }

        /* Writings archive */
        .writing-card {
            background: white;
            padding: 2rem;
            border-radius: 2px;
            box-shadow: 0 2px 8px var(--shadow);
            border-left: 3px solid var(--navy);
            margin-bottom: 1rem;
        }

        .writing-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
            padding-bottom: 1rem;
            border-bottom: 1px solid var(--whisper);
        }

        .writing-date {
            font-size: 0.8rem;
            color: var(--text-soft);
        }

        .writing-text {
            font-family: 'Cormorant Garamond', serif;
            font-size: 1.15rem;
            line-height: 1.9;
            color: var(--text);
            white-space: pre-wrap;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(27, 43, 58, 0.5);
            z-index: 200;
            backdrop-filter: blur(4px);
        }

        .modal.active {
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .modal-content {
            background: white;
            padding: 3rem;
            border-radius: 2px;
            max-width: 600px;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: 0 8px 32px var(--shadow-strong);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
            border-bottom: 1px solid var(--whisper);
            padding-bottom: 1rem;
        }

        .modal-title {
            font-family: 'Cormorant Garamond', serif;
            font-size: 1.75rem;
            color: var(--navy);
        }

        .close-btn {
            background: transparent;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--text-soft);
            transition: color 0.2s;
        }

        .close-btn:hover {
            color: var(--crimson);
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-label {
            display: block;
            font-size: 0.9rem;
            color: var(--text);
            margin-bottom: 0.5rem;
        }

        .form-input,
        .form-textarea,
        .form-select {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #DDD;
            border-radius: 2px;
            font-family: 'Work Sans', sans-serif;
            font-size: 0.95rem;
            transition: border-color 0.2s;
        }

        .form-input:focus,
        .form-textarea:focus,
        .form-select:focus {
            outline: none;
            border-color: var(--gold);
        }

        .form-textarea {
            min-height: 100px;
            resize: vertical;
        }

        .form-actions {
            display: flex;
            gap: 1rem;
            justify-content: flex-end;
            margin-top: 2rem;
        }

        .image-upload-area {
            border: 2px dashed #DDD;
            border-radius: 2px;
            padding: 2rem;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
        }

        .image-upload-area:hover {
            border-color: var(--gold);
            background: var(--whisper);
        }

        .image-preview {
            max-width: 100%;
            max-height: 300px;
            margin-top: 1rem;
            border-radius: 2px;
        }

        /* Category Grid */
        .category-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

        /* Writing area */
        .writing-container {
            background: white;
            padding: 3rem;
            border-radius: 2px;
            box-shadow: 0 4px 24px var(--shadow);
            margin-bottom: 2rem;
        }

        .writing-area {
            width: 100%;
            min-height: 400px;
            padding: 2rem;
            border: 1px solid #EEE;
            border-radius: 2px;
            font-family: 'Cormorant Garamond', serif;
            font-size: 1.25rem;
            line-height: 2;
            color: var(--text);
            resize: vertical;
        }

        .writing-area:focus {
            outline: none;
            border-color: var(--gold);
        }

        .writing-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 1.5rem;
        }

        .word-count {
            font-size: 0.9rem;
            color: var(--text-soft);
        }

        /* Speaking section */
        #spoken-text {
            margin-top: 1.5rem;
            min-height: 60px;
            padding: 1rem;
            background: var(--whisper);
            border-left: 2px solid var(--gold);
            font-family: 'Cormorant Garamond', serif;
            font-size: 1.25rem;
        }

        .speaking-controls {
            display: flex;
            gap: 1rem;
            margin-top: 1rem;
        }

        /* Practice Stats */
        .practice-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 1rem;
            margin-bottom: 2rem;
        }

        .stat-card {
            background: white;
            padding: 1.5rem;
            border-radius: 2px;
            border-left: 3px solid var(--gold);
            text-align: center;
        }

        .stat-number {
            font-family: 'Cormorant Garamond', serif;
            font-size: 2.5rem;
            font-weight: 500;
            color: var(--crimson);
            margin-bottom: 0.25rem;
        }

        .stat-label {
            font-size: 0.8rem;
            color: var(--text-soft);
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        .speaking-controls {
            display: flex;
            gap: 1rem;
            margin-top: 1rem;
        }

        /* Tabs */
        .tabs {
            display: flex;
            gap: 0.5rem;
            margin-bottom: 2rem;
            border-bottom: 1px solid var(--whisper);
        }

        .tab {
            padding: 0.75rem 1.5rem;
            border: none;
            background: transparent;
            font-family: 'Work Sans', sans-serif;
            font-size: 0.9rem;
            cursor: pointer;
            color: var(--text-soft);
            border-bottom: 2px solid transparent;
            transition: all 0.2s;
        }

        .tab:hover {
            color: var(--navy);
        }

        .tab.active {
            color: var(--navy);
            border-bottom-color: var(--crimson);
        }

        .tab-content {
            display: none;
        }

        /* Filter Bar */
        .filter-bar {
            display: flex;
            flex-wrap: wrap;
            gap: 0.75rem;
            padding: 1.75rem;
            background: white;
            border-radius: 16px;
            margin-bottom: 2rem;
            box-shadow: 0 2px 12px var(--shadow);
            border: 1px solid rgba(201, 168, 97, 0.2);
        }

        .filter-tag {
            padding: 0.65rem 1.5rem;
            border: 2px solid var(--whisper);
            background: var(--cream);
            font-family: 'Work Sans', sans-serif;
            font-size: 0.9rem;
            font-weight: 500;
            color: var(--text);
            cursor: pointer;
            border-radius: 24px;
            transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
        }

        .filter-tag:hover {
            transform: translateY(-2px);
            border-color: var(--gold);
            background: var(--gold-pale);
            box-shadow: 0 4px 12px rgba(201, 168, 97, 0.2);
        }

        .filter-tag.active {
            background: var(--crimson);
            color: white;
            border-color: var(--crimson);
            box-shadow: 0 4px 16px rgba(139, 38, 53, 0.3);
            transform: translateY(-1px);
        }

        .filter-tag.active::after {
            content: '✓';
            margin-left: 0.5rem;
            font-weight: 700;
        }

        /* Question Section (Parler) */
        .question-section {
            background: white;
            padding: 2rem;
            border-radius: 16px;
            box-shadow: 0 2px 12px var(--shadow);
            margin-bottom: 2rem;
            border: 1px solid rgba(201, 168, 97, 0.2);
        }

        .question-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 1rem;
            margin-bottom: 1.25rem;
            padding-bottom: 0.75rem;
            border-bottom: 1px solid var(--whisper);
        }

        .question-title {
            font-family: 'Work Sans', sans-serif;
            font-size: 0.75rem;
            font-weight: 600;
            color: var(--gold);
            margin: 0;
            letter-spacing: 0.15em;
            text-transform: uppercase;
        }

        .doc-link {
            display: inline-flex;
            align-items: center;
            gap: 0.4rem;
            padding: 0.5rem 1rem;
            background: var(--whisper);
            color: var(--navy);
            text-decoration: none;
            border-radius: 8px;
            font-family: 'Work Sans', sans-serif;
            font-size: 0.8rem;
            font-weight: 500;
            transition: all 0.2s ease;
            border: 1px solid transparent;
        }

        .doc-link:hover {
            background: var(--gold-pale);
            border-color: var(--gold);
            color: var(--crimson);
        }

        .doc-link svg {
            width: 14px;
            height: 14px;
            opacity: 0.7;
        }

        .question-input {
            font-size: 1.15rem !important;
            font-family: 'Cormorant Garamond', serif !important;
            font-weight: 400;
            color: var(--navy) !important;
            padding: 1rem 1.25rem !important;
            border-radius: 12px !important;
            border: 2px solid var(--whisper) !important;
            background: var(--cream) !important;
            transition: all 0.3s ease !important;
        }

        .question-input:focus {
            border-color: var(--gold) !important;
            background: white !important;
            box-shadow: 0 0 0 4px rgba(201, 168, 97, 0.1) !important;
            outline: none !important;
        }

        .question-input::placeholder {
            font-family: 'Work Sans', sans-serif;
            font-size: 0.95rem;
            font-style: italic;
            color: var(--text-soft);
            opacity: 0.6;
        }

        /* Beautiful Speak Button */
        .btn-speak {
            display: inline-flex;
            align-items: center;
            gap: 0.75rem;
            padding: 1rem 2rem;
            background: linear-gradient(135deg, var(--crimson) 0%, #A64253 100%);
            color: white;
            border: none;
            border-radius: 12px;
            font-family: 'Work Sans', sans-serif;
            font-size: 1.1rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 4px 16px rgba(139, 38, 53, 0.25);
            margin-bottom: 1.5rem;
            position: relative;
            overflow: hidden;
        }

        .mic-icon {
            width: 22px;
            height: 22px;
            flex-shrink: 0;
        }

        .btn-speak::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.5s;
        }

        .btn-speak:hover::before {
            left: 100%;
        }

        .btn-speak:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 24px rgba(139, 38, 53, 0.35);
        }

        .btn-speak:active {
            transform: translateY(0);
        }

        .btn-speak.btn-danger {
            background: linear-gradient(135deg, #c0392b 0%, #e74c3c 100%);
        }

        .tab-content.active {
            display: block;
        }

        /* SVG Icons */
        .svg-icon {
            width: 20px;
            height: 20px;
            fill: currentColor;
            display: inline-block;
            vertical-align: middle;
        }

        .svg-icon-lg {
            width: 48px;
            height: 48px;
            fill: currentColor;
        }

        /* Heart Note */
        .heart-note {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.9);
            background: white;
            padding: 2.5rem;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(139, 38, 53, 0.2);
            z-index: 10000;
            max-width: 320px;
            text-align: center;
            border-top: 4px solid var(--rosy);
            animation: heartNoteIn 0.6s cubic-bezier(0.4, 0, 0.2, 1) forwards;
            display: none;
        }

        @keyframes heartNoteIn {
            from { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
            to { opacity: 1; transform: translate(-50%, -50%) scale(1); }
        }

        /* Responsive */
        @media (max-width: 768px) {
            .affirmation {
                right: 1rem;
                max-width: 240px;
            }

            .header {
                padding: 1.5rem 1rem 0.5rem;
            }

            .main {
                padding: 2rem 1rem 3rem;
            }

            .nav {
                padding: 1rem;
            }

            .entrance-card {
                padding: 2rem 1.5rem;
            }

            .entrance-sentence {
                font-size: 1.75rem;
            }

            .word-grid {
                grid-template-columns: 1fr;
            }

            .data-actions {
                flex-direction: column;
                align-items: center;
            }

            .modal-content {
                padding: 2rem 1.5rem;
            }

            .tabs {
                overflow-x: auto;
            }

            .speaking-controls {
                flex-direction: column;
            }

            .category-grid {
                grid-template-columns: 1fr;
            }

            .pdf-save-btn {
                bottom: 1rem;
                left: 1rem;
                width: 48px;
                height: 48px;
            }

            .pdf-save-btn svg {
                width: 20px;
                height: 20px;
            }

            .transcript-btn {
                width: 36px;
                height: 36px;
            }

            .transcript-btn svg {
                width: 18px;
                height: 18px;
            }
        }
    </style>
</head>
<body>
    <!-- Affirmation -->
    <div class="affirmation" id="affirmation">
        <div class="affirmation-text"></div>
        <div class="affirmation-translation"></div>
    </div>

    <!-- Heart Note -->
    <div class="heart-note" id="heart-note">
        <div id="heart-reason"></div>
        <div style="margin-top: 1.5rem; font-size: 0.9rem; color: var(--text-soft);">
            C'est ton voyage.
        </div>
    </div>

    <!-- Header -->
    <header class="header">
        <div class="header-inner">
            <div class="logo">
                <div class="logo-main">Ma Maison</div>
                <div class="logo-sub">French Sanctuary</div>
            </div>
            <div class="signature">apprendre</div>
        </div>
    </header>

    <!-- Navigation -->
    <nav class="nav">
        <button class="nav-link active" data-room="entree">L'Entrée</button>
        <button class="nav-link" data-room="jardin">Le Jardin</button>
        <button class="nav-link" data-room="lire">Lire</button>
        <button class="nav-link" data-room="ecouter">Écouter</button>
        <button class="nav-link" data-room="parler">Parler</button>
        <button class="nav-link" data-room="ecrire">Écrire</button>
        <button class="nav-link" data-room="notes">Notes</button>
        <button class="nav-link" data-room="ressources">Ressources</button>
    </nav>

    <!-- Main -->
    <main class="main">
        <!-- L'Entrée -->
        <section class="room active" id="entree">
            <div class="room-intro">
                <h1 class="room-title">L'Entrée</h1>
                <p class="room-description">
                    Entre doucement. Prends ton temps. C'est ton espace, ton rythme.
                </p>
            </div>

            <div id="entrance-content"></div>

            <!-- Data management -->
            <div class="entrance-card">
                <div class="entrance-sentence">Tes données</div>
                <div class="entrance-translation">
                    Tout reste sur ton appareil. Tu peux sauvegarder ou recommencer.
                </div>
                <div class="data-actions">
                    <button class="btn btn-secondary" id="export-data">
                        ⬇ Exporter tout
                    </button>
                    <button class="btn btn-secondary" id="import-data">
                        ⬆ Importer tout
                    </button>
                    <button class="btn-drive" id="drive-link" title="Sauvegarde Google Drive">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                            <path d="M18 10h-1.26A8 8 0 1 0 9 20h9a5 5 0 0 0 0-10z"></path>
                        </svg>
                    </button>
                    <button class="btn btn-danger" id="reset-data">
                        Recommencer à zéro
                    </button>
                </div>
            </div>
        </section>

        <!-- Le Jardin -->
        <section class="room" id="jardin">
            <div class="room-intro">
                <h1 class="room-title">Le Jardin</h1>
                <p class="room-description">
                    Plante des mots. Laisse-les grandir dans leur propre temps.
                </p>
            </div>

            <!-- Jardin Filters - NEW -->
            <div class="entrance-card" id="jardin-filters">
                <div class="entrance-sentence" style="font-size:1.5rem;">Explorer le jardin</div>

                <div class="category-grid">
                    <div>
                        <label class="form-label">Année</label>
                        <select class="form-select" id="filter-year">
                            <option value="">Toutes</option>
                        </select>
                    </div>

                    <div>
                        <label class="form-label">Trimestre</label>
                        <select class="form-select" id="filter-quarter">
                            <option value="">Tous</option>
                            <option value="Q1">Q1</option>
                            <option value="Q2">Q2</option>
                            <option value="Q3">Q3</option>
                            <option value="Q4">Q4</option>
                        </select>
                    </div>

                    <div>
                        <label class="form-label">Semaine</label>
                        <select class="form-select" id="filter-week">
                            <option value="">Toutes</option>
                        </select>
                    </div>

                    <div>
                        <label class="form-label">Thème</label>
                        <select class="form-select" id="filter-theme">
                            <option value="">Tous les thèmes</option>
                        </select>
                    </div>
                </div>

                <div style="text-align:right;">
                    <button class="btn btn-secondary" id="reset-filters">Tout afficher</button>
                </div>
            </div>

            <!-- Game section -->
            <div class="game-section">
                <button class="btn btn-primary" id="random-word">
                    Donne-moi un mot
                </button>
                <div class="game-result" id="game-result">
                    <div class="game-prompt">Clique pour commencer</div>
                </div>
            </div>

            <div style="margin-bottom: 2rem; text-align: center;">
                <button class="btn btn-primary" id="add-word-btn">+ Planter un nouveau mot</button>
            </div>

            <div class="word-grid" id="word-grid"></div>

            <!-- PDF Save Button -->
            <button class="pdf-save-btn" id="save-words-pdf" title="Sauvegarder les mots en PDF" style="display: none;">
                <svg viewBox="0 0 24 24" fill="currentColor">
                    <path d="M14 2H6c-1.1 0-2 .9-2 2v16c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V8l-6-6zm4 18H6V4h7v5h5v11zM8 15.5h8v1H8v-1zm0-3h8v1H8v-1z"/>
                </svg>
            </button>
        </section>

        <!-- Lire -->
        <section class="room" id="lire">
            <div class="room-intro">
                <h1 class="room-title">Lire</h1>
                <p class="room-description">
                    Garde une trace de ce que tu lis ou veux lire.
                </p>
            </div>

            <div style="margin-bottom: 2rem; text-align: center;">
                <button class="btn btn-primary" id="add-reading-btn">+ Ajouter un article ou livre</button>
            </div>

            <div class="resource-grid" id="reading-grid"></div>
        </section>

        <!-- Écouter -->
        <section class="room" id="ecouter">
            <div class="room-intro">
                <h1 class="room-title">Écouter</h1>
                <p class="room-description">
                    Chansons, vidéos, films — tout ce que tu écoutes pour apprendre.
                </p>
            </div>

            <div style="margin-bottom: 2rem; text-align: center;">
                <button class="btn btn-primary" id="add-listening-btn">+ Ajouter une chanson/vidéo/film</button>
            </div>

            <div class="resource-grid" id="listening-grid"></div>
        </section>

        <!-- Parler -->
        <section class="room" id="parler">
            <div class="room-intro">
                <h1 class="room-title">Parler</h1>
                <p class="room-description">
                    Réponds aux questions. Enregistre ta voix. Personne ne juge.
                </p>
            </div>

            <!-- Tabs -->
            <div class="tabs">
                <button class="tab active" data-tab="practice">Pratiquer</button>
                <button class="tab" data-tab="recordings-tab">Enregistrements</button>
            </div>

            <!-- Practice tab -->
            <div class="tab-content active" id="practice">
                <!-- Question Input with Google Doc Link -->
                <div class="question-section">
                    <div class="question-header">
                        <h3 class="question-title">Question à répondre</h3>
                        <a href="https://docs.google.com/document/d/1VRRqrIv1ZbgeH5rBHolE_v-FRdrPXLIg9n7lz-DTX6g/edit?usp=drivesdk" target="_blank" class="doc-link">
                            <svg class="svg-icon" viewBox="0 0 24 24" fill="currentColor">
                                <path d="M14 2H6c-1.1 0-1.99.9-1.99 2L4 20c0 1.1.89 2 1.99 2H18c1.1 0 2-.9 2-2V8l-6-6zm2 16H8v-2h8v2zm0-4H8v-2h8v2zm-3-5V3.5L18.5 9H13z"/>
                            </svg>
                            <span>Voir les questions</span>
                        </a>
                    </div>
                    <input type="text" class="form-input question-input" id="parler-question" placeholder="Colle ou écris ta question ici...">
                </div>

                <!-- Recording Interface -->
                <div class="entrance-card">
                    <button class="btn-speak" id="start-speaking">
                        <svg class="mic-icon" viewBox="0 0 24 24" fill="currentColor">
                            <path d="M12 14c1.66 0 3-1.34 3-3V5c0-1.66-1.34-3-3-3S9 3.34 9 5v6c0 1.66 1.34 3 3 3z"/>
                            <path d="M17 11c0 2.76-2.24 5-5 5s-5-2.24-5-5H5c0 3.53 2.61 6.43 6 6.92V21h2v-3.08c3.39-.49 6-3.39 6-6.92h-2z"/>
                        </svg>
                        Parler maintenant
                    </button>
                    
                    <div id="speaking-indicator" style="display: none; text-align: center; margin: 1rem 0; color: var(--crimson); font-weight: 500;">
                        <span style="display: inline-block; animation: pulse 1.5s ease-in-out infinite;">● En écoute...</span>
                    </div>
                    
                    <div id="spoken-text" style="min-height: 60px;"></div>
                    
                    <div class="speaking-controls" id="recording-controls" style="display: none;">
                        <input type="text" class="form-input" id="recording-note" placeholder="Ajoute une note supplémentaire (optionnel)...">
                        <button class="btn btn-secondary" id="save-recording">Sauvegarder</button>
                    </div>
                </div>
            </div>

            <!-- Recordings tab -->
            <div class="tab-content" id="recordings-tab">
                <!-- Stats Summary -->
                <div class="practice-stats" id="practice-stats" style="display: none;">
                    <div class="stat-card">
                        <div class="stat-number" id="total-recordings">0</div>
                        <div class="stat-label">Sessions totales</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number" id="this-week-recordings">0</div>
                        <div class="stat-label">Cette semaine</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number" id="total-words-spoken">0</div>
                        <div class="stat-label">Mots prononcés</div>
                    </div>
                </div>

                <div id="recordings-list"></div>
            </div>
        </section>

        <!-- Écrire -->
        <section class="room" id="ecrire">
            <div class="room-intro">
                <h1 class="room-title">Écrire</h1>
                <p class="room-description">
                    Écris ce que tu veux. Tout est sauvegardé.
                </p>
            </div>

            <!-- Tabs -->
            <div class="tabs">
                <button class="tab active" data-tab="write">Écrire</button>
                <button class="tab" data-tab="archive">Archive</button>
            </div>

            <!-- Write tab -->
            <div class="tab-content active" id="write">
                <div class="writing-container">
                    <textarea 
                        class="writing-area" 
                        id="writing-area"
                        placeholder="Commence à écrire..."></textarea>
                    
                    <div class="writing-footer">
                        <div class="word-count" id="word-count">0 mots</div>
                        <button class="btn btn-primary" id="save-writing">Sauvegarder</button>
                    </div>
                </div>
            </div>

            <!-- Archive tab -->
            <div class="tab-content" id="archive">
                <div id="writings-archive"></div>
            </div>
        </section>

        <!-- Notes -->
        <section class="room" id="notes">
            <div class="room-intro">
                <h1 class="room-title">Notes</h1>
                <p class="room-description">
                    Ta base de connaissances personnelle. Grammaire, prononciation, phrases — tout organisé.
                </p>
            </div>

            <!-- Filters -->
            <div class="filter-bar">
                <button class="filter-tag active" data-note-filter="all">Tout</button>
                <button class="filter-tag" data-note-filter="grammaire">Grammaire</button>
                <button class="filter-tag" data-note-filter="prononciation">Prononciation</button>
                <button class="filter-tag" data-note-filter="phrases">Phrases</button>
                <button class="filter-tag" data-note-filter="vocabulaire">Vocabulaire</button>
                <button class="filter-tag" data-note-filter="culture">Culture</button>
                <button class="filter-tag" data-note-filter="autre">Autre</button>
            </div>

            <!-- Add Note Button -->
            <div style="margin-bottom: 2rem; text-align: center;">
                <button class="btn btn-primary" onclick="openModal('note-modal')">+ Ajouter une note</button>
            </div>

            <!-- Notes Grid -->
            <div id="notes-grid"></div>
        </section>

        <!-- Ressources -->
        <section class="room" id="ressources">
            <div class="room-intro">
                <h1 class="room-title">Ressources</h1>
                <p class="room-description">
                    Sites web, chaînes YouTube, applications — tous tes outils pour apprendre.
                </p>
            </div>

            <div style="margin-bottom: 2rem; text-align: center;">
                <button class="btn btn-primary" id="add-resource-btn">+ Ajouter une ressource</button>
            </div>

            <div class="resource-grid" id="resources-grid"></div>
        </section>
    </main>

    <!-- Word Modal -->
    <div class="modal" id="word-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">Planter un mot</h2>
                <button class="close-btn" onclick="closeModal('word-modal')">&times;</button>
            </div>
            
            <form id="word-form">
                <div class="form-group">
                    <label class="form-label">Image (optionnel)</label>
                    <div class="image-upload-area" id="word-image-upload">
                        <p>Clique pour ajouter une image</p>
                        <img id="word-image-preview" class="image-preview" style="display: none;">
                    </div>
                    <input type="file" id="word-image-input" accept="image/*" style="display: none;">
                </div>

                <div class="form-group">
                    <label class="form-label">Le mot en français</label>
                    <input type="text" class="form-input" id="word-input" required>
                </div>

                <div class="form-group">
                    <label class="form-label">Signification / Meaning</label>
                    <input type="text" class="form-input" id="meaning-input" placeholder="What it means to you">
                </div>

                <div class="form-group">
                    <label class="form-label">Article (optionnel)</label>
                    <select class="form-select" id="article-input">
                        <option value="">—</option>
                        <option value="le">le (masculin)</option>
                        <option value="la">la (féminin)</option>
                        <option value="l'">l' (voyelle)</option>
                        <option value="les">les (pluriel)</option>
                    </select>
                </div>

                <div class="form-group">
                    <label class="form-label">Genre (optionnel)</label>
                    <select class="form-select" id="gender-input">
                        <option value="">—</option>
                        <option value="m">masculin</option>
                        <option value="f">féminin</option>
                    </select>
                </div>

                <div class="category-grid">
                    <div>
                        <label class="form-label">Thème / Topic</label>
                        <input type="text" class="form-input" id="theme-input" placeholder="ex: amour, mode, cuisine..." list="theme-suggestions">
                        <datalist id="theme-suggestions">
                            <option value="amour">
                            <option value="mode">
                            <option value="nature">
                            <option value="nourriture">
                            <option value="voyage">
                            <option value="art">
                            <option value="musique">
                            <option value="émotions">
                        </datalist>
                    </div>

                    <div>
                        <label class="form-label">Semaine / Week</label>
                        <select class="form-select" id="week-input">
                            <option value="">—</option>
                            <option value="1">Semaine 1</option>
                            <option value="2">Semaine 2</option>
                            <option value="3">Semaine 3</option>
                            <option value="4">Semaine 4</option>
                            <option value="5">Semaine 5</option>
                            <option value="6">Semaine 6</option>
                            <option value="7">Semaine 7</option>
                            <option value="8">Semaine 8</option>
                            <option value="9">Semaine 9</option>
                            <option value="10">Semaine 10</option>
                            <option value="11">Semaine 11</option>
                            <option value="12">Semaine 12</option>
                        </select>
                    </div>

                    <div>
                        <label class="form-label">Trimestre / Quarter</label>
                        <select class="form-select" id="quarter-input">
                            <option value="">—</option>
                            <option value="Q1">Q1</option>
                            <option value="Q2">Q2</option>
                            <option value="Q3">Q3</option>
                            <option value="Q4">Q4</option>
                        </select>
                    </div>

                    <div>
                        <label class="form-label">Année / Year</label>
                        <select class="form-select" id="year-input">
                            <option value="">—</option>
                            <option value="2026">2026</option>
                            <option value="2027">2027</option>
                            <option value="2028">2028</option>
                            <option value="2029">2029</option>
                            <option value="2030">2030</option>
                        </select>
                    </div>
                </div>

                <div class="form-group">
                    <label class="form-label">Contexte neutre</label>
                    <input type="text" class="form-input" id="context1" placeholder="Une phrase simple avec ce mot">
                </div>

                <div class="form-group">
                    <label class="form-label">Contexte émotionnel (optionnel)</label>
                    <input type="text" class="form-input" id="context2" placeholder="Une phrase qui a du sens pour toi">
                </div>

                <div class="form-group">
                    <label class="form-label">Contexte idiomatique (optionnel)</label>
                    <input type="text" class="form-input" id="context3" placeholder="Expression ou phrase naturelle">
                </div>

                <div class="form-group">
                    <label class="form-label">Note personnelle (optionnel)</label>
                    <textarea class="form-textarea" id="note-input" placeholder="Pourquoi ce mot t'intéresse ? D'où vient-il ?"></textarea>
                </div>

                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('word-modal')">Annuler</button>
                    <button type="submit" class="btn btn-primary">Planter</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Edit Word Modal -->
    <div class="modal" id="edit-word-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">Modifier le mot</h2>
                <button class="close-btn" onclick="closeModal('edit-word-modal')">&times;</button>
            </div>
            
            <form id="edit-word-form">
                <input type="hidden" id="edit-word-id">
                
                <div class="form-group">
                    <label class="form-label">Image (optionnel)</label>
                    <div class="image-upload-area" id="edit-word-image-upload">
                        <p>Clique pour changer l'image</p>
                        <img id="edit-word-image-preview" class="image-preview" style="display: none;">
                    </div>
                    <input type="file" id="edit-word-image-input" accept="image/*" style="display: none;">
                </div>

                <div class="form-group">
                    <label class="form-label">Le mot en français</label>
                    <input type="text" class="form-input" id="edit-word-input" required>
                </div>

                <div class="form-group">
                    <label class="form-label">Signification / Meaning</label>
                    <input type="text" class="form-input" id="edit-meaning-input">
                </div>

                <div class="form-group">
                    <label class="form-label">Article (optionnel)</label>
                    <select class="form-select" id="edit-article-input">
                        <option value="">—</option>
                        <option value="le">le (masculin)</option>
                        <option value="la">la (féminin)</option>
                        <option value="l'">l' (voyelle)</option>
                        <option value="les">les (pluriel)</option>
                    </select>
                </div>

                <div class="form-group">
                    <label class="form-label">Genre (optionnel)</label>
                    <select class="form-select" id="edit-gender-input">
                        <option value="">—</option>
                        <option value="m">masculin</option>
                        <option value="f">féminin</option>
                    </select>
                </div>

                <div class="category-grid">
                    <div>
                        <label class="form-label">Thème / Topic</label>
                        <input type="text" class="form-input" id="edit-theme-input" list="theme-suggestions">
                    </div>

                    <div>
                        <label class="form-label">Semaine / Week</label>
                        <select class="form-select" id="edit-week-input">
                            <option value="">—</option>
                            <option value="1">Semaine 1</option>
                            <option value="2">Semaine 2</option>
                            <option value="3">Semaine 3</option>
                            <option value="4">Semaine 4</option>
                            <option value="5">Semaine 5</option>
                            <option value="6">Semaine 6</option>
                            <option value="7">Semaine 7</option>
                            <option value="8">Semaine 8</option>
                            <option value="9">Semaine 9</option>
                            <option value="10">Semaine 10</option>
                            <option value="11">Semaine 11</option>
                            <option value="12">Semaine 12</option>
                        </select>
                    </div>

                    <div>
                        <label class="form-label">Trimestre / Quarter</label>
                        <select class="form-select" id="edit-quarter-input">
                            <option value="">—</option>
                            <option value="Q1">Q1</option>
                            <option value="Q2">Q2</option>
                            <option value="Q3">Q3</option>
                            <option value="Q4">Q4</option>
                        </select>
                    </div>

                    <div>
                        <label class="form-label">Année / Year</label>
                        <select class="form-select" id="edit-year-input">
                            <option value="">—</option>
                            <option value="2026">2026</option>
                            <option value="2027">2027</option>
                            <option value="2028">2028</option>
                            <option value="2029">2029</option>
                            <option value="2030">2030</option>
                        </select>
                    </div>
                </div>

                <div class="form-group">
                    <label class="form-label">Contexte neutre</label>
                    <input type="text" class="form-input" id="edit-context1">
                </div>

                <div class="form-group">
                    <label class="form-label">Contexte émotionnel (optionnel)</label>
                    <input type="text" class="form-input" id="edit-context2">
                </div>

                <div class="form-group">
                    <label class="form-label">Contexte idiomatique (optionnel)</label>
                    <input type="text" class="form-input" id="edit-context3">
                </div>

                <div class="form-group">
                    <label class="form-label">Note personnelle (optionnel)</label>
                    <textarea class="form-textarea" id="edit-note-input"></textarea>
                </div>

                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('edit-word-modal')">Annuler</button>
                    <button type="submit" class="btn btn-primary">Sauvegarder</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Reading Modal -->
    <div class="modal" id="reading-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">Ajouter à ta bibliothèque</h2>
                <button class="close-btn" onclick="closeModal('reading-modal')">&times;</button>
            </div>
            
            <form id="reading-form">
                <div class="form-group">
                    <label class="form-label">Type</label>
                    <select class="form-select" id="reading-type" required>
                        <option value="article">Article</option>
                        <option value="book">Livre</option>
                        <option value="blog">Blog</option>
                        <option value="other">Autre</option>
                    </select>
                </div>

                <div class="form-group">
                    <label class="form-label">Titre</label>
                    <input type="text" class="form-input" id="reading-title" required>
                </div>

                <div class="form-group">
                    <label class="form-label">Lien (optionnel)</label>
                    <input type="url" class="form-input" id="reading-link" placeholder="https://...">
                </div>

                <div class="form-group">
                    <label class="form-label">Statut</label>
                    <select class="form-select" id="reading-status">
                        <option value="want">Je veux lire</option>
                        <option value="reading">En train de lire</option>
                        <option value="done">Lu</option>
                    </select>
                </div>

                <div class="form-group">
                    <label class="form-label">Notes</label>
                    <textarea class="form-textarea" id="reading-note" placeholder="Pourquoi tu veux lire ça ? Qu'est-ce que tu en penses ?"></textarea>
                </div>

                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('reading-modal')">Annuler</button>
                    <button type="submit" class="btn btn-primary">Ajouter</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Listening Modal -->
    <div class="modal" id="listening-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">Ajouter à écouter</h2>
                <button class="close-btn" onclick="closeModal('listening-modal')">&times;</button>
            </div>
            
            <form id="listening-form">
                <div class="form-group">
                    <label class="form-label">Type</label>
                    <select class="form-select" id="listening-type" required>
                        <option value="song">Chanson</option>
                        <option value="video">Vidéo YouTube</option>
                        <option value="movie">Film</option>
                        <option value="series">Série</option>
                        <option value="podcast">Podcast</option>
                        <option value="other">Autre</option>
                    </select>
                </div>

                <div class="form-group">
                    <label class="form-label">Titre</label>
                    <input type="text" class="form-input" id="listening-title" required>
                </div>

                <div class="form-group">
                    <label class="form-label">Lien (optionnel)</label>
                    <input type="url" class="form-input" id="listening-link" placeholder="https://...">
                </div>

                <div class="form-group">
                    <label class="form-label">Lien paroles/transcription (optionnel)</label>
                    <input type="url" class="form-input" id="listening-transcript" placeholder="https://...">
                </div>

                <div class="form-group">
                    <label class="form-label">Notes</label>
                    <textarea class="form-textarea" id="listening-note" placeholder="Qu'est-ce que tu apprends ? Expressions intéressantes ?"></textarea>
                </div>

                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('listening-modal')">Annuler</button>
                    <button type="submit" class="btn btn-primary">Ajouter</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Resources Modal -->
    <div class="modal" id="resources-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">Ajouter une ressource</h2>
                <button class="close-btn" onclick="closeModal('resources-modal')">&times;</button>
            </div>
            
            <form id="resources-form">
                <div class="form-group">
                    <label class="form-label">Type</label>
                    <select class="form-select" id="resources-type" required>
                        <option value="website">Site Web</option>
                        <option value="youtube">Chaîne YouTube</option>
                        <option value="app">Application</option>
                        <option value="podcast">Podcast</option>
                        <option value="tool">Outil</option>
                        <option value="course">Cours</option>
                        <option value="other">Autre</option>
                    </select>
                </div>

                <div class="form-group">
                    <label class="form-label">Nom</label>
                    <input type="text" class="form-input" id="resources-name" required placeholder="Ex: Duolingo, French Today...">
                </div>

                <div class="form-group">
                    <label class="form-label">Description</label>
                    <input type="text" class="form-input" id="resources-description" placeholder="À quoi sert cette ressource ?">
                </div>

                <div class="form-group">
                    <label class="form-label">Lien (optionnel mais recommandé)</label>
                    <input type="url" class="form-input" id="resources-link" placeholder="https://...">
                </div>

                <div class="form-group">
                    <label class="form-label">Notes personnelles</label>
                    <textarea class="form-textarea" id="resources-note" placeholder="Pourquoi tu aimes cette ressource ? Comment tu l'utilises ?"></textarea>
                </div>

                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('resources-modal')">Annuler</button>
                    <button type="submit" class="btn btn-primary">Ajouter</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Note Modal -->
    <div class="modal" id="note-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">Ajouter une note</h2>
                <button class="close-btn" onclick="closeModal('note-modal')">&times;</button>
            </div>
            
            <form id="note-form">
                <div class="form-group">
                    <label class="form-label">Catégorie</label>
                    <select class="form-select" id="note-category" required>
                        <option value="">Choisir...</option>
                        <option value="grammaire">Grammaire</option>
                        <option value="prononciation">Prononciation</option>
                        <option value="phrases">Phrases</option>
                        <option value="vocabulaire">Vocabulaire</option>
                        <option value="culture">Culture</option>
                        <option value="autre">Autre</option>
                    </select>
                </div>

                <div class="form-group">
                    <label class="form-label">Titre / Question</label>
                    <input type="text" class="form-input" id="note-title" placeholder="ex: Comment utiliser le subjonctif ?" required>
                </div>

                <div class="form-group">
                    <label class="form-label">Contenu / Réponse</label>
                    <textarea class="form-textarea" id="note-content" rows="6" placeholder="Écris ta note ici..." required></textarea>
                </div>

                <div class="form-group">
                    <label class="form-label">Lien (optionnel)</label>
                    <input type="url" class="form-input" id="note-link" placeholder="https://...">
                </div>

                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('note-modal')">Annuler</button>
                    <button type="submit" class="btn btn-primary">Sauvegarder</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Hidden file input for import -->
    <input type="file" id="import-file-input" accept=".json" style="display: none;">

    <!-- Floating Heart -->
    <svg class="floating-heart" width="80" height="80" viewBox="0 0 24 24" fill="#A64253">
        <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
    </svg>

    <script>
        // ============================================
        // DATA MANAGEMENT
        // ============================================
        let vocabulary = JSON.parse(localStorage.getItem('vocabulary') || '[]');
        let writings = JSON.parse(localStorage.getItem('writings') || '[]');
        let readingList = JSON.parse(localStorage.getItem('readingList') || '[]');
        let listeningList = JSON.parse(localStorage.getItem('listeningList') || '[]');
        let recordings = JSON.parse(localStorage.getItem('recordings') || '[]');
        let resourcesList = JSON.parse(localStorage.getItem('resourcesList') || '[]');
        let notes = JSON.parse(localStorage.getItem('notes') || '[]');

        let currentRecording = null;

        // ============================================
        // FILTER STATE - NEW
        // ============================================
        let activeFilters = {
            year: "",
            quarter: "",
            week: "",
            theme: ""
        };

        // ============================================
        // IMPORT / EXPORT - FIXED
        // ============================================
        document.getElementById('export-data').addEventListener('click', () => {
            const data = {
                vocabulary,
                writings,
                readingList,
                listeningList,
                recordings,
                resourcesList,
                notes,
                exportDate: new Date().toISOString()
            };

            const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `ma-maison-${new Date().toISOString().split('T')[0]}.json`;
            a.click();
            URL.revokeObjectURL(url);
        });

        // FIX: Added missing import button click handler
        document.getElementById('import-data').addEventListener('click', () => {
            document.getElementById('import-file-input').click();
        });

        document.getElementById('import-file-input').addEventListener('change', (e) => {
            const file = e.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = (event) => {
                try {
                    const data = JSON.parse(event.target.result);
                    
                    if (confirm('Importer ces données ? Cela remplacera tout ce que tu as actuellement.')) {
                        vocabulary = data.vocabulary || [];
                        writings = data.writings || [];
                        readingList = data.readingList || [];
                        listeningList = data.listeningList || [];
                        recordings = data.recordings || [];
                        resourcesList = data.resourcesList || [];
                        notes = data.notes || [];
                        
                        localStorage.setItem('vocabulary', JSON.stringify(vocabulary));
                        localStorage.setItem('writings', JSON.stringify(writings));
                        localStorage.setItem('readingList', JSON.stringify(readingList));
                        localStorage.setItem('listeningList', JSON.stringify(listeningList));
                        localStorage.setItem('recordings', JSON.stringify(recordings));
                        localStorage.setItem('resourcesList', JSON.stringify(resourcesList));
                        localStorage.setItem('notes', JSON.stringify(notes));
                        
                        renderGarden();
                        populateJardinFilters(); // NEW
                        renderReadingList();
                        renderListeningList();
                        renderRecordings();
                        renderWritingsArchive();
                        renderResourcesList();
                        renderNotes();
                        
                        alert('Données importées avec succès ✓');
                    }
                } catch (err) {
                    alert('Erreur : fichier invalide');
                    console.error(err);
                }
            };
            reader.readAsText(file);
            // Reset the file input
            e.target.value = '';
        });

        document.getElementById('drive-link').addEventListener('click', () => {
            window.open('https://drive.google.com/drive/folders/1E7JYANvw4DjaJ2VUsPZuuSExqB4PzU9f', '_blank');
        });

        document.getElementById('reset-data').addEventListener('click', () => {
            if (confirm('Vraiment tout effacer ? Cette action est irréversible.')) {
                if (confirm('Dernière confirmation — tu es sûr ?')) {
                    localStorage.clear();
                    vocabulary = [];
                    writings = [];
                    readingList = [];
                    listeningList = [];
                    recordings = [];
                    resourcesList = [];
                    activeFilters = { year: "", quarter: "", week: "", theme: "" }; // NEW
                    renderGarden();
                    populateJardinFilters(); // NEW
                    renderReadingList();
                    renderListeningList();
                    renderRecordings();
                    renderWritingsArchive();
                    renderResourcesList();
                    alert('Tout a été effacé. Tu peux recommencer.');
                }
            }
        });

        // ============================================
        // AFFIRMATIONS
        // ============================================
        const affirmations = [
            { fr: "Tu es en train d'apprendre.", en: "You are learning." },
            { fr: "Chaque mot compte.", en: "Every word counts." },
            { fr: "C'est bien d'aller lentement.", en: "It's good to go slowly." },
            { fr: "Tu n'as rien à prouver.", en: "You have nothing to prove." },
            { fr: "La langue t'appartient déjà.", en: "The language already belongs to you." },
            { fr: "Être débutant, c'est courageux.", en: "Being a beginner is brave." },
            { fr: "Ce que tu fais compte.", en: "What you do matters." },
            { fr: "Tu es déjà assez.", en: "You are already enough." },
            { fr: "La beauté n'est pas une faiblesse.", en: "Beauty is not weakness." },
            { fr: "Tu apprends plus vite que tu crois.", en: "You learn faster than you think." },
            { fr: "Prends ton temps.", en: "Take your time." },
            { fr: "Tu es capable.", en: "You are capable." }
        ];

        function showAffirmation() {
            const affEl = document.getElementById('affirmation');
            const aff = affirmations[Math.floor(Math.random() * affirmations.length)];
            
            affEl.querySelector('.affirmation-text').textContent = aff.fr;
            affEl.querySelector('.affirmation-translation').textContent = aff.en;
            
            affEl.classList.add('visible');
            
            setTimeout(() => {
                affEl.classList.remove('visible');
            }, 8000);
        }

        setTimeout(() => {
            showAffirmation();
            setInterval(showAffirmation, 180000);
        }, 30000);

        // ============================================
        // SIGNATURE MAGIC - ONE RANDOM REASON
        // ============================================
        let apprendreClicks = 0;
        let apprendreTimeout;

        const poeticReasons = [
            "Pour vivre dans les rues de Paris",
            "Pour trouver l'amour au-delà des frontières",
            "Pour être libre dans ma propre peau",
            "Pour la beauté des mots qui dansent",
            "Pour défendre les droits humains, en français",
            "Pour écouter le monde avec un nouvel cœur",
            "Pour devenir qui je suis vraiment",
            "Pour lire les poèmes dans leur langue natale",
            "Pour comprendre les chansons qui font pleurer",
            "Pour écrire des lettres à des inconnus",
            "Pour voyager sans être touriste",
            "Pour rêver en couleurs différentes",
            "Pour construire une carrière avec compassion",
            "Pour sentir le monde avec plus de nuances",
            "Pour la joie de comprendre un jeu de mots",
            "Pour parler à des étrangers comme des amis",
            "Pour lire les menus sans hésitation",
            "Pour le plaisir de l'accent qui roule",
            "Pour les conversations de minuit à Paris",
            "Pour être à la fois chez soi et ailleurs"
        ];

        document.querySelector('.signature').addEventListener('click', function() {
            apprendreClicks++;
            
            // Clear previous timeout
            if (apprendreTimeout) clearTimeout(apprendreTimeout);
            
            // Set timeout to reset counter
            apprendreTimeout = setTimeout(() => {
                apprendreClicks = 0;
            }, 2000);
            
            // Show random reason on 3rd click
            if (apprendreClicks === 3) {
                this.style.color = '#D4A5A5';
                this.style.opacity = '0.9';
                this.style.transition = 'all 0.5s ease';
                
                // Show one random poetic reason
                showRandomHeartReason();
                apprendreClicks = 0;
                
                // Reset after 10 seconds
                setTimeout(() => {
                    this.style.color = 'var(--gold)';
                    this.style.opacity = '0.7';
                }, 10000);
            }
        });

        function showRandomHeartReason() {
            const randomReason = poeticReasons[Math.floor(Math.random() * poeticReasons.length)];
            const heartNote = document.getElementById('heart-note');
            const heartReason = document.getElementById('heart-reason');
            
            // Add heart icon
            heartReason.innerHTML = `
                <svg width="48" height="48" viewBox="0 0 24 24" fill="#D4A5A5" style="margin-bottom: 1rem;">
                    <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
                </svg>
                <div style="font-family: 'Cormorant Garamond'; font-size: 1.3rem; color: var(--navy); line-height: 1.6;">
                    ${randomReason}
                </div>
            `;
            
            heartNote.style.display = 'block';
            
            // Add close functionality
            heartNote.onclick = function() {
                heartNote.style.opacity = '0';
                heartNote.style.transform = 'translate(-50%, -50%) scale(0.95)';
                heartNote.style.transition = 'all 0.5s ease';
                setTimeout(() => {
                    heartNote.style.display = 'none';
                    heartNote.style.opacity = '1';
                    heartNote.style.transform = 'translate(-50%, -50%) scale(1)';
                }, 500);
            };
            
            // Auto-remove after 8 seconds
            setTimeout(() => {
                if (heartNote.style.display === 'block') {
                    heartNote.style.opacity = '0';
                    heartNote.style.transform = 'translate(-50%, -50%) scale(0.95)';
                    heartNote.style.transition = 'all 0.5s ease';
                    setTimeout(() => {
                        heartNote.style.display = 'none';
                        heartNote.style.opacity = '1';
                        heartNote.style.transform = 'translate(-50%, -50%) scale(1)';
                    }, 500);
                }
            }, 8000);
        }

        // ============================================
        // DOUBLE-CLICK MAGIC ON ICONS ✨
        // ============================================
        document.addEventListener('dblclick', function(e) {
            const icon = e.target.closest('.empty-icon');
            if (icon) {
                const svg = icon.querySelector('svg');
                if (svg) {
                    // Turn gold with animation
                    svg.style.fill = '#C9A861';
                    svg.style.opacity = '1';
                    svg.style.transform = 'scale(1.2)';
                    svg.style.transition = 'all 0.4s cubic-bezier(0.4, 0, 0.2, 1)';
                    
                    // Show affirmation
                    showAffirmation();
                    
                    // Gentle pulse then settle
                    setTimeout(() => {
                        svg.style.transform = 'scale(1.05)';
                    }, 400);
                    
                    setTimeout(() => {
                        svg.style.transform = 'scale(1)';
                    }, 700);
                }
            }
        });

        // ============================================
        // ENTRANCE PHRASES
        // ============================================
        const entrancePhrases = [
            {
                sentence: "Entre.",
                translation: "Come in.",
                note: "The imperative form of 'entrer' (to enter). A simple, direct welcome. Notice how French commands can be gentle—they invite rather than order."
            },
            {
                sentence: "Prends ton temps.",
                translation: "Take your time.",
                note: "From 'prendre' (to take). This phrase embodies permission to slow down. The reflexive 'ton temps' (your time) makes it personal."
            },
            {
                sentence: "Reste ici.",
                translation: "Stay here.",
                note: "From 'rester' (to stay). An invitation to presence. 'Ici' (here) grounds you in the moment."
            }
        ];

        function renderEntrance() {
            const container = document.getElementById('entrance-content');
            container.innerHTML = entrancePhrases.map(p => `
                <div class="entrance-card">
                    <div class="entrance-sentence">${p.sentence}</div>
                    <div class="entrance-translation">${p.translation}</div>
                    <div class="entrance-note">${p.note}</div>
                </div>
            `).join('');
        }

        // ============================================
        // IMAGE HANDLING - FIXED
        // ============================================
        function setupImageUpload(uploadAreaId, inputId, previewId) {
            const uploadArea = document.getElementById(uploadAreaId);
            const input = document.getElementById(inputId);
            const preview = document.getElementById(previewId);

            if (!uploadArea || !input || !preview) return;

            uploadArea.addEventListener('click', () => input.click());

            input.addEventListener('change', (e) => {
                const file = e.target.files[0];
                if (!file) return;

                // Check if file is an image
                if (!file.type.startsWith('image/')) {
                    alert('Veuillez sélectionner une image valide');
                    return;
                }

                const reader = new FileReader();
                reader.onload = (event) => {
                    preview.src = event.target.result;
                    preview.style.display = 'block';
                };
                reader.onerror = () => {
                    alert('Erreur lors du chargement de l\'image');
                };
                reader.readAsDataURL(file);
            });
        }

        // ============================================
        // VOCABULARY GARDEN - UPDATED WITH FILTERS
        // ============================================
        function getFilteredVocabulary() {
            return vocabulary.filter(word => {
                if (activeFilters.year && word.year !== activeFilters.year) return false;
                if (activeFilters.quarter && word.quarter !== activeFilters.quarter) return false;
                if (activeFilters.week && word.week !== activeFilters.week) return false;
                if (activeFilters.theme && word.theme !== activeFilters.theme) return false;
                return true;
            });
        }

        function renderGarden() {
            const grid = document.getElementById('word-grid');
            const filteredVocabulary = getFilteredVocabulary();
            
            if (filteredVocabulary.length === 0) {
                grid.innerHTML = `
                    <div class="empty">
                        <div class="empty-icon">
                            <svg class="svg-icon-lg" viewBox="0 0 24 24" fill="currentColor" style="opacity: 0.3;">
                                <path d="M12 22c4.97 0 9-4.03 9-9-4.97 0-9 4.03-9 9zM5.6 10.25c0 1.38 1.12 2.5 2.5 2.5.53 0 1.01-.16 1.42-.44l-.02.19c0 1.38 1.12 2.5 2.5 2.5s2.5-1.12 2.5-2.5l-.02-.19c.4.28.89.44 1.42.44 1.38 0 2.5-1.12 2.5-2.5 0-1.25-.93-2.3-2.14-2.46.4-.49.64-1.1.64-1.79 0-1.38-1.12-2.5-2.5-2.5-.53 0-1.01.16-1.42.44l.02-.19C12.5 2.12 11.38 1 10 1S7.5 2.12 7.5 3.5l.02.19c-.4-.28-.89-.44-1.42-.44-1.38 0-2.5 1.12-2.5 2.5 0 .69.24 1.3.64 1.79-1.21.16-2.14 1.21-2.14 2.46z"/>
                            </svg>
                        </div>
                        <div class="empty-text">
                            ${vocabulary.length === 0 ? 'Rien ici encore...<br>Plante ton premier mot quand tu es prêt.' : 'Aucun mot ne correspond à tes filtres.<br>Essaie avec des critères différents.'}
                        </div>
                    </div>
                `;
                updatePDFButtonVisibility();
                return;
            }

            // Sort by most recent first
            const sortedVocabulary = [...filteredVocabulary].sort((a, b) => b.id - a.id);

            grid.innerHTML = sortedVocabulary.map(word => `
                <div class="word-card">
                    <div class="word-actions">
                        <button class="icon-btn" onclick="editWord(${word.id})" title="Modifier">
                            <svg class="svg-icon" viewBox="0 0 24 24">
                                <path d="M3 17.25V21h3.75L17.81 9.94l-3.75-3.75L3 17.25zM20.71 7.04c.39-.39.39-1.02 0-1.41l-2.34-2.34c-.39-.39-1.02-.39-1.41 0l-1.83 1.83 3.75 3.75 1.83-1.83z"/>
                            </svg>
                        </button>
                        <button class="icon-btn" onclick="deleteWord(${word.id})" title="Supprimer">
                            <svg class="svg-icon" viewBox="0 0 24 24">
                                <path d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM19 4h-3.5l-1-1h-5l-1 1H5v2h14V4z"/>
                            </svg>
                        </button>
                    </div>
                    ${word.image ? `<img src="${word.image}" class="word-image" alt="${word.french}">` : ''}
                    
                    <div class="category-tags">
                        ${word.theme ? `<div class="category-tag topic">${word.theme}</div>` : ''}
                        ${word.week ? `<div class="category-tag time">Semaine ${word.week}</div>` : ''}
                        ${word.quarter ? `<div class="category-tag time">${word.quarter}</div>` : ''}
                        ${word.year ? `<div class="category-tag time">${word.year}</div>` : ''}
                    </div>
                    
                    <div class="word-french">${word.french}</div>
                    ${word.meaning ? `<div class="word-meaning">${word.meaning}</div>` : ''}
                    ${word.article ? `<div class="word-article">${word.article}</div>` : ''}
                    
                    <div class="word-contexts">
                        ${word.contexts && word.contexts[0] ? `
                            <div class="context">
                                <div class="context-label">Neutre</div>
                                <div class="context-sentence">${word.contexts[0]}</div>
                            </div>
                        ` : ''}
                        ${word.contexts && word.contexts[1] ? `
                            <div class="context">
                                <div class="context-label">Émotionnel</div>
                                <div class="context-sentence">${word.contexts[1]}</div>
                            </div>
                        ` : ''}
                        ${word.contexts && word.contexts[2] ? `
                            <div class="context">
                                <div class="context-label">Idiomatique</div>
                                <div class="context-sentence">${word.contexts[2]}</div>
                            </div>
                        ` : ''}
                    </div>
                    ${word.note ? `<div class="word-note">${word.note}</div>` : ''}
                </div>
            `).join('');
            
            updatePDFButtonVisibility();
        }

        // ============================================
        // POPULATE JARDIN FILTERS - NEW
        // ============================================
        function populateJardinFilters() {
            const years = [...new Set(vocabulary.map(w => w.year).filter(Boolean))].sort();
            const weeks = [...new Set(vocabulary.map(w => w.week).filter(Boolean))].sort((a, b) => a - b);
            const themes = [...new Set(vocabulary.map(w => w.theme).filter(Boolean))].sort();

            const yearSelect = document.getElementById('filter-year');
            const weekSelect = document.getElementById('filter-week');
            const themeSelect = document.getElementById('filter-theme');

            // Year options
            yearSelect.innerHTML = '<option value="">Toutes</option>' +
                years.map(y => `<option value="${y}">${y}</option>`).join('');

            // Week options
            weekSelect.innerHTML = '<option value="">Toutes</option>' +
                weeks.map(w => `<option value="${w}">Semaine ${w}</option>`).join('');

            // Theme options
            themeSelect.innerHTML = '<option value="">Tous les thèmes</option>' +
                themes.map(t => `<option value="${t}">${t}</option>`).join('');

            // Set current filter values if they exist
            if (activeFilters.year) yearSelect.value = activeFilters.year;
            if (activeFilters.week) weekSelect.value = activeFilters.week;
            if (activeFilters.theme) themeSelect.value = activeFilters.theme;
            if (activeFilters.quarter) document.getElementById('filter-quarter').value = activeFilters.quarter;
        }

        // ============================================
        // FILTER EVENT LISTENERS - NEW
        // ============================================
        function setupFilterListeners() {
            document.getElementById('filter-year').addEventListener('change', e => {
                activeFilters.year = e.target.value;
                renderGarden();
            });

            document.getElementById('filter-quarter').addEventListener('change', e => {
                activeFilters.quarter = e.target.value;
                renderGarden();
            });

            document.getElementById('filter-week').addEventListener('change', e => {
                activeFilters.week = e.target.value;
                renderGarden();
            });

            document.getElementById('filter-theme').addEventListener('change', e => {
                activeFilters.theme = e.target.value;
                renderGarden();
            });

            document.getElementById('reset-filters').addEventListener('click', () => {
                activeFilters = { year: "", quarter: "", week: "", theme: "" };

                document.getElementById('filter-year').value = "";
                document.getElementById('filter-quarter').value = "";
                document.getElementById('filter-week').value = "";
                document.getElementById('filter-theme').value = "";

                renderGarden();
            });
        }

        function openModal(id) {
            document.getElementById(id).classList.add('active');
            
            // AUTO-FILL FILTERS WHEN ADDING A WORD - NEW
            if (id === 'word-modal') {
                document.getElementById('year-input').value = activeFilters.year || "";
                document.getElementById('quarter-input').value = activeFilters.quarter || "";
                document.getElementById('week-input').value = activeFilters.week || "";
                document.getElementById('theme-input').value = activeFilters.theme || "";
            }
        }

        function closeModal(id) {
            document.getElementById(id).classList.remove('active');
            const forms = ['word-form', 'edit-word-form', 'reading-form', 'listening-form', 'resources-form'];
            forms.forEach(formId => {
                const form = document.getElementById(formId);
                if (form) form.reset();
            });
            
            // Reset image previews
            const previews = ['word-image-preview', 'edit-word-image-preview'];
            previews.forEach(previewId => {
                const preview = document.getElementById(previewId);
                if (preview) {
                    preview.style.display = 'none';
                    preview.src = '';
                }
            });
            
            // Reset file inputs
            const fileInputs = ['word-image-input', 'edit-word-image-input'];
            fileInputs.forEach(inputId => {
                const input = document.getElementById(inputId);
                if (input) input.value = '';
            });
        }

        function editWord(id) {
            const word = vocabulary.find(w => w.id === id);
            if (!word) return;

            document.getElementById('edit-word-id').value = id;
            document.getElementById('edit-word-input').value = word.french;
            document.getElementById('edit-meaning-input').value = word.meaning || '';
            document.getElementById('edit-article-input').value = word.article || '';
            document.getElementById('edit-gender-input').value = word.gender || '';
            document.getElementById('edit-theme-input').value = word.theme || '';
            document.getElementById('edit-week-input').value = word.week || '';
            document.getElementById('edit-quarter-input').value = word.quarter || '';
            document.getElementById('edit-year-input').value = word.year || '';
            document.getElementById('edit-context1').value = word.contexts && word.contexts[0] ? word.contexts[0] : '';
            document.getElementById('edit-context2').value = word.contexts && word.contexts[1] ? word.contexts[1] : '';
            document.getElementById('edit-context3').value = word.contexts && word.contexts[2] ? word.contexts[2] : '';
            document.getElementById('edit-note-input').value = word.note || '';

            if (word.image) {
                const preview = document.getElementById('edit-word-image-preview');
                preview.src = word.image;
                preview.style.display = 'block';
            }

            openModal('edit-word-modal');
        }

        function deleteWord(id) {
            if (confirm('Supprimer ce mot ?')) {
                vocabulary = vocabulary.filter(w => w.id !== id);
                localStorage.setItem('vocabulary', JSON.stringify(vocabulary));
                renderGarden();
                populateJardinFilters(); // Update filters after deletion
            }
        }

        // ============================================
        // ADD WORD - FIXED
        // ============================================
        document.getElementById('word-form').addEventListener('submit', (e) => {
            e.preventDefault();
            
            const imagePreview = document.getElementById('word-image-preview');
            
            const word = {
                id: Date.now(),
                french: document.getElementById('word-input').value.trim(),
                meaning: document.getElementById('meaning-input').value.trim() || '',
                article: document.getElementById('article-input').value,
                gender: document.getElementById('gender-input').value,
                theme: document.getElementById('theme-input').value.trim() || '',
                week: document.getElementById('week-input').value || '',
                quarter: document.getElementById('quarter-input').value || '',
                year: document.getElementById('year-input').value || '',
                contexts: [
                    document.getElementById('context1').value.trim(),
                    document.getElementById('context2').value.trim(),
                    document.getElementById('context3').value.trim()
                ].filter(Boolean),
                note: document.getElementById('note-input').value.trim() || '',
                image: imagePreview.style.display !== 'none' ? imagePreview.src : null,
                created: new Date().toISOString()
            };

            // Validate required field
            if (!word.french) {
                alert('Veuillez entrer un mot en français');
                return;
            }

            vocabulary.push(word);
            localStorage.setItem('vocabulary', JSON.stringify(vocabulary));
            renderGarden();
            populateJardinFilters(); // Update filters after adding
            closeModal('word-modal');
        });

        // ============================================
        // EDIT WORD - FIXED
        // ============================================
        document.getElementById('edit-word-form').addEventListener('submit', (e) => {
            e.preventDefault();
            
            const id = parseInt(document.getElementById('edit-word-id').value);
            const index = vocabulary.findIndex(w => w.id === id);
            
            if (index === -1) return;

            const imagePreview = document.getElementById('edit-word-image-preview');

            vocabulary[index] = {
                ...vocabulary[index],
                french: document.getElementById('edit-word-input').value.trim(),
                meaning: document.getElementById('edit-meaning-input').value.trim() || '',
                article: document.getElementById('edit-article-input').value,
                gender: document.getElementById('edit-gender-input').value,
                theme: document.getElementById('edit-theme-input').value.trim() || '',
                week: document.getElementById('edit-week-input').value || '',
                quarter: document.getElementById('edit-quarter-input').value || '',
                year: document.getElementById('edit-year-input').value || '',
                contexts: [
                    document.getElementById('edit-context1').value.trim(),
                    document.getElementById('edit-context2').value.trim(),
                    document.getElementById('edit-context3').value.trim()
                ].filter(Boolean),
                note: document.getElementById('edit-note-input').value.trim() || '',
                image: imagePreview.style.display !== 'none' ? imagePreview.src : vocabulary[index].image
            };

            // Validate required field
            if (!vocabulary[index].french) {
                alert('Veuillez entrer un mot en français');
                return;
            }

            localStorage.setItem('vocabulary', JSON.stringify(vocabulary));
            renderGarden();
            populateJardinFilters(); // Update filters after editing
            closeModal('edit-word-modal');
        });

        // ============================================
        // RANDOM WORD GAME - UPDATED FOR FILTERS
        // ============================================
        document.getElementById('random-word').addEventListener('click', () => {
            const filteredVocabulary = getFilteredVocabulary();
            
            if (filteredVocabulary.length === 0) {
                document.getElementById('game-result').innerHTML = `
                    <div class="game-prompt">${vocabulary.length === 0 ? 'Plante quelques mots d\'abord' : 'Aucun mot ne correspond à tes filtres'}</div>
                `;
                return;
            }

            const word = filteredVocabulary[Math.floor(Math.random() * filteredVocabulary.length)];
            const prompts = [
                "Utilise ce mot dans une phrase",
                "Dis-le à voix haute",
                "Écris une émotion avec ce mot",
                "Trouve un synonyme",
                "Conjugue ce verbe (ou invente une phrase)",
                "Dessine ce que ce mot signifie pour toi"
            ];
            const prompt = prompts[Math.floor(Math.random() * prompts.length)];

            document.getElementById('game-result').innerHTML = `
                <div class="game-word">${word.french}</div>
                <div class="game-prompt">${prompt}</div>
            `;
        });

        // ============================================
        // READING LIST - FIXED
        // ============================================
        function renderReadingList() {
            const grid = document.getElementById('reading-grid');
            
            if (readingList.length === 0) {
                grid.innerHTML = `
                    <div class="empty">
                        <div class="empty-icon">
                            <svg class="svg-icon-lg" viewBox="0 0 24 24" fill="currentColor" style="opacity: 0.3;">
                                <path d="M21 5c-1.11-.35-2.33-.5-3.5-.5-1.95 0-4.05.4-5.5 1.5-1.45-1.1-3.55-1.5-5.5-1.5S2.45 4.9 1 6v14.65c0 .25.25.5.5.5.1 0 .15-.05.25-.05C3.1 20.45 5.05 20 6.5 20c1.95 0 4.05.4 5.5 1.5 1.35-.85 3.8-1.5 5.5-1.5 1.65 0 3.35.3 4.75 1.05.1.05.15.05.25.05.25 0 .5-.25.5-.5V6c-.6-.45-1.25-.75-2-1zm0 13.5c-1.1-.35-2.3-.5-3.5-.5-1.7 0-4.15.65-5.5 1.5V8c1.35-.85 3.8-1.5 5.5-1.5 1.2 0 2.4.15 3.5.5v11.5z"/>
                            </svg>
                        </div>
                        <div class="empty-text">Rien ici encore...</div>
                    </div>
                `;
                return;
            }

            const statusLabels = {
                want: 'Je veux lire',
                reading: 'En train de lire',
                done: 'Lu'
            };

            // Sort by most recent first
            const sortedReadingList = [...readingList].sort((a, b) => b.id - a.id);

            grid.innerHTML = sortedReadingList.map(item => `
                <div class="resource-card">
                    <div class="resource-info">
                        <div class="resource-type">${item.type}</div>
                        <div class="resource-title">${item.title}</div>
                        ${item.link ? `<a href="${item.link}" class="resource-link" target="_blank" rel="noopener noreferrer">${item.link}</a>` : ''}
                        ${item.note ? `<div class="resource-note">${item.note}</div>` : ''}
                        <div class="resource-status">${statusLabels[item.status]}</div>
                    </div>
                    <button class="icon-btn" onclick="deleteReading(${item.id})" title="Supprimer">
                        <svg class="svg-icon" viewBox="0 0 24 24">
                            <path d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM19 4h-3.5l-1-1h-5l-1 1H5v2h14V4z"/>
                        </svg>
                    </button>
                </div>
            `).join('');
        }

        function deleteReading(id) {
            if (confirm('Supprimer cet article ?')) {
                readingList = readingList.filter(r => r.id !== id);
                localStorage.setItem('readingList', JSON.stringify(readingList));
                renderReadingList();
            }
        }

        document.getElementById('add-reading-btn').addEventListener('click', () => {
            openModal('reading-modal');
        });

        document.getElementById('reading-form').addEventListener('submit', (e) => {
            e.preventDefault();
            
            const item = {
                id: Date.now(),
                type: document.getElementById('reading-type').value,
                title: document.getElementById('reading-title').value.trim(),
                link: document.getElementById('reading-link').value.trim(),
                status: document.getElementById('reading-status').value,
                note: document.getElementById('reading-note').value.trim() || '',
                created: new Date().toISOString()
            };

            // Validate required field
            if (!item.title) {
                alert('Veuillez entrer un titre');
                return;
            }

            readingList.push(item);
            localStorage.setItem('readingList', JSON.stringify(readingList));
            renderReadingList();
            closeModal('reading-modal');
        });

        // ============================================
        // LISTENING LIST - FIXED
        // ============================================
        function renderListeningList() {
            const grid = document.getElementById('listening-grid');
            
            if (listeningList.length === 0) {
                grid.innerHTML = `
                    <div class="empty">
                        <div class="empty-icon">
                            <svg class="svg-icon-lg" viewBox="0 0 24 24" fill="currentColor" style="opacity: 0.3;">
                                <path d="M12 3v9.28c-.47-.17-.97-.28-1.5-.28C8.01 12 6 14.01 6 16.5S8.01 21 10.5 21c2.31 0 4.2-1.75 4.45-4H15V6h4V3h-7z"/>
                            </svg>
                        </div>
                        <div class="empty-text">Rien ici encore...</div>
                    </div>
                `;
                return;
            }

            // Sort by most recent first
            const sortedListeningList = [...listeningList].sort((a, b) => b.id - a.id);

            grid.innerHTML = sortedListeningList.map(item => `
                <div class="resource-card">
                    <div class="resource-info">
                        <div class="resource-type">${item.type}</div>
                        <div class="resource-title">${item.title}</div>
                        ${item.link ? `<a href="${item.link}" class="resource-link" target="_blank" rel="noopener noreferrer">${item.link}</a>` : ''}
                        ${item.note ? `<div class="resource-note">${item.note}</div>` : ''}
                    </div>
                    <div class="resource-actions">
                        ${item.transcriptLink ? `
                            <a href="${item.transcriptLink}" class="transcript-btn" target="_blank" rel="noopener noreferrer" title="Voir les paroles/transcription">
                                <svg viewBox="0 0 24 24" fill="currentColor">
                                    <path d="M14 2H6c-1.1 0-1.99.9-1.99 2L4 20c0 1.1.89 2 1.99 2H18c1.1 0 2-.9 2-2V8l-6-6zm2 16H8v-2h8v2zm0-4H8v-2h8v2zm-3-5V3.5L18.5 9H13z"/>
                                </svg>
                            </a>
                        ` : ''}
                        <button class="icon-btn" onclick="deleteListening(${item.id})" title="Supprimer">
                            <svg class="svg-icon" viewBox="0 0 24 24">
                                <path d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM19 4h-3.5l-1-1h-5l-1 1H5v2h14V4z"/>
                            </svg>
                        </button>
                    </div>
                </div>
            `).join('');
        }

        function deleteListening(id) {
            if (confirm('Supprimer ce média ?')) {
                listeningList = listeningList.filter(l => l.id !== id);
                localStorage.setItem('listeningList', JSON.stringify(listeningList));
                renderListeningList();
            }
        }

        document.getElementById('add-listening-btn').addEventListener('click', () => {
            openModal('listening-modal');
        });

        document.getElementById('listening-form').addEventListener('submit', (e) => {
            e.preventDefault();
            
            const item = {
                id: Date.now(),
                type: document.getElementById('listening-type').value,
                title: document.getElementById('listening-title').value.trim(),
                link: document.getElementById('listening-link').value.trim(),
                transcriptLink: document.getElementById('listening-transcript').value.trim(),
                note: document.getElementById('listening-note').value.trim() || '',
                created: new Date().toISOString()
            };

            // Validate required field
            if (!item.title) {
                alert('Veuillez entrer un titre');
                return;
            }

            listeningList.push(item);
            localStorage.setItem('listeningList', JSON.stringify(listeningList));
            renderListeningList();
            closeModal('listening-modal');
        });

        // ============================================
        // RESOURCES LIST - FIXED
        // ============================================
        function renderResourcesList() {
            const grid = document.getElementById('resources-grid');
            
            if (resourcesList.length === 0) {
                grid.innerHTML = `
                    <div class="empty">
                        <div class="empty-icon">
                            <svg class="svg-icon-lg" viewBox="0 0 24 24" fill="currentColor" style="opacity: 0.3;">
                                <path d="M3.9 12c0-1.71 1.39-3.1 3.1-3.1h4V7H7c-2.76 0-5 2.24-5 5s2.24 5 5 5h4v-1.9H7c-1.71 0-3.1-1.39-3.1-3.1zM8 13h8v-2H8v2zm9-6h-4v1.9h4c1.71 0 3.1 1.39 3.1 3.1s-1.39 3.1-3.1 3.1h-4V17h4c2.76 0 5-2.24 5-5s-2.24-5-5-5z"/>
                            </svg>
                        </div>
                        <div class="empty-text">Rien ici encore...</div>
                    </div>
                `;
                return;
            }

            const typeLabels = {
                website: 'Site Web',
                youtube: 'YouTube',
                app: 'Application',
                podcast: 'Podcast',
                tool: 'Outil',
                course: 'Cours',
                other: 'Autre'
            };

            // Sort by most recent first
            const sortedResourcesList = [...resourcesList].sort((a, b) => b.id - a.id);

            grid.innerHTML = sortedResourcesList.map(item => `
                <div class="resource-card">
                    <div class="resource-info">
                        <div class="resource-type">${typeLabels[item.type] || item.type}</div>
                        <div class="resource-title">${item.name}</div>
                        ${item.description ? `<div class="resource-note" style="margin-bottom: 0.5rem;">${item.description}</div>` : ''}
                        ${item.link ? `<a href="${item.link}" class="resource-link" target="_blank" rel="noopener noreferrer">${item.link}</a>` : ''}
                        ${item.note ? `<div class="resource-note">${item.note}</div>` : ''}
                    </div>
                    <button class="icon-btn" onclick="deleteResource(${item.id})" title="Supprimer">
                        <svg class="svg-icon" viewBox="0 0 24 24">
                            <path d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM19 4h-3.5l-1-1h-5l-1 1H5v2h14V4z"/>
                        </svg>
                    </button>
                </div>
            `).join('');
        }

        function deleteResource(id) {
            if (confirm('Supprimer cette ressource ?')) {
                resourcesList = resourcesList.filter(r => r.id !== id);
                localStorage.setItem('resourcesList', JSON.stringify(resourcesList));
                renderResourcesList();
            }
        }

        document.getElementById('add-resource-btn').addEventListener('click', () => {
            openModal('resources-modal');
        });

        document.getElementById('resources-form').addEventListener('submit', (e) => {
            e.preventDefault();
            
            const item = {
                id: Date.now(),
                type: document.getElementById('resources-type').value,
                name: document.getElementById('resources-name').value.trim(),
                description: document.getElementById('resources-description').value.trim() || '',
                link: document.getElementById('resources-link').value.trim(),
                note: document.getElementById('resources-note').value.trim() || '',
                created: new Date().toISOString()
            };

            // Validate required field
            if (!item.name) {
                alert('Veuillez entrer un nom');
                return;
            }

            resourcesList.push(item);
            localStorage.setItem('resourcesList', JSON.stringify(resourcesList));
            renderResourcesList();
            closeModal('resources-modal');
        });

        // ============================================
        // SPEAKING - FIXED VERSION
        // ============================================
        function initializeSpeechRecognition() {
            const startSpeakingBtn = document.getElementById('start-speaking');
            const spokenText = document.getElementById('spoken-text');
            const indicator = document.getElementById('speaking-indicator');
            const controls = document.getElementById('recording-controls');
            
            if (!startSpeakingBtn) return;
            
            const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
            
            if (SpeechRecognition) {
                let recognition;
                let isRecognizing = false;
                
                try {
                    recognition = new SpeechRecognition();
                    recognition.lang = 'fr-FR';
                    recognition.continuous = false;
                    recognition.interimResults = false;
                    
                    startSpeakingBtn.addEventListener('click', function() {
                        if (isRecognizing) {
                            recognition.stop();
                            isRecognizing = false;
                            indicator.style.display = 'none';
                            return;
                        }
                        
                        spokenText.textContent = 'Écoute... (parle maintenant)';
                        indicator.style.display = 'block';
                        try {
                            recognition.start();
                            isRecognizing = true;
                        } catch (error) {
                            spokenText.textContent = 'Erreur de démarrage. Réessaie.';
                            isRecognizing = false;
                            indicator.style.display = 'none';
                        }
                    });
                    
                    recognition.onresult = function(event) {
                        isRecognizing = false;
                        indicator.style.display = 'none';
                        const transcript = event.results[0][0].transcript;
                        spokenText.textContent = transcript;
                        currentRecording = transcript;
                        controls.style.display = 'flex';
                    };
                    
                    recognition.onerror = function(event) {
                        isRecognizing = false;
                        indicator.style.display = 'none';
                        if (event.error === 'no-speech') {
                            spokenText.textContent = 'Pas de parole détectée. Réessaie.';
                        } else if (event.error === 'audio-capture') {
                            spokenText.textContent = 'Microphone non détecté. Vérifie tes paramètres.';
                        } else if (event.error === 'not-allowed') {
                            spokenText.textContent = 'Permission microphone refusée. Autorise-le dans les paramètres du navigateur.';
                        } else {
                            spokenText.textContent = 'Erreur: ' + event.error;
                        }
                    };
                    
                    recognition.onend = function() {
                        isRecognizing = false;
                        indicator.style.display = 'none';
                    };
                    
                } catch (error) {
                    startSpeakingBtn.disabled = true;
                    spokenText.textContent = 'La reconnaissance vocale ne fonctionne pas dans ce navigateur. Essaie Chrome ou Edge.';
                }
            } else {
                startSpeakingBtn.disabled = true;
                spokenText.textContent = 'La reconnaissance vocale n\'est pas supportée par ton navigateur. Utilise Chrome ou Edge.';
            }
        }

        // Practice prompt selection
        document.getElementById('save-recording').addEventListener('click', () => {
            if (!currentRecording) {
                alert('Parle d\'abord pour enregistrer quelque chose');
                return;
            }

            const question = document.getElementById('parler-question').value.trim();

            const recording = {
                id: Date.now(),
                question: question || 'Sans question',
                transcript: currentRecording,
                note: document.getElementById('recording-note').value.trim() || '',
                created: new Date().toISOString()
            };

            recordings.push(recording);
            localStorage.setItem('recordings', JSON.stringify(recordings));
            
            // Clear UI
            document.getElementById('spoken-text').textContent = '';
            document.getElementById('recording-note').value = '';
            document.getElementById('parler-question').value = '';
            document.getElementById('recording-controls').style.display = 'none';
            currentRecording = null;

            renderRecordings();
            alert('Sauvegardé ✓');
        });

        function renderRecordings() {
            const list = document.getElementById('recordings-list');
            const statsDiv = document.getElementById('practice-stats');
            
            if (recordings.length === 0) {
                statsDiv.style.display = 'none';
                list.innerHTML = `
                    <div class="empty">
                        <div class="empty-icon">
                            <svg class="svg-icon-lg" viewBox="0 0 24 24" fill="currentColor" style="opacity: 0.3;">
                                <path d="M12 14c1.66 0 3-1.34 3-3V5c0-1.66-1.34-3-3-3S9 3.34 9 5v6c0 1.66 1.34 3 3 3zm5.91-3c-.49 0-.9.36-.98.85C16.52 14.2 14.47 16 12 16s-4.52-1.8-4.93-4.15c-.08-.49-.49-.85-.98-.85-.61 0-1.09.54-1 1.14.49 3 2.89 5.35 5.91 5.78V20c0 .55.45 1 1 1s1-.45 1-1v-2.08c3.02-.43 5.42-2.78 5.91-5.78.1-.6-.39-1.14-1-1.14z"/>
                            </svg>
                        </div>
                        <div class="empty-text">Rien ici encore...</div>
                    </div>
                `;
                return;
            }

            // Show stats
            statsDiv.style.display = 'grid';
            
            // Calculate stats
            const totalRecordings = recordings.length;
            const oneWeekAgo = new Date();
            oneWeekAgo.setDate(oneWeekAgo.getDate() - 7);
            const thisWeekRecordings = recordings.filter(r => new Date(r.created) >= oneWeekAgo).length;
            const totalWords = recordings.reduce((sum, r) => sum + (r.transcript ? r.transcript.split(/\s+/).length : 0), 0);
            
            document.getElementById('total-recordings').textContent = totalRecordings;
            document.getElementById('this-week-recordings').textContent = thisWeekRecordings;
            document.getElementById('total-words-spoken').textContent = totalWords;

            // Sort by most recent first
            const sortedRecordings = [...recordings].sort((a, b) => b.id - a.id);

            list.innerHTML = sortedRecordings.map(rec => {
                const wordCount = rec.transcript ? rec.transcript.split(/\s+/).length : 0;
                const date = new Date(rec.created);
                const dateStr = date.toLocaleDateString('fr-FR', { 
                    weekday: 'long', 
                    year: 'numeric', 
                    month: 'long', 
                    day: 'numeric' 
                });
                const timeStr = date.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' });
                
                return `
                    <div class="recording-card">
                        <div class="recording-header">
                            <div>
                                <div class="recording-date">${dateStr} à ${timeStr}</div>
                                <div style="font-size: 0.75rem; color: var(--gold); margin-top: 0.25rem;">${wordCount} mots prononcés</div>
                            </div>
                            <button class="icon-btn" onclick="deleteRecording(${rec.id})">
                                <svg class="svg-icon" viewBox="0 0 24 24">
                                    <path d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM19 4h-3.5l-1-1h-5l-1 1H5v2h14V4z"/>
                                </svg>
                            </button>
                        </div>
                        ${rec.question ? `<div style="font-weight: 500; color: var(--crimson); margin-bottom: 0.75rem; font-size: 1rem;">Q: ${rec.question}</div>` : ''}
                        <div class="recording-transcript">${rec.transcript}</div>
                        ${rec.note ? `<div class="recording-note">${rec.note}</div>` : ''}
                    </div>
                `;
            }).join('');
        }

        function deleteRecording(id) {
            if (confirm('Supprimer cet enregistrement ?')) {
                recordings = recordings.filter(r => r.id !== id);
                localStorage.setItem('recordings', JSON.stringify(recordings));
                renderRecordings();
            }
        }

        // ============================================
        // WRITING - FIXED
        // ============================================
        const writingArea = document.getElementById('writing-area');
        const wordCountEl = document.getElementById('word-count');

        writingArea.addEventListener('input', () => {
            const text = writingArea.value.trim();
            const words = text ? text.split(/\s+/).length : 0;
            wordCountEl.textContent = `${words} mot${words !== 1 ? 's' : ''}`;
        });

        document.getElementById('save-writing').addEventListener('click', () => {
            const text = writingArea.value.trim();
            if (!text) {
                alert('Écris quelque chose d\'abord');
                return;
            }

            const writing = {
                id: Date.now(),
                text: text,
                created: new Date().toISOString()
            };

            writings.push(writing);
            localStorage.setItem('writings', JSON.stringify(writings));

            writingArea.value = '';
            wordCountEl.textContent = '0 mots';
            
            renderWritingsArchive();
            alert('Sauvegardé ✓');
        });

        function renderWritingsArchive() {
            const archive = document.getElementById('writings-archive');
            
            if (writings.length === 0) {
                archive.innerHTML = `
                    <div class="empty">
                        <div class="empty-icon">
                            <svg class="svg-icon-lg" viewBox="0 0 24 24" fill="currentColor" style="opacity: 0.3;">
                                <path d="M3 17.25V21h3.75L17.81 9.94l-3.75-3.75L3 17.25zM20.71 7.04c.39-.39.39-1.02 0-1.41l-2.34-2.34c-.39-.39-1.02-.39-1.41 0l-1.83 1.83 3.75 3.75 1.83-1.83z"/>
                            </svg>
                        </div>
                        <div class="empty-text">Rien ici encore...</div>
                    </div>
                `;
                return;
            }

            // Sort by most recent first
            const sortedWritings = [...writings].sort((a, b) => b.id - a.id);

            archive.innerHTML = sortedWritings.map(writing => `
                <div class="writing-card">
                    <div class="writing-header">
                        <div class="writing-date">${new Date(writing.created).toLocaleDateString('fr-FR', {
                            year: 'numeric',
                            month: 'long',
                            day: 'numeric'
                        })}</div>
                        <button class="icon-btn" onclick="deleteWriting(${writing.id})">
                            <svg class="svg-icon" viewBox="0 0 24 24">
                                <path d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM19 4h-3.5l-1-1h-5l-1 1H5v2h14V4z"/>
                            </svg>
                        </button>
                    </div>
                    <div class="writing-text">${writing.text.replace(/\n/g, '<br>')}</div>
                </div>
            `).join('');
        }

        function deleteWriting(id) {
            if (confirm('Supprimer cette écriture ?')) {
                writings = writings.filter(w => w.id !== id);
                localStorage.setItem('writings', JSON.stringify(writings));
                renderWritingsArchive();
            }
        }

        // ============================================
        // TABS
        // ============================================
        document.querySelectorAll('.tab').forEach(tab => {
            tab.addEventListener('click', () => {
                const parent = tab.closest('section');
                const targetId = tab.dataset.tab;
                
                parent.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
                parent.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
                
                tab.classList.add('active');
                parent.querySelector(`#${targetId}`).classList.add('active');
            });
        });

        // ============================================
        // PDF EXPORT FOR WORDS
        // ============================================
        function saveWordsAsPDF() {
            const { jsPDF } = window.jspdf;
            if (!jsPDF) {
                alert('Erreur : bibliothèque PDF non chargée');
                return;
            }
            
            const doc = new jsPDF();
            
            // Title
            doc.setFontSize(22);
            doc.setTextColor(139, 38, 53); // crimson
            doc.text('Mon Vocabulaire Français', 20, 20);
            
            doc.setFontSize(10);
            doc.setTextColor(107, 97, 92); // text-soft
            const filterText = Object.values(activeFilters).filter(Boolean).length > 0 
                ? `Filtres actifs: ${Object.entries(activeFilters).filter(([k,v]) => v).map(([k,v]) => `${k}:${v}`).join(', ')}` 
                : '';
            doc.text(`Généré le ${new Date().toLocaleDateString('fr-FR')} ${filterText}`, 20, 28);
            
            let y = 40;
            const pageHeight = doc.internal.pageSize.height;
            const margin = 20;
            
            // Sort by most recent first
            const filteredVocabulary = getFilteredVocabulary();
            const sortedVocabulary = [...filteredVocabulary].sort((a, b) => b.id - a.id);
            
            sortedVocabulary.forEach((word, index) => {
                // Check if we need a new page
                if (y > pageHeight - 40) {
                    doc.addPage();
                    y = 20;
                }
                
                // Word number and French word
                doc.setFontSize(14);
                doc.setTextColor(27, 43, 58); // navy
                doc.text(`${index + 1}. ${word.french}`, margin, y);
                y += 7;
                
                // Article if present
                if (word.article) {
                    doc.setFontSize(10);
                    doc.setTextColor(201, 168, 97); // gold
                    doc.text(`Article: ${word.article}`, margin + 5, y);
                    y += 5;
                }
                
                // Meaning
                if (word.meaning) {
                    doc.setFontSize(10);
                    doc.setTextColor(42, 37, 32); // text
                    doc.text(`Signification: ${word.meaning}`, margin + 5, y);
                    y += 5;
                }
                
                // Categories
                const categories = [];
                if (word.theme) categories.push(word.theme);
                if (word.week) categories.push(`Semaine ${word.week}`);
                if (word.quarter) categories.push(word.quarter);
                if (word.year) categories.push(word.year);
                
                if (categories.length > 0) {
                    doc.setFontSize(9);
                    doc.setTextColor(107, 97, 92);
                    doc.text(categories.join(' • '), margin + 5, y);
                    y += 5;
                }
                
                // Contexts
                if (word.contexts && word.contexts.length > 0) {
                    doc.setFontSize(9);
                    doc.setTextColor(107, 97, 92);
                    
                    if (word.contexts[0]) {
                        const contextText = doc.splitTextToSize(`Neutre: ${word.contexts[0]}`, 170);
                        doc.text(contextText, margin + 5, y);
                        y += contextText.length * 4;
                    }
                    
                    if (word.contexts[1]) {
                        const contextText = doc.splitTextToSize(`Émotionnel: ${word.contexts[1]}`, 170);
                        doc.text(contextText, margin + 5, y);
                        y += contextText.length * 4;
                    }
                    
                    if (word.contexts[2]) {
                        const contextText = doc.splitTextToSize(`Idiomatique: ${word.contexts[2]}`, 170);
                        doc.text(contextText, margin + 5, y);
                        y += contextText.length * 4;
                    }
                }
                
                // Note
                if (word.note) {
                    doc.setFontSize(9);
                    doc.setTextColor(107, 97, 92);
                    const noteText = doc.splitTextToSize(`Note: ${word.note}`, 170);
                    doc.text(noteText, margin + 5, y);
                    y += noteText.length * 4;
                }
                
                y += 8; // Space between words
            });
            
            // Save the PDF
            doc.save(`vocabulaire-francais-${new Date().toISOString().split('T')[0]}.pdf`);
        }

        // PDF button visibility and click handler
        function updatePDFButtonVisibility() {
            const pdfBtn = document.getElementById('save-words-pdf');
            if (pdfBtn) {
                pdfBtn.style.display = getFilteredVocabulary().length > 0 ? 'flex' : 'none';
            }
        }

        document.getElementById('save-words-pdf').addEventListener('click', saveWordsAsPDF);

        // ============================================
        // NAVIGATION
        // ============================================
        document.querySelectorAll('.nav-link').forEach(link => {
            link.addEventListener('click', () => {
                const room = link.dataset.room;
                
                document.querySelectorAll('.room').forEach(r => r.classList.remove('active'));
                document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
                
                document.getElementById(room).classList.add('active');
                link.classList.add('active');
            });
        });

        // ============================================
        // NOTES SECTION
        // ============================================
        let activeNoteFilter = 'all';

        function renderNotes() {
            const grid = document.getElementById('notes-grid');
            
            const filteredNotes = activeNoteFilter === 'all' 
                ? notes 
                : notes.filter(n => n.category === activeNoteFilter);
            
            if (filteredNotes.length === 0) {
                grid.innerHTML = `
                    <div class="empty">
                        <div class="empty-icon">
                            <svg class="svg-icon-lg" viewBox="0 0 24 24" fill="currentColor" style="opacity: 0.3;">
                                <path d="M14 2H6c-1.1 0-1.99.9-1.99 2L4 20c0 1.1.89 2 1.99 2H18c1.1 0 2-.9 2-2V8l-6-6zm2 16H8v-2h8v2zm0-4H8v-2h8v2zm-3-5V3.5L18.5 9H13z"/>
                            </svg>
                        </div>
                        <div class="empty-text">Rien ici encore...</div>
                    </div>
                `;
                return;
            }

            // Sort by most recent first
            const sortedNotes = [...filteredNotes].sort((a, b) => b.id - a.id);

            grid.innerHTML = sortedNotes.map(note => {
                const categoryColors = {
                    grammaire: 'var(--crimson)',
                    prononciation: 'var(--gold)',
                    phrases: 'var(--navy)',
                    vocabulaire: 'var(--rosy)',
                    culture: 'var(--sage)',
                    autre: 'var(--text-soft)'
                };
                
                const categoryColor = categoryColors[note.category] || 'var(--text-soft)';
                
                return `
                    <div class="note-card">
                        <div class="note-header">
                            <span class="note-category" style="background: ${categoryColor}20; color: ${categoryColor}; border-left: 3px solid ${categoryColor};">
                                ${note.category}
                            </span>
                            <button class="icon-btn" onclick="deleteNote(${note.id})">
                                <svg class="svg-icon" viewBox="0 0 24 24">
                                    <path d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM19 4h-3.5l-1-1h-5l-1 1H5v2h14V4z"/>
                                </svg>
                            </button>
                        </div>
                        <h3 class="note-title">${note.title}</h3>
                        <div class="note-content">${note.content.replace(/\n/g, '<br>')}</div>
                        ${note.link ? `
                            <a href="${note.link}" target="_blank" class="note-link">
                                <svg class="svg-icon" viewBox="0 0 24 24" style="width: 14px; height: 14px;">
                                    <path d="M3.9 12c0-1.71 1.39-3.1 3.1-3.1h4V7H7c-2.76 0-5 2.24-5 5s2.24 5 5 5h4v-1.9H7c-1.71 0-3.1-1.39-3.1-3.1zM8 13h8v-2H8v2zm9-6h-4v1.9h4c1.71 0 3.1 1.39 3.1 3.1s-1.39 3.1-3.1 3.1h-4V17h4c2.76 0 5-2.24 5-5s-2.24-5-5-5z"/>
                                </svg>
                                Voir la ressource
                            </a>
                        ` : ''}
                        <div class="note-date">${new Date(note.created).toLocaleDateString('fr-FR', { 
                            year: 'numeric', 
                            month: 'long', 
                            day: 'numeric' 
                        })}</div>
                    </div>
                `;
            }).join('');
        }

        function deleteNote(id) {
            if (confirm('Supprimer cette note ?')) {
                notes = notes.filter(n => n.id !== id);
                localStorage.setItem('notes', JSON.stringify(notes));
                renderNotes();
            }
        }

        // Note filter listeners
        document.querySelectorAll('[data-note-filter]').forEach(btn => {
            btn.addEventListener('click', () => {
                activeNoteFilter = btn.dataset.noteFilter;
                
                document.querySelectorAll('[data-note-filter]').forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                
                renderNotes();
            });
        });

        // Note form submission
        document.getElementById('note-form').addEventListener('submit', (e) => {
            e.preventDefault();
            
            const note = {
                id: Date.now(),
                category: document.getElementById('note-category').value,
                title: document.getElementById('note-title').value.trim(),
                content: document.getElementById('note-content').value.trim(),
                link: document.getElementById('note-link').value.trim(),
                created: new Date().toISOString()
            };

            notes.push(note);
            localStorage.setItem('notes', JSON.stringify(notes));
            
            renderNotes();
            closeModal('note-modal');
            
            // Reset form
            document.getElementById('note-form').reset();
        });

        // ============================================
        // INITIALIZE - FIXED
        // ============================================
        document.addEventListener('DOMContentLoaded', () => {
            renderEntrance();
            renderGarden();
            populateJardinFilters(); // NEW
            setupFilterListeners(); // NEW
            renderReadingList();
            renderListeningList();
            renderRecordings();
            renderWritingsArchive();
            renderResourcesList();
            renderNotes();
            
            // Fix: Properly attach event listener for add word button
            const addWordBtn = document.getElementById('add-word-btn');
            if (addWordBtn) {
                addWordBtn.addEventListener('click', function() {
                    openModal('word-modal');
                });
            }

            // Fix: Initialize image upload handlers
            setupImageUpload('word-image-upload', 'word-image-input', 'word-image-preview');
            setupImageUpload('edit-word-image-upload', 'edit-word-image-input', 'edit-word-image-preview');
            
            // Initialize speech recognition
            initializeSpeechRecognition();
        });
    </script>
</body>
</html>
