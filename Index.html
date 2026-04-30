// ========================================
// Global Variables & State Management
// ========================================

let currentUser = null;
let allTools = [];
let allCategories = [];
let toolsUsageData = {};
let recentTools = [];
let favoriteTools = [];
let currentTheme = 'dark';
let channelsData = [];
let weeklySchedule = [];

// ========================================
// Initialize App
// ========================================

document.addEventListener('DOMContentLoaded', () => {
    loadFromLocalStorage();
    checkLoginStatus();
    initializeEventListeners();
    updateLastOpenTime();
});

// ========================================
// Local Storage Management
// ========================================

function loadFromLocalStorage() {
    currentUser = JSON.parse(localStorage.getItem('rng_user')) || null;
    toolsUsageData = JSON.parse(localStorage.getItem('rng_tools_usage')) || {};
    recentTools = JSON.parse(localStorage.getItem('rng_recent_tools')) || [];
    favoriteTools = JSON.parse(localStorage.getItem('rng_favorites')) || [];
    currentTheme = localStorage.getItem('rng_theme') || 'dark';
    
    // Load custom data
    const customTools = JSON.parse(localStorage.getItem('rng_custom_tools')) || [];
    const customCategories = JSON.parse(localStorage.getItem('rng_custom_categories')) || [];
    
    // Merge with config
    allTools = [...CONFIG.tools, ...customTools];
    allCategories = [...CONFIG.categories, ...customCategories];
    channelsData = JSON.parse(localStorage.getItem('rng_channels')) || CONFIG.channels;
    weeklySchedule = JSON.parse(localStorage.getItem('rng_schedule')) || CONFIG.weeklySchedule;
}

function saveToLocalStorage() {
    localStorage.setItem('rng_user', JSON.stringify(currentUser));
    localStorage.setItem('rng_tools_usage', JSON.stringify(toolsUsageData));
    localStorage.setItem('rng_recent_tools', JSON.stringify(recentTools));
    localStorage.setItem('rng_favorites', JSON.stringify(favoriteTools));
    localStorage.setItem('rng_theme', currentTheme);
    localStorage.setItem('rng_channels', JSON.stringify(channelsData));
    localStorage.setItem('rng_schedule', JSON.stringify(weeklySchedule));
}

function updateLastOpenTime() {
    const now = new Date();
    localStorage.setItem('rng_last_open', now.toISOString());
    displayLastOpenTime();
}

function displayLastOpenTime() {
    const lastOpen = localStorage.getItem('rng_last_open');
    if (lastOpen) {
        const lastDate = new Date(lastOpen);
        const now = new Date();
        const diff = Math.floor((now - lastDate) / 60000); // minutes
        
        let timeText = 'এইমাত্র';
        if (diff > 60) {
            const hours = Math.floor(diff / 60);
            timeText = `${hours} ঘন্টা আগে`;
        } else if (diff > 1) {
            timeText = `${diff} মিনিট আগে`;
        }
        
        document.getElementById('lastOpen').textContent = `শেষ ব্যবহার: ${timeText}`;
    }
}

// ========================================
// Login System
// ========================================

function checkLoginStatus() {
    const loginScreen = document.getElementById('loginScreen');
    const mainApp = document.getElementById('mainApp');
    
    if (currentUser) {
        loginScreen.classList.add('hidden');
        mainApp.classList.remove('hidden');
        displayUserInfo();
        initializeApp();
    } else {
        loginScreen.classList.remove('hidden');
        mainApp.classList.add('hidden');
    }
}

function initializeEventListeners() {
    // Login button
    document.getElementById('googleLoginBtn')?.addEventListener('click', handleGoogleLogin);
    
    // Logout button
    document.getElementById('logoutBtn')?.addEventListener('click', handleLogout);
    
    // Sidebar toggle
    document.getElementById('sidebarToggle')?.addEventListener('click', toggleSidebar);
    document.getElementById('closeSidebar')?.addEventListener('click', toggleSidebar);
    
    // Theme toggle
    document.getElementById('themeToggle')?.addEventListener('click', toggleTheme);
    
    // Search
    document.getElementById('searchInput')?.addEventListener('input', handleSearch);
    
    // Quick access tabs
    document.querySelectorAll('.tab-btn').forEach(btn => {
        btn.addEventListener('click', (e) => switchTab(e.target.dataset.tab));
    });
    
    // Modal close
    document.querySelectorAll('.modal-close').forEach(btn => {
        btn.addEventListener('click', closeModal);
    });
    
    // Manage buttons
    document.querySelectorAll('.manage-btn').forEach(btn => {
        btn.addEventListener('click', (e) => {
            const action = e.currentTarget.dataset.action;
            handleManageAction(action);
        });
    });
    
    // Click outside sidebar to close
    document.addEventListener('click', (e) => {
        const sidebar = document.getElementById('sidebar');
        const toggle = document.getElementById('sidebarToggle');
        if (!sidebar.contains(e.target) && !toggle.contains(e.target)) {
            sidebar.classList.remove('active');
        }
    });
}

function handleGoogleLogin() {
    // Simulated Google Login
    const simulatedUser = {
        name: 'RNG Creator',
        email: 'rngcreator@gmail.com',
        photo: 'https://ui-avatars.com/api/?name=RNG+Creator&background=2ecc71&color=fff&size=100'
    };
    
    currentUser = simulatedUser;
    saveToLocalStorage();
    checkLoginStatus();
    showNotification('সফলভাবে লগইন হয়েছে!', 'success');
}

function handleLogout() {
    if (confirm('আপনি কি লগআউট করতে চান?')) {
        currentUser = null;
        saveToLocalStorage();
        checkLoginStatus();
        showNotification('লগআউট সম্পন্ন হয়েছে', 'info');
    }
}

function displayUserInfo() {
    if (currentUser) {
        document.getElementById('userName').textContent = currentUser.name;
        document.getElementById('userPhoto').src = currentUser.photo;
    }
}

// ========================================
// Initialize App Components
// ========================================

function initializeApp() {
    renderSidebarCategories();
    renderYouTubeChannels();
    renderWeeklySchedule();
    renderQuickAccess('recent');
    renderAllTools();
    applyTheme();
}

function renderSidebarCategories() {
    const nav = document.getElementById('categoryNav');
    nav.innerHTML = '';
    
    allCategories.forEach(category => {
        const navItem = document.createElement('a');
        navItem.className = 'nav-item';
        navItem.href = `#${category.id}`;
        navItem.innerHTML = `
            <i class="${category.icon}"></i>
            <span>${category.name}</span>
        `;
        navItem.addEventListener('click', (e) => {
            e.preventDefault();
            scrollToCategory(category.id);
            toggleSidebar();
        });
        nav.appendChild(navItem);
    });
}

function scrollToCategory(categoryId) {
    const element = document.getElementById(categoryId);
    if (element) {
        element.scrollIntoView({ behavior: 'smooth', block: 'start' });
    }
}

// ========================================
// YouTube Channels with API Integration
// ========================================

async function renderYouTubeChannels() {
    const container = document.getElementById('channelsContainer');
    container.innerHTML = '<div class="spinner"></div>';
    
    try {
        const channelsWithData = await Promise.all(
            channelsData.map(async (channel) => {
                const stats = await fetchYouTubeStats(channel.channelId);
                return { ...channel, ...stats };
            })
        );
        
        container.innerHTML = '';
        channelsWithData.forEach(channel => {
            const card = createChannelCard(channel);
            container.appendChild(card);
        });
    } catch (error) {
        console.error('Error fetching channel data:', error);
        container.innerHTML = `
            <div class="empty-state">
                <i class="fas fa-exclamation-triangle"></i>
                <p>চ্যানেল ডেটা লোড করতে সমস্যা হয়েছে</p>
            </div>
        `;
    }
}

async function fetchYouTubeStats(channelId) {
    try {
        const response = await fetch(
            `https://www.googleapis.com/youtube/v3/channels?part=statistics,snippet&id=${channelId}&key=${CONFIG.youtubeApiKey}`
        );
        
        if (!response.ok) throw new Error('API Error');
        
        const data = await response.json();
        if (data.items && data.items.length > 0) {
            const stats = data.items[0].statistics;
            const snippet = data.items[0].snippet;
            return {
                subscribers: formatNumber(stats.subscriberCount),
                views: formatNumber(stats.viewCount),
                videos: formatNumber(stats.videoCount),
                thumbnail: snippet.thumbnails.high.url
            };
        }
    } catch (error) {
        console.error('YouTube API Error:', error);
        return {
            subscribers: 'N/A',
            views: 'N/A',
            videos: 'N/A',
            thumbnail: 'https://via.placeholder.com/60'
        };
    }
}

function createChannelCard(channel) {
    const card = document.createElement('div');
    card.className = 'channel-card glass-effect';
    card.innerHTML = `
        <div class="channel-header">
            <img src="${channel.thumbnail}" alt="${channel.name}" class="channel-logo">
            <div class="channel-info">
                <h3>${channel.name}</h3>
                <span class="verified"><i class="fas fa-check-circle"></i> Verified</span>
            </div>
        </div>
        <div class="channel-stats">
            <div class="stat-item">
                <span class="stat-label">সাবস্ক্রাইবার</span>
                <span class="stat-value">${channel.subscribers}</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">মোট ভিউ</span>
                <span class="stat-value">${channel.views}</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">ভিডিও সংখ্যা</span>
                <span class="stat-value">${channel.videos}</span>
            </div>
        </div>
    `;
    
    card.addEventListener('click', () => openChannelModal(channel));
    return card;
}

function openChannelModal(channel) {
    const modal = document.getElementById('modalContainer');
    const modalBody = document.getElementById('modalBody');
    
    modalBody.innerHTML = `
        <h2><i class="fab fa-youtube"></i> ${channel.name}</h2>
        <div class="channel-modal-content">
            <img src="${channel.thumbnail}" style="width: 150px; border-radius: 50%; margin: 20px auto; display: block;">
            <div class="stat-item">
                <span class="stat-label">চ্যানেল URL</span>
                <span class="stat-value">${channel.url}</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">সাবস্ক্রাইবার</span>
                <span class="stat-value">${channel.subscribers}</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">মোট ভিউ</span>
                <span class="stat-value">${channel.views}</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">ভিডিও</span>
                <span class="stat-value">${channel.videos}</span>
            </div>
            <a href="${channel.url}" target="_blank" class="submit-btn" style="margin-top: 20px; display: block; text-align: center; text-decoration: none;">
                <i class="fas fa-external-link-alt"></i> চ্যানেলে যান
            </a>
        </div>
    `;
    
    modal.classList.add('active');
}

// ========================================
// Weekly Schedule
// ========================================

function renderWeeklySchedule() {
    const container = document.getElementById('scheduleContainer');
    const today = new Date().getDay(); // 0 = Sunday, 6 = Saturday
    const tomorrow = (today + 1) % 7;
    
    container.innerHTML = '';
    weeklySchedule.forEach((day, index) => {
        const card = document.createElement('div');
        card.className = 'schedule-card glass-effect';
        
        // Highlight today and tomorrow
        if (index === today) card.classList.add('today');
        if (index === tomorrow) card.classList.add('tomorrow');
        
        const scheduleHTML = day.schedule.map(item => `
            <div class="schedule-details">
                <div class="schedule-channel">${item.channel}</div>
                <span class="schedule-type ${item.type === 'বন্ধ' ? 'off' : ''}">${item.type}</span>
            </div>
        `).join('');
        
        card.innerHTML = `
            <div class="day-name">${day.day}</div>
            ${scheduleHTML}
        `;
        
        container.appendChild(card);
    });
}

// ========================================
// Quick Access (Recent, Most Used, Favorites)
// ========================================

function renderQuickAccess(tab) {
    const container = document.getElementById('quickAccessContent');
    let tools = [];
    
    switch(tab) {
        case 'recent':
            tools = recentTools.slice(0, 6).map(id => allTools.find(t => t.id === id)).filter(Boolean);
            break;
        case 'mostUsed':
            tools = Object.entries(toolsUsageData)
                .sort(([,a], [,b]) => b - a)
                .slice(0, 6)
                .map(([id]) => allTools.find(t => t.id === id))
                .filter(Boolean);
            break;
        case 'favorites':
            tools = favoriteTools.map(id => allTools.find(t => t.id === id)).filter(Boolean);
            break;
    }
    
    if (tools.length === 0) {
        container.innerHTML = `
            <div class="empty-state">
                <i class="fas fa-inbox"></i>
                <p>কোনো টুল নেই</p>
            </div>
        `;
        return;
    }
    
    container.innerHTML = '';
    tools.forEach(tool => {
        const card = createToolCard(tool);
        container.appendChild(card);
    });
}

function switchTab(tab) {
    document.querySelectorAll('.tab-btn').forEach(btn => {
        btn.classList.toggle('active', btn.dataset.tab === tab);
    });
    renderQuickAccess(tab);
}

// ========================================
// Render All Tools by Category
// ========================================

function renderAllTools() {
    const container = document.getElementById('toolsContainer');
    container.innerHTML = '';
    
    allCategories.forEach(category => {
        const categoryTools = allTools.filter(tool => tool.category === category.id);
        
        if (categoryTools.length === 0) return;
        
        const section = document.createElement('section');
        section.className = 'tools-category';
        section.id = category.id;
        
        section.innerHTML = `
            <h2 class="category-title">
                <i class="${category.icon}"></i> ${category.name}
            </h2>
            <div class="tools-grid" id="grid-${category.id}"></div>
        `;
        
        container.appendChild(section);
        
        const grid = document.getElementById(`grid-${category.id}`);
        categoryTools.forEach(tool => {
            const card = createToolCard(tool);
            grid.appendChild(card);
        });
    });
}

function createToolCard(tool) {
    const card = document.createElement('div');
    card.className = 'tool-card glass-effect';
    
    if (!currentUser) {
        card.classList.add('locked');
    }
    
    const isFavorite = favoriteTools.includes(tool.id);
    
    card.innerHTML = `
        <div class="tool-header">
            <div class="tool-icon">
                <i class="${tool.icon}"></i>
            </div>
            <button class="favorite-btn ${isFavorite ? 'active' : ''}" data-tool-id="${tool.id}">
                <i class="fas fa-star"></i>
            </button>
        </div>
        <div class="tool-name">${tool.name}</div>
        <div class="tool-description">${tool.description}</div>
        <span class="tool-type-badge ${tool.type}">${tool.type === 'builtin' ? 'Built-in' : 'External'}</span>
        ${!currentUser ? '<div class="lock-overlay"><i class="fas fa-lock"></i></div>' : ''}
    `;
    
    // Favorite button
    const favBtn = card.querySelector('.favorite-btn');
    favBtn.addEventListener('click', (e) => {
        e.stopPropagation();
        toggleFavorite(tool.id);
    });
    
    // Tool click
    card.addEventListener('click', () => {
        if (!currentUser) {
            showNotification('দয়া করে লগইন করুন', 'warning');
            return;
        }
        handleToolClick(tool);
    });
    
    return card;
}

function toggleFavorite(toolId) {
    const index = favoriteTools.indexOf(toolId);
    if (index > -1) {
        favoriteTools.splice(index, 1);
    } else {
        favoriteTools.push(toolId);
    }
    saveToLocalStorage();
    renderAllTools();
    renderQuickAccess('favorites');
}

// ========================================
// Handle Tool Click
// ========================================

function handleToolClick(tool) {
    // Update usage stats
    toolsUsageData[tool.id] = (toolsUsageData[tool.id] || 0) + 1;
    
    // Update recent tools
    recentTools = recentTools.filter(id => id !== tool.id);
    recentTools.unshift(tool.id);
    recentTools = recentTools.slice(0, 10);
    
    saveToLocalStorage();
    
    if (tool.type === 'builtin') {
        openBuiltinTool(tool);
    } else if (tool.type === 'external') {
        window.open(tool.url, '_blank');
        showNotification(`${tool.name} খোলা হচ্ছে...`, 'info');
    }
}

// ========================================
// Built-in Tools
// ========================================

function openBuiltinTool(tool) {
    const modal = document.getElementById('toolModal');
    const modalBody = document.getElementById('toolModalBody');
    
    modalBody.innerHTML = getToolInterface(tool);
    modal.classList.add('active');
    
    // Initialize tool-specific functionality
    initializeToolFunctionality(tool.id);
}

function getToolInterface(tool) {
    const interfaces = {
        'profit-loss-calc': `
            <div class="tool-interface">
                <h2><i class="fas fa-calculator"></i> লাভ/ক্ষতি ক্যালকুলেটর</h2>
                <div class="calculator-display">
                    <div class="form-group">
                        <label>ক্রয়মূল্য (টাকা)</label>
                        <input type="number" id="costPrice" placeholder="উদাহরণ: 100">
                    </div>
                    <div class="form-group">
                        <label>বিক্রয়মূল্য (টাকা)</label>
                        <input type="number" id="sellingPrice" placeholder="উদাহরণ: 150">
                    </div>
                    <button class="submit-btn" onclick="calculateProfitLoss()">হিসাব করুন</button>
                    <div id="profitLossResult" class="result-box hidden">
                        <div class="result-label">ফলাফল</div>
                        <div class="result-value" id="plAmount"></div>
                        <div class="result-label" style="margin-top: 10px;">শতাংশ</div>
                        <div class="result-value" id="plPercentage"></div>
                    </div>
                </div>
            </div>
        `,
        'percentage-calc': `
            <div class="tool-interface">
                <h2><i class="fas fa-percent"></i> শতাংশ ক্যালকুলেটর</h2>
                <div class="calculator-display">
                    <div class="input-row">
                        <div class="form-group">
                            <label>সংখ্যা</label>
                            <input type="number" id="percentNumber" placeholder="১০০">
                        </div>
                        <div class="form-group">
                            <label>শতাংশ (%)</label>
                            <input type="number" id="percentValue" placeholder="২০">
                        </div>
                    </div>
                    <button class="submit-btn" onclick="calculatePercentage()">হিসাব করুন</button>
                    <div id="percentResult" class="result-box hidden">
                        <div class="result-label">উত্তর</div>
                        <div class="result-value" id="percentAnswer"></div>
                    </div>
                </div>
            </div>
        `,
        'age-calc': `
            <div class="tool-interface">
                <h2><i class="fas fa-birthday-cake"></i> বয়স ক্যালকুলেটর</h2>
                <div class="calculator-display">
                    <div class="form-group">
                        <label>জন্ম তারিখ</label>
                        <input type="date" id="birthDate">
                    </div>
                    <button class="submit-btn" onclick="calculateAge()">বয়স বের করুন</button>
                    <div id="ageResult" class="result-box hidden">
                        <div class="result-label">আপনার বয়স</div>
                        <div class="result-value" id="ageYears"></div>
                        <div class="result-label" style="margin-top: 10px;">পরবর্তী জন্মদিন</div>
                        <div class="result-value" style="font-size: 16px;" id="nextBirthday"></div>
                    </div>
                </div>
            </div>
        `,
        'youtube-earnings': `
            <div class="tool-interface">
                <h2><i class="fab fa-youtube"></i> ইউটিউব আয় ক্যালকুলেটর</h2>
                <div class="calculator-display">
                    <div class="form-group">
                        <label>দৈনিক ভিউ</label>
                        <input type="number" id="dailyViews" placeholder="১০০০">
                    </div>
                    <div class="form-group">
                        <label>CPM (প্রতি ১০০০ ভিউ আয়)</label>
                        <input type="number" id="cpmRate" placeholder="২" value="2">
                    </div>
                    <button class="submit-btn" onclick="calculateYouTubeEarnings()">আয় হিসাব করুন</button>
                    <div id="earningsResult" class="result-box hidden">
                        <div class="result-label">দৈনিক আয়</div>
                        <div class="result-value" id="dailyEarnings"></div>
                        <div class="result-label" style="margin-top: 10px;">মাসিক আয়</div>
                        <div class="result-value" id="monthlyEarnings"></div>
                        <div class="result-label" style="margin-top: 10px;">বার্ষিক আয়</div>
                        <div class="result-value" id="yearlyEarnings"></div>
                    </div>
                </div>
            </div>
        `,
        'youtube-thumbnail': `
            <div class="tool-interface">
                <h2><i class="fab fa-youtube"></i> ইউটিউব থাম্বনেইল ডাউনলোডার</h2>
                <div class="calculator-display">
                    <div class="form-group">
                        <label>ইউটিউব ভিডিও লিংক</label>
                        <input type="text" id="videoUrl" placeholder="https://www.youtube.com/watch?v=...">
                    </div>
                    <button class="submit-btn" onclick="getThumbnails()">থাম্বনেইল পান</button>
                    <div id="thumbnailPreview"></div>
                </div>
            </div>
        `,
        'word-counter': `
            <div class="tool-interface">
                <h2><i class="fas fa-font"></i> ওয়ার্ড কাউন্টার</h2>
                <div class="calculator-display">
                    <div class="form-group">
                        <label>টেক্সট লিখুন</label>
                        <textarea id="textInput" placeholder="এখানে লিখুন..." style="min-height: 150px;"></textarea>
                    </div>
                    <div class="result-box">
                        <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px;">
                            <div>
                                <div class="result-label">শব্দ</div>
                                <div class="result-value" id="wordCount">০</div>
                            </div>
                            <div>
                                <div class="result-label">অক্ষর</div>
                                <div class="result-value" id="charCount">০</div>
                            </div>
                            <div>
                                <div class="result-label">বাক্য</div>
                                <div class="result-value" id="sentenceCount">০</div>
                            </div>
                            <div>
                                <div class="result-label">প্যারাগ্রাফ</div>
                                <div class="result-value" id="paraCount">০</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        `,
        'password-generator': `
            <div class="tool-interface">
                <h2><i class="fas fa-key"></i> পাসওয়ার্ড জেনারেটর</h2>
                <div class="calculator-display">
                    <div class="form-group">
                        <label>পাসওয়ার্ড দৈর্ঘ্য</label>
                        <input type="number" id="passwordLength" value="16" min="6" max="32">
                    </div>
                    <button class="submit-btn" onclick="generatePassword()">পাসওয়ার্ড তৈরি করুন</button>
                    <div id="passwordResult" class="result-box hidden">
                        <div class="result-label">আপনার পাসওয়ার্ড</div>
                        <div class="result-value" style="font-size: 18px; word-break: break-all;" id="generatedPassword"></div>
                        <button class="download-btn" onclick="copyPassword()">
                            <i class="fas fa-copy"></i> কপি করুন
                        </button>
                    </div>
                </div>
            </div>
        `,
        'qr-generator': `
            <div class="tool-interface">
                <h2><i class="fas fa-qrcode"></i> QR কোড জেনারেটর</h2>
                <div class="calculator-display">
                    <div class="form-group">
                        <label>টেক্সট বা লিংক</label>
                        <input type="text" id="qrText" placeholder="https://example.com">
                    </div>
                    <button class="submit-btn" onclick="generateQRCode()">QR তৈরি করুন</button>
                    <div id="qrPreview" class="qr-preview"></div>
                </div>
            </div>
        `,
        'unit-converter': `
            <div class="tool-interface">
                <h2><i class="fas fa-exchange-alt"></i> ইউনিট কনভার্টার</h2>
                <div class="calculator-display">
                    <div class="form-group">
                        <label>ধরন নির্বাচন করুন</label>
                        <select id="unitType" onchange="updateUnitOptions()">
                            <option value="length">দৈর্ঘ্য</option>
                            <option value="weight">ওজন</option>
                            <option value="volume">আয়তন</option>
                        </select>
                    </div>
                    <div class="input-row">
                        <div class="form-group">
                            <label>থেকে</label>
                            <select id="fromUnit"></select>
                        </div>
                        <div class="form-group">
                            <label>এ</label>
                            <select id="toUnit"></select>
                        </div>
                    </div>
                    <div class="form-group">
                        <label>মান</label>
                        <input type="number" id="unitValue" placeholder="১">
                    </div>
                    <button class="submit-btn" onclick="convertUnit()">রূপান্তর করুন</button>
                    <div id="unitResult" class="result-box hidden">
                        <div class="result-label">ফলাফল</div>
                        <div class="result-value" id="convertedValue"></div>
                    </div>
                </div>
            </div>
        `,
        'temperature-converter': `
            <div class="tool-interface">
                <h2><i class="fas fa-thermometer-half"></i> তাপমাত্রা কনভার্টার</h2>
                <div class="calculator-display">
                    <div class="form-group">
                        <label>তাপমাত্রা</label>
                        <input type="number" id="tempValue" placeholder="০">
                    </div>
                    <div class="form-group">
                        <label>থেকে</label>
                        <select id="fromTemp">
                            <option value="celsius">সেলসিয়াস (°C)</option>
                            <option value="fahrenheit">ফারেনহাইট (°F)</option>
                            <option value="kelvin">কেলভিন (K)</option>
                        </select>
                    </div>
                    <button class="submit-btn" onclick="convertTemperature()">রূপান্তর করুন</button>
                    <div id="tempResult" class="result-box">
                        <div style="display: grid; gap: 10px;">
                            <div>
                                <div class="result-label">সেলসিয়াস</div>
                                <div class="result-value" id="celsiusResult">-</div>
                            </div>
                            <div>
                                <div class="result-label">ফারেনহাইট</div>
                                <div class="result-value" id="fahrenheitResult">-</div>
                            </div>
                            <div>
                                <div class="result-label">কেলভিন</div>
                                <div class="result-value" id="kelvinResult">-</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        `
    };
    
    return interfaces[tool.id] || `<p>এই টুলটি শীঘ্রই আসছে...</p>`;
}

function initializeToolFunctionality(toolId) {
    switch(toolId) {
        case 'word-counter':
            document.getElementById('textInput').addEventListener('input', countWords);
            break;
        case 'unit-converter':
            updateUnitOptions();
            break;
    }
}

// ========================================
// Tool Functions
// ========================================

function calculateProfitLoss() {
    const cost = parseFloat(document.getElementById('costPrice').value);
    const selling = parseFloat(document.getElementById('sellingPrice').value);
    
    if (!cost || !selling) {
        showNotification('সব ফিল্ড পূরণ করুন', 'warning');
        return;
    }
    
    const difference = selling - cost;
    const percentage = ((difference / cost) * 100).toFixed(2);
    const type = difference >= 0 ? 'লাভ' : 'ক্ষতি';
    
    document.getElementById('plAmount').textContent = `${type}: ৳${Math.abs(difference).toFixed(2)}`;
    document.getElementById('plPercentage').textContent = `${Math.abs(percentage)}%`;
    document.getElementById('profitLossResult').classList.remove('hidden');
}

function calculatePercentage() {
    const number = parseFloat(document.getElementById('percentNumber').value);
    const percent = parseFloat(document.getElementById('percentValue').value);
    
    if (!number || !percent) {
        showNotification('সব ফিল্ড পূরণ করুন', 'warning');
        return;
    }
    
    const result = (number * percent) / 100;
    document.getElementById('percentAnswer').textContent = result.toFixed(2);
    document.getElementById('percentResult').classList.remove('hidden');
}

function calculateAge() {
    const birthDate = new Date(document.getElementById('birthDate').value);
    if (!birthDate.getTime()) {
        showNotification('সঠিক তারিখ দিন', 'warning');
        return;
    }
    
    const today = new Date();
    let age = today.getFullYear() - birthDate.getFullYear();
    const monthDiff = today.getMonth() - birthDate.getMonth();
    
    if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birthDate.getDate())) {
        age--;
    }
    
    // Next birthday
    let nextBirthday = new Date(today.getFullYear(), birthDate.getMonth(), birthDate.getDate());
    if (nextBirthday < today) {
        nextBirthday.setFullYear(today.getFullYear() + 1);
    }
    const daysUntil = Math.ceil((nextBirthday - today) / (1000 * 60 * 60 * 24));
    
    document.getElementById('ageYears').textContent = `${age} বছর`;
    document.getElementById('nextBirthday').textContent = `${daysUntil} দিন বাকি`;
    document.getElementById('ageResult').classList.remove('hidden');
}

function calculateYouTubeEarnings() {
    const views = parseFloat(document.getElementById('dailyViews').value);
    const cpm = parseFloat(document.getElementById('cpmRate').value);
    
    if (!views || !cpm) {
        showNotification('সব ফিল্ড পূরণ করুন', 'warning');
        return;
    }
    
    const daily = (views / 1000) * cpm;
    const monthly = daily * 30;
    const yearly = daily * 365;
    
    document.getElementById('dailyEarnings').textContent = `$${daily.toFixed(2)}`;
    document.getElementById('monthlyEarnings').textContent = `$${monthly.toFixed(2)}`;
    document.getElementById('yearlyEarnings').textContent = `$${yearly.toFixed(2)}`;
    document.getElementById('earningsResult').classList.remove('hidden');
}

function getThumbnails() {
    const url = document.getElementById('videoUrl').value;
    const videoId = extractYouTubeID(url);
    
    if (!videoId) {
        showNotification('সঠিক ইউটিউব লিংক দিন', 'warning');
        return;
    }
    
    const qualities = [
        { name: 'Max Quality', url: `https://img.youtube.com/vi/${videoId}/maxresdefault.jpg` },
        { name: 'High Quality', url: `https://img.youtube.com/vi/${videoId}/hqdefault.jpg` },
        { name: 'Medium Quality', url: `https://img.youtube.com/vi/${videoId}/mqdefault.jpg` },
        { name: 'Standard Quality', url: `https://img.youtube.com/vi/${videoId}/sddefault.jpg` }
    ];
    
    const preview = document.getElementById('thumbnailPreview');
    preview.innerHTML = '<div class="thumbnail-preview">';
    
    qualities.forEach(q => {
        preview.innerHTML += `
            <div class="thumbnail-item">
                <img src="${q.url}" alt="${q.name}">
                <a href="${q.url}" download="${videoId}-${q.name}.jpg" class="download-btn">
                    <i class="fas fa-download"></i> ${q.name}
                </a>
            </div>
        `;
    });
    
    preview.innerHTML += '</div>';
}

function extractYouTubeID(url) {
    const regex = /(?:youtube\.com\/(?:[^\/]+\/.+\/|(?:v|e(?:mbed)?)\/|.*[?&]v=)|youtu\.be\/)([^"&?\/\s]{11})/;
    const match = url.match(regex);
    return match ? match[1] :
