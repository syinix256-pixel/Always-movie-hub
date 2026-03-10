# Always-movie-hub
Always movie hub
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Always Movie Hub - Stream & Download</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            user-select: none;
            -webkit-user-select: none;
        }

        :root {
            --primary: #e50914;
            --primary-dark: #b2070f;
            --bg-primary: #ffffff;
            --bg-secondary: #f5f5f5;
            --text-primary: #333333;
            --text-secondary: #666666;
            --border: #e0e0e0;
            --success: #28a745;
            --danger: #dc3545;
            --warning: #ffc107;
            --safe-top: env(safe-area-inset-top, 0px);
            --safe-bottom: env(safe-area-inset-bottom, 0px);
        }

        .dark-mode {
            --bg-primary: #1a1a1a;
            --bg-secondary: #2d2d2d;
            --text-primary: #ffffff;
            --text-secondary: #b0b0b0;
            --border: #404040;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background-color: var(--bg-primary);
            color: var(--text-primary);
            overscroll-behavior-y: none;
            min-height: 100vh;
            transition: background-color 0.3s;
        }

        .app {
            max-width: 1200px;
            margin: 0 auto;
            padding: var(--safe-top) 0 var(--safe-bottom) 0;
        }

        /* Desktop Navigation */
        .desktop-nav {
            position: fixed;
            top: var(--safe-top);
            left: 0;
            right: 0;
            background-color: var(--bg-secondary);
            border-bottom: 1px solid var(--border);
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 1000;
        }

        .nav-brand {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--primary);
        }

        .nav-links {
            display: flex;
            gap: 30px;
        }

        .nav-link {
            color: var(--text-secondary);
            text-decoration: none;
            font-weight: 500;
            cursor: pointer;
            padding: 5px 10px;
        }

        .nav-link.active {
            color: var(--primary);
            border-bottom: 2px solid var(--primary);
        }

        /* Bottom Navigation (Mobile) */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background-color: var(--bg-secondary);
            border-top: 1px solid var(--border);
            display: flex;
            justify-content: space-around;
            padding: 10px 0 calc(10px + var(--safe-bottom)) 0;
            z-index: 1000;
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
            color: var(--text-secondary);
            font-size: 0.75rem;
            cursor: pointer;
            padding: 5px 15px;
        }

        .nav-item.active {
            color: var(--primary);
        }

        .nav-icon {
            font-size: 1.5rem;
        }

        /* Main Content */
        .main-content {
            padding: 20px;
            margin-top: 70px;
            margin-bottom: 70px;
            min-height: calc(100vh - 140px);
        }

        /* Pages */
        .page {
            display: none;
        }

        .page.active {
            display: block;
        }

        /* Home Page */
        .featured {
            position: relative;
            height: 400px;
            border-radius: 15px;
            overflow: hidden;
            margin-bottom: 30px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }

        .featured-content {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            padding: 40px;
            background: linear-gradient(transparent, rgba(0,0,0,0.8));
            color: white;
        }

        .featured-title {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }

        .featured-buttons {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }

        .btn-primary {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 5px;
            font-size: 1rem;
            cursor: pointer;
            font-weight: bold;
        }

        .btn-secondary {
            background-color: rgba(255,255,255,0.3);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 5px;
            font-size: 1rem;
            cursor: pointer;
            font-weight: bold;
        }

        .section-title {
            font-size: 1.5rem;
            margin: 30px 0 20px;
        }

        .movie-row {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 15px;
        }

        .movie-card {
            background-color: var(--bg-secondary);
            border-radius: 10px;
            overflow: hidden;
            cursor: pointer;
        }

        .movie-thumbnail {
            width: 100%;
            aspect-ratio: 2/3;
            background: linear-gradient(45deg, var(--primary), var(--primary-dark));
            position: relative;
        }

        .movie-info {
            padding: 10px;
        }

        .movie-title {
            font-weight: 500;
            margin-bottom: 5px;
        }

        .movie-meta {
            font-size: 0.85rem;
            color: var(--text-secondary);
        }

        /* Subscription Page */
        .subscription-container {
            max-width: 800px;
            margin: 0 auto;
        }

        .plans-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .plan-card {
            background-color: var(--bg-secondary);
            border-radius: 15px;
            padding: 30px;
            text-align: center;
            border: 2px solid transparent;
            cursor: pointer;
            transition: all 0.3s;
        }

        .plan-card.selected {
            border-color: var(--primary);
            transform: scale(1.05);
        }

        .price {
            font-size: 2rem;
            font-weight: bold;
            color: var(--primary);
            margin: 20px 0;
        }

        .price small {
            font-size: 1rem;
            color: var(--text-secondary);
        }

        .plan-features {
            list-style: none;
            margin: 20px 0;
        }

        .plan-features li {
            margin: 10px 0;
            color: var(--text-secondary);
        }

        .payment-section {
            background-color: var(--bg-secondary);
            border-radius: 15px;
            padding: 30px;
            margin-top: 30px;
        }

        .provider-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin: 20px 0;
        }

        .provider-btn {
            padding: 15px;
            border: 2px solid var(--border);
            border-radius: 10px;
            background: none;
            color: var(--text-primary);
            cursor: pointer;
            font-size: 1rem;
        }

        .provider-btn.active {
            border-color: var(--primary);
            background-color: var(--primary);
            color: white;
        }

        .input-group {
            margin: 20px 0;
        }

        .input-group label {
            display: block;
            margin-bottom: 8px;
            color: var(--text-secondary);
        }

        .input-group input {
            width: 100%;
            padding: 15px;
            border: 1px solid var(--border);
            border-radius: 10px;
            background-color: var(--bg-primary);
            color: var(--text-primary);
            font-size: 1rem;
        }

        .subscribe-btn {
            width: 100%;
            padding: 15px;
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
        }

        /* Downloads Page */
        .downloads-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
        }

        .clear-all-btn {
            padding: 10px 20px;
            background-color: var(--danger);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .downloads-grid {
            display: grid;
            gap: 15px;
        }

        .download-item {
            display: flex;
            background-color: var(--bg-secondary);
            border-radius: 10px;
            overflow: hidden;
        }

        .download-thumb {
            width: 100px;
            height: 150px;
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
        }

        .download-details {
            flex: 1;
            padding: 15px;
        }

        .download-progress {
            height: 4px;
            background-color: var(--border);
            border-radius: 2px;
            margin: 10px 0;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background-color: var(--primary);
            width: 0%;
        }

        .download-actions {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }

        .play-btn {
            padding: 8px 20px;
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        /* Settings Page */
        .settings-section {
            background-color: var(--bg-secondary);
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
        }

        .settings-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
            border-bottom: 1px solid var(--border);
        }

        .settings-item:last-child {
            border-bottom: none;
        }

        .switch {
            position: relative;
            display: inline-block;
            width: 50px;
            height: 24px;
        }

        .switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: var(--border);
            transition: .3s;
            border-radius: 24px;
        }

        .slider:before {
            position: absolute;
            content: "";
            height: 20px;
            width: 20px;
            left: 2px;
            bottom: 2px;
            background-color: white;
            transition: .3s;
            border-radius: 50%;
        }

        input:checked + .slider {
            background-color: var(--primary);
        }

        input:checked + .slider:before {
            transform: translateX(26px);
        }

        .danger-btn {
            width: 100%;
            padding: 15px;
            background-color: var(--danger);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1rem;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0,0,0,0.5);
            align-items: center;
            justify-content: center;
            z-index: 2000;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background-color: var(--bg-secondary);
            padding: 30px;
            border-radius: 15px;
            max-width: 400px;
            width: 90%;
        }

        .modal-title {
            font-size: 1.5rem;
            margin-bottom: 20px;
        }

        .modal-text {
            color: var(--text-secondary);
            margin-bottom: 20px;
        }

        .modal-input {
            width: 100%;
            padding: 15px;
            border: 1px solid var(--border);
            border-radius: 5px;
            margin-bottom: 20px;
            background-color: var(--bg-primary);
            color: var(--text-primary);
        }

        .modal-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }

        .modal-cancel {
            padding: 12px;
            background-color: var(--border);
            color: var(--text-primary);
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .modal-confirm {
            padding: 12px;
            background-color: var(--danger);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .toast {
            position: fixed;
            bottom: 100px;
            left: 50%;
            transform: translateX(-50%);
            background-color: var(--bg-secondary);
            color: var(--text-primary);
            padding: 15px 30px;
            border-radius: 50px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            display: none;
            z-index: 1500;
        }

        .toast.show {
            display: block;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .desktop-nav {
                display: none;
            }
            
            .main-content {
                margin-top: 0;
                margin-bottom: 70px;
                padding-bottom: 20px;
            }
            
            .featured-title {
                font-size: 1.5rem;
            }
            
            .plans-container {
                grid-template-columns: 1fr;
            }
            
            .plan-card.selected {
                transform: scale(1.02);
            }
        }

        @media (min-width: 769px) {
            .bottom-nav {
                display: none;
            }
        }
    </style>
</head>
<body>
    <div class="app" id="app">
        <!-- Desktop Navigation -->
        <nav class="desktop-nav">
            <div class="nav-brand">🎬 Always Movie Hub</div>
            <div class="nav-links">
                <a class="nav-link active" onclick="showPage('home')">Home</a>
                <a class="nav-link" onclick="showPage('browse')">Browse</a>
                <a class="nav-link" onclick="showPage('watchlist')">Watchlist</a>
                <a class="nav-link" onclick="showPage('downloads')">Downloads</a>
                <a class="nav-link" onclick="showPage('settings')">Settings</a>
            </div>
        </nav>

        <!-- Bottom Navigation (Mobile) -->
        <nav class="bottom-nav">
            <div class="nav-item active" onclick="showPage('home')">
                <span class="nav-icon">🏠</span>
                <span>Home</span>
            </div>
            <div class="nav-item" onclick="showPage('browse')">
                <span class="nav-icon">🔍</span>
                <span>Browse</span>
            </div>
            <div class="nav-item" onclick="showPage('watchlist')">
                <span class="nav-icon">⭐</span>
                <span>Watchlist</span>
            </div>
            <div class="nav-item" onclick="showPage('downloads')">
                <span class="nav-icon">📥</span>
                <span>Downloads</span>
            </div>
            <div class="nav-item" onclick="showPage('settings')">
                <span class="nav-icon">⚙️</span>
                <span>Settings</span>
            </div>
        </nav>

        <!-- Main Content -->
        <main class="main-content">
            <!-- Home Page -->
            <div id="home" class="page active">
                <div class="featured">
                    <div class="featured-content">
                        <h1 class="featured-title">Featured Movie</h1>
                        <p>Watch the latest blockbuster movies and TV shows</p>
                        <div class="featured-buttons">
                            <button class="btn-primary" onclick="showToast('Playing featured movie')">▶ Play</button>
                            <button class="btn-secondary">ℹ More Info</button>
                        </div>
                    </div>
                </div>

                <h2 class="section-title">Trending Now</h2>
                <div class="movie-row">
                    <div class="movie-card" onclick="showToast('Movie details')">
                        <div class="movie-thumbnail"></div>
                        <div class="movie-info">
                            <div class="movie-title">Action Movie 1</div>
                            <div class="movie-meta">2024 • 2h 15m</div>
                        </div>
                    </div>
                    <div class="movie-card" onclick="showToast('Movie details')">
                        <div class="movie-thumbnail"></div>
                        <div class="movie-info">
                            <div class="movie-title">Comedy Movie 1</div>
                            <div class="movie-meta">2024 • 1h 45m</div>
                        </div>
                    </div>
                    <div class="movie-card" onclick="showToast('Movie details')">
                        <div class="movie-thumbnail"></div>
                        <div class="movie-info">
                            <div class="movie-title">Drama Series</div>
                            <div class="movie-meta">2023 • 45m ep</div>
                        </div>
                    </div>
                </div>

                <h2 class="section-title">Continue Watching</h2>
                <div class="movie-row">
                    <div class="movie-card" onclick="showToast('Continue watching')">
                        <div class="movie-thumbnail"></div>
                        <div class="movie-info">
                            <div class="movie-title">Movie 2</div>
                            <div class="movie-meta">45% completed</div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Browse Page -->
            <div id="browse" class="page">
                <h1>Browse Movies</h1>
                <div style="margin: 20px 0">
                    <input type="text" placeholder="Search movies..." style="width: 100%; padding: 15px; border-radius: 10px; border: 1px solid var(--border); background-color: var(--bg-primary); color: var(--text-primary);">
                </div>
                
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 15px; margin: 20px 0;">
                    <select style="padding: 10px; border-radius: 5px; background-color: var(--bg-primary); color: var(--text-primary); border: 1px solid var(--border);">
                        <option>All Categories</option>
                        <option>Action</option>
                        <option>Comedy</option>
                        <option>Drama</option>
                    </select>
                    
                    <select style="padding: 10px; border-radius: 5px; background-color: var(--bg-primary); color: var(--text-primary); border: 1px solid var(--border);">
                        <option>All Years</option>
                        <option>2024</option>
                        <option>2023</option>
                        <option>2022</option>
                    </select>
                </div>

                <div class="movie-row">
                    <div class="movie-card" onclick="showToast('Movie details')">
                        <div class="movie-thumbnail"></div>
                        <div class="movie-info">
                            <div class="movie-title">The Last Warrior</div>
                            <div class="movie-meta">2024 • Action</div>
                        </div>
                    </div>
                    <div class="movie-card" onclick="showToast('Movie details')">
                        <div class="movie-thumbnail"></div>
                        <div class="movie-info">
                            <div class="movie-title">Comedy Night</div>
                            <div class="movie-meta">2023 • Comedy</div>
                        </div>
                    </div>
                    <div class="movie-card" onclick="showToast('Movie details')">
                        <div class="movie-thumbnail"></div>
                        <div class="movie-info">
                            <div class="movie-title">Drama King</div>
                            <div class="movie-meta">2024 • Drama</div>
                        </div>
                    </div>
                    <div class="movie-card" onclick="showToast('Movie details')">
                        <div class="movie-thumbnail"></div>
                        <div class="movie-info">
                            <div class="movie-title">Action Heroes</div>
                            <div class="movie-meta">2023 • Action</div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Watchlist Page -->
            <div id="watchlist" class="page">
                <h1>My Watchlist</h1>
                
                <div style="margin: 20px 0; text-align: center; padding: 50px; background-color: var(--bg-secondary); border-radius: 10px;">
                    <span style="font-size: 4rem;">📺</span>
                    <h2 style="margin: 20px 0;">Your watchlist is empty</h2>
                    <p style="color: var(--text-secondary); margin-bottom: 20px;">Add movies to keep track of what you want to watch</p>
                    <button class="btn-primary" onclick="showPage('browse')">Browse Movies</button>
                </div>
            </div>

            <!-- Downloads Page -->
            <div id="downloads" class="page">
                <div class="downloads-header">
                    <h1>My Downloads</h1>
                    <button class="clear-all-btn" onclick="showToast('All downloads cleared')">Clear All</button>
                </div>

                <div class="downloads-grid">
                    <div class="download-item">
                        <div class="download-thumb"></div>
                        <div class="download-details">
                            <h3>Action Movie 1</h3>
                            <div class="download-progress">
                                <div class="progress-fill" style="width: 100%"></div>
                            </div>
                            <div style="display: flex; justify-content: space-between; margin: 5px 0; color: var(--text-secondary);">
                                <span>1.2 GB</span>
                                <span>Completed</span>
                            </div>
                            <div class="download-actions">
                                <button class="play-btn" onclick="showToast('Playing movie')">▶ Play</button>
                                <button class="clear-all-btn" style="padding: 8px 15px;" onclick="showToast('Removed from downloads')">Remove</button>
                            </div>
                        </div>
                    </div>

                    <div class="download-item">
                        <div class="download-thumb"></div>
                        <div class="download-details">
                            <h3>Comedy Series - Episode 5</h3>
                            <div class="download-progress">
                                <div class="progress-fill" style="width: 100%"></div>
                            </div>
                            <div style="display: flex; justify-content: space-between; margin: 5px 0; color: var(--text-secondary);">
                                <span>850 MB</span>
                                <span>Completed</span>
                            </div>
                            <div class="download-actions">
                                <button class="play-btn" onclick="showToast('Playing episode')">▶ Play</button>
                                <button class="clear-all-btn" style="padding: 8px 15px;" onclick="showToast('Removed from downloads')">Remove</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Subscription Page -->
            <div id="subscription" class="page">
                <div class="subscription-container">
                    <h1>Choose Your Plan</h1>
                    
                    <div class="plans-container">
                        <div class="plan-card" onclick="selectPlan('weekly')" id="weekly-plan">
                            <h3>Weekly Plan</h3>
                            <div class="price">UGX 8,000<small>/week</small></div>
                            <ul class="plan-features">
                                <li>✓ Unlimited streaming</li>
                                <li>✓ Download enabled</li>
                                <li>✓ HD Quality</li>
                                <li>✓ Cancel anytime</li>
                            </ul>
                        </div>

                        <div class="plan-card selected" onclick="selectPlan('monthly')" id="monthly-plan">
                            <h3>Monthly Plan</h3>
                            <div class="price">UGX 25,000<small>/month</small></div>
                            <ul class="plan-features">
                                <li>✓ All weekly features</li>
                                <li>✓ Save 20%</li>
                                <li>✓ Priority support</li>
                                <li>✓ 4K Ultra HD</li>
                            </ul>
                            <span style="position: absolute; top: -10px; right: 20px; background-color: var(--primary); color: white; padding: 5px 15px; border-radius: 20px; font-size: 0.85rem;">Best Value</span>
                        </div>
                    </div>

                    <div class="payment-section">
                        <h2>Payment Details</h2>
                        
                        <div class="provider-buttons">
                            <button class="provider-btn active" onclick="selectProvider('MTN')" id="mtn-btn">MTN Mobile Money<br><small>0775648886</small></button>
                            <button class="provider-btn" onclick="selectProvider('AIRTEL')" id="airtel-btn">Airtel Money<br><small>0707538010</small></button>
                        </div>

                        <div class="input-group">
                            <label>Mobile Money Number</label>
                            <input type="tel" id="phone-number" placeholder="e.g., 0775648886" value="0775648886">
                        </div>

                        <button class="subscribe-btn" onclick="processPayment()" id="subscribe-btn">
                            Pay UGX 25,000
                        </button>

                        <p style="text-align: center; margin-top: 20px; color: var(--text-secondary); font-size: 0.9rem;">
                            You will receive a prompt on your phone to complete payment
                        </p>
                    </div>
                </div>
            </div>

            <!-- Settings Page -->
            <div id="settings" class="page">
                <h1>Settings</h1>

                <div class="settings-section">
                    <h2>Account</h2>
                    <div class="settings-item">
                        <span>Email</span>
                        <span>user@example.com</span>
                    </div>
                    <div class="settings-item">
                        <span>Phone</span>
                        <span>+256 775 648 886</span>
                    </div>
                </div>

                <div class="settings-section">
                    <h2>Preferences</h2>
                    <div class="settings-item">
                        <span>Notifications</span>
                        <label class="switch">
                            <input type="checkbox" checked id="notifications">
                            <span class="slider"></span>
                        </label>
                    </div>
                    <div class="settings-item">
                        <span>Dark Mode</span>
                        <label class="switch">
                            <input type="checkbox" id="dark-mode" onchange="toggleDarkMode()">
                            <span class="slider"></span>
                        </label>
                    </div>
                    <div class="settings-item">
                        <span>Download Quality</span>
                        <select style="padding: 5px; border-radius: 5px; background-color: var(--bg-primary); color: var(--text-primary); border: 1px solid var(--border);">
                            <option>Auto</option>
                            <option>High (1080p)</option>
                            <option>Medium (720p)</option>
                            <option>Low (480p)</option>
                        </select>
                    </div>
                </div>

                <div class="settings-section">
                    <h2>Subscription</h2>
                    <div class="settings-item">
                        <span>Current Plan</span>
                        <span class="plan-badge" style="background-color: var(--primary); color: white; padding: 5px 15px; border-radius: 20px;">Monthly</span>
                    </div>
                    <div class="settings-item">
                        <span>Expires</span>
                        <span>April 10, 2024</span>
                    </div>
                    <button class="danger-btn" style="background-color: var(--warning);" onclick="showPage('subscription')">
                        Change Plan
                    </button>
                </div>

                <div class="settings-section">
                    <h2>Danger Zone</h2>
                    <button class="danger-btn" onclick="showDeleteModal()">
                        Delete Account
                    </button>
                </div>
            </div>
        </main>

        <!-- Delete Account Modal -->
        <div class="modal" id="delete-modal">
            <div class="modal-content">
                <h2 class="modal-title">Delete Account</h2>
                <p class="modal-text">This action is permanent and cannot be undone. All your data will be permanently deleted.</p>
                <input type="text" class="modal-input" placeholder="Type DELETE to confirm" id="delete-confirm">
                <div class="modal-buttons">
                    <button class="modal-cancel" onclick="hideDeleteModal()">Cancel</button>
                    <button class="modal-confirm" onclick="deleteAccount()">Delete Account</button>
                </div>
            </div>
        </div>

        <!-- Toast Notification -->
        <div class="toast" id="toast">Notification</div>
    </div>

    <script>
        // State
        let currentPlan = 'monthly';
        let currentProvider = 'MTN';
        let subscription = null;

        // Navigation
        function showPage(pageId) {
            // Hide all pages
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            
            // Show selected page
            document.getElementById(pageId).classList.add('active');
            
            // Update nav links
            document.querySelectorAll('.nav-link, .nav-item').forEach(link => {
                link.classList.remove('active');
            });
            
            // Find and activate corresponding nav links
            document.querySelectorAll(`[onclick="showPage('${pageId}')"]`).forEach(link => {
                link.classList.add('active');
            });
            
            // If subscription page, check if already subscribed
            if (pageId === 'subscription' && subscription) {
                showToast('You already have an active subscription');
            }
        }

        // Toast notification
        function showToast(message) {
            const toast = document.getElementById('toast');
            toast.textContent = message;
            toast.classList.add('show');
            
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }

        // Dark mode toggle
        function toggleDarkMode() {
            const isDark = document.getElementById('dark-mode').checked;
            if (isDark) {
                document.documentElement.classList.add('dark-mode');
            } else {
                document.documentElement.classList.remove('dark-mode');
            }
        }

        // Check system dark mode
        const darkModeMediaQuery = window.matchMedia('(prefers-color-scheme: dark)');
        if (darkModeMediaQuery.matches) {
            document.getElementById('dark-mode').checked = true;
            document.documentElement.classList.add('dark-mode');
        }

        // Subscription
        function selectPlan(plan) {
            currentPlan = plan;
            
            // Update UI
            document.getElementById('weekly-plan').classList.remove('selected');
            document.getElementById('monthly-plan').classList.remove('selected');
            document.getElementById(plan + '-plan').classList.add('selected');
            
            // Update button text
            const price = plan === 'weekly' ? '8,000' : '25,000';
            document.getElementById('subscribe-btn').textContent = `Pay UGX ${price}`;
        }

        function selectProvider(provider) {
            currentProvider = provider;
            
            // Update UI
            document.getElementById('mtn-btn').classList.remove('active');
            document.getElementById('airtel-btn').classList.remove('active');
            document.getElementById(provider.toLowerCase() + '-btn').classList.add('active');
        }

        function processPayment() {
            const phoneNumber = document.getElementById('phone-number').value;
            
            if (!phoneNumber || phoneNumber.length < 10) {
                showToast('Please enter a valid phone number');
                return;
            }
            
            // Validate that it's either MTN or Airtel number
            const isValidMTN = phoneNumber.startsWith('077') || phoneNumber.startsWith('078');
            const isValidAirtel = phoneNumber.startsWith('070') || phoneNumber.startsWith('075');
            
            if (!isValidMTN && !isValidAirtel) {
                showToast('Please enter a valid MTN or Airtel number');
                return;
            }
            
            // Simulate payment processing
            const price = currentPlan === 'weekly' ? '8,000' : '25,000';
            document.getElementById('subscribe-btn').disabled = true;
            document.getElementById('subscribe-btn').textContent = 'Processing...';
            
            setTimeout(() => {
                subscription = {
                    plan: currentPlan,
                    phoneNumber: phoneNumber,
                    provider: currentProvider,
                    startDate: new Date().toISOString(),
                    expiryDate: new Date(Date.now() + (currentPlan === 'weekly' ? 7 : 30) * 24 * 60 * 60 * 1000).toISOString()
                };
                
                document.getElementById('subscribe-btn').disabled = false;
                document.getElementById('subscribe-btn').textContent = `Pay UGX ${price}`;
                
                showToast(`Payment initiated! Check ${phoneNumber} to complete`);
                
                // Navigate to home after successful payment
                setTimeout(() => {
                    showPage('home');
                }, 2000);
            }, 2000);
        }

        // Delete account modal
        function showDeleteModal() {
            document.getElementById('delete-modal').classList.add('active');
        }

        function hideDeleteModal() {
            document.getElementById('delete-modal').classList.remove('active');
            document.getElementById('delete-confirm').value = '';
        }

        function deleteAccount() {
            const confirmText = document.getElementById('delete-confirm').value;
            
            if (confirmText !== 'DELETE') {
                showToast('Please type DELETE to confirm');
                return;
            }
            
            showToast('Account deleted successfully');
            hideDeleteModal();
            
            // Reset app state
            subscription = null;
            currentPlan = 'monthly';
            
            // Navigate to home
            showPage('home');
        }

        // Initialize
        window.onload = function() {
            // Check if user is subscribed (simulated)
            // In a real app, this would check localStorage or API
        };

        // Handle orientation change
        window.addEventListener('resize', function() {
            // Adjust UI if needed
        });

        // Prevent pull-to-refresh on mobile
        document.body.addEventListener('touchmove', function(e) {
            if (e.target === document.body) {
                e.preventDefault();
            }
        }, { passive: false });
    </script>
</body>
</html>
