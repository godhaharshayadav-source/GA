<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Middle East Business Transformation Intelligence Platform</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Load Chart.js for Data Visualization -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js@3.7.1/dist/chart.min.js"></script>
    <!-- Load Lucide Icons for aesthetic enhancement -->
    <script src="https://unpkg.com/lucide@latest"></script>
    
    <!-- Tailwind Configuration for Custom Look -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        // Cream/Beige Luxury Palette
                        'bg-light': '#fcf8f3', // Very soft, off-white cream background
                        'card-base': 'rgba(255, 255, 255, 0.95)', // Near-white, opaque card base
                        'accent-primary': '#b8860b', // Dark Goldenrod / Rich Bronze (Primary Accent)
                        'accent-secondary': '#6b8e23', // Olive Drab (Growth/Success)
                        'accent-danger': '#8b0000', // Dark Red (Risk)
                        'text-dark': '#3c2f2f', // Rich dark brown/espresso for high contrast
                        'text-muted-light': '#8b7355', // Medium tan/sepia for muted text
                        'border-light': '#e0ddd5', // Light taupe/tan for subtle border
                        'highlight': '#fffacd', // Lemon Chiffon for highlighting active state
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        /* --- GLOBAL STYLES --- */
        body {
            background-color: theme('colors.bg-light');
            color: theme('colors.text-dark');
            font-family: theme('fontFamily.sans');
            min-height: 100vh;
            /* Gradient for a soft background */
            background-image: linear-gradient(to bottom right, #fcf8f3, #e8e3dc); 
        }

        /* --- CARD DESIGN (Clean, Embossed Light Look) --- */
        .card {
            background-color: theme('colors.card-base');
            border: 1px solid theme('colors.border-light');
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
            border-radius: 0.75rem;
            transition: all 0.3s ease-out;
            position: relative;
            overflow: hidden;
        }
        .card:hover {
            transform: translateY(-1px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.12);
            border-color: theme('colors.accent-primary');
        }
        
        .kpi-value {
            font-size: 2.75rem;
            font-weight: 800;
            line-height: 1.1;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.05); 
        }
        .kpi-label {
            font-size: 0.75rem;
            color: theme('colors.text-muted-light');
            font-weight: 600;
            letter-spacing: 0.05em;
            text-transform: uppercase;
            margin-top: 0.25rem;
        }
        .risk-indicator {
            padding: 0.4rem 1rem;
            border-radius: 9999px;
            font-weight: 700;
            font-size: 0.8rem;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }
        .risk-red { background-color: theme('colors.accent-danger'); color: white; animation: pulse-danger 2s infinite; }
        .risk-yellow { background-color: theme('colors.yellow.500'); color: theme('colors.text-dark'); }
        .risk-green { background-color: theme('colors.accent-secondary'); color: white; }
        
        @keyframes pulse-danger {
            0% { box-shadow: 0 0 0 0 rgba(139, 0, 0, 0.4); }
            70% { box-shadow: 0 0 0 10px rgba(139, 0, 0, 0); }
            100% { box-shadow: 0 0 0 0 rgba(139, 0, 0, 0); }
        }

        .section-title {
            font-weight: 800;
            letter-spacing: 0.05em;
            color: theme('colors.text-dark');
        }
        
        .industry-tile:hover {
            border-color: theme('colors.accent-primary');
            transform: scale(1.01);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
        }
        .progress-bar-container {
            background-color: theme('colors.border-light');
            height: 8px;
            border-radius: 4px;
            overflow: hidden;
            box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
        }
        .progress-bar {
            height: 100%;
            transition: width 0.5s ease-in-out;
        }

        /* Map Styling */
        #gcc-map path {
            fill: theme('colors.border-light');
            stroke: theme('colors.text-dark');
            stroke-width: 0.5;
            cursor: pointer;
            transition: fill 0.3s, transform 0.3s;
        }
        #gcc-map path:hover {
            fill: theme('colors.highlight');
            transform: scale(1.02);
        }
        .country-active {
            fill: theme('colors.highlight') !important;
            stroke: theme('colors.accent-primary') !important;
            stroke-width: 2 !important;
        }
    </style>
</head>
<body class="p-4 md:p-10">

    <!-- Header and Title -->
    <header class="mb-10 border-b border-border-light pb-4">
        <h1 class="text-3xl md:text-5xl font-extrabold text-accent-primary tracking-tighter">
            <i data-lucide="zap" class="inline-block h-8 w-8 mr-2 text-accent-secondary"></i>
            Middle East Business Transformation Intelligence Platform
        </h1>
        <p class="text-text-muted-light text-sm md:text-base mt-2">
            GCC Strategic Transformation Insights | Real-time Market, Risk, Sustainability & Technology Lenses
        </p>
    </header>

    <!-- 1. MEGA-TREND OVERVIEW PANEL -->
    <section id="mega-trend-overview" class="mb-12">
        <h2 class="text-xl section-title mb-6 border-l-4 border-accent-primary pl-3 flex items-center">
            <i data-lucide="globe" class="h-5 w-5 mr-2"></i> 1. ACTIVE INTELLIGENCE SNAPSHOT
        </h2>
        <div class="grid grid-cols-1 lg:grid-cols-5 gap-6">
            
            <!-- Dynamic KPI Cards (Col 1-3) -->
            <div id="kpi-display-cards" class="lg:col-span-3 grid grid-cols-2 md:grid-cols-3 gap-4">
                <!-- Dynamic KPI 1 -->
                <!-- ENSURE FLEX ALIGNMENT FOR VERTICAL STABILITY -->
                <div class="card p-4 rounded-xl flex flex-col justify-center h-full">
                    <div class="flex items-center space-x-2">
                        <i data-lucide="trending-up" id="kpi-icon-1" class="h-6 w-6 text-accent-secondary"></i>
                        <p class="kpi-value" id="kpi-value-1" style="color: var(--kpi-color-1, #6b8e23);">+5.8%</p>
                    </div>
                    <p class="kpi-label" id="kpi-label-1">Non-Oil GDP Growth (YoY)</p>
                </div>
    
                <!-- Dynamic KPI 2 -->
                <div class="card p-4 rounded-xl flex flex-col justify-center h-full">
                    <div class="flex items-center space-x-2">
                        <i data-lucide="banknote" id="kpi-icon-2" class="h-6 w-6 text-accent-primary"></i>
                        <p class="kpi-value" id="kpi-value-2" style="color: var(--kpi-color-2, #b8860b);">$43B</p>
                    </div>
                    <p class="kpi-label" id="kpi-label-2">FDI Inflows (LTM)</p>
                </div>
    
                <!-- Dynamic KPI 3 (Risk) -->
                <div class="card p-4 rounded-xl flex flex-col justify-between h-full">
                    <div class="flex items-center space-x-2">
                        <i data-lucide="alert-triangle" id="kpi-icon-3" class="h-6 w-6 text-accent-danger"></i>
                        <p class="kpi-value text-accent-danger" id="kpi-value-3">5.2/10</p>
                    </div>
                    <p class="kpi-label" id="kpi-label-3">Geopolitical Risk Index</p>
                    <div class="risk-indicator risk-red mt-3 text-center" id="risk-indicator-3">ELEVATED RISK</div>
                </div>
            </div>

            <!-- SVG Map (Col 4-5) -->
            <div class="card p-6 rounded-xl lg:col-span-2 min-h-[150px] flex flex-col items-center justify-center">
                <h3 class="text-lg font-semibold text-text-dark mb-3">Country Focus</h3>
                <div id="map-container" class="w-full max-w-sm">
                    <!-- Placeholder for the GCC Map -->
                    <svg id="gcc-map" viewBox="0 0 300 300" class="w-full h-auto">
                        <!-- Simplified KSA shape -->
                        <path id="ksa" d="M120 50 L180 50 L200 150 L150 250 L100 250 L80 150 Z" data-country="ksa" data-name="Saudi Arabia" />
                        <!-- Simplified UAE shape -->
                        <path id="uae" d="M200 150 L250 160 L240 200 L200 180 Z" data-country="uae" data-name="UAE" />
                        <!-- Simplified Qatar shape -->
                        <path id="qatar" d="M185 155 L195 160 L190 180 Z" data-country="qatar" data-name="Qatar" />
                        <!-- Simplified Oman shape -->
                        <path id="oman" d="M250 160 L280 180 L260 220 L240 200 Z" data-country="oman" data-name="Oman" />
                        <!-- Simplified Placeholder Label/Water -->
                        <text x="150" y="280" text-anchor="middle" class="text-xs fill-text-muted-light">Click a country for focus</text>
                    </svg>
                </div>
            </div>

        </div>
    </section>

    <!-- 2. INDUSTRY DEEP DIVE SECTION (Structure remains for responsiveness) -->
    <section id="industry-deep-dive" class="mb-12">
        <h2 class="text-xl section-title mb-6 border-l-4 border-accent-primary pl-3 flex items-center">
             <i data-lucide="layout-dashboard" class="h-5 w-5 mr-2"></i> 2. INDUSTRY DEEP DIVE (Select to Expand)
        </h2>
        <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-7 gap-4">
            <!-- Industry Tiles (using the luxury color palette) -->
            <div class="card industry-tile p-4 rounded-xl shadow-sm border-l-4 border-accent-secondary">
                <p class="text-lg font-semibold text-text-dark">Energy</p>
                <p class="text-text-muted-light text-xs mt-1">Growth: +4% | Renewables: 15%</p>
            </div>
            <div class="card industry-tile p-4 rounded-xl shadow-sm border-l-4 border-accent-secondary">
                <p class="text-lg font-semibold text-text-dark">Tourism</p>
                <p class="text-text-muted-light text-xs mt-1">Growth: +12% | Occupancy: 75%</p>
            </div>
            <div class="card industry-tile p-4 rounded-xl shadow-sm border-l-4 border-accent-secondary">
                <p class="text-lg font-semibold text-text-dark">E-commerce</p>
                <p class="text-text-muted-light text-xs mt-1">Penetration: 35% | Avg. basket: $150</p>
            </div>
            <div class="card industry-tile p-4 rounded-xl shadow-sm border-l-4 border-accent-secondary">
                <p class="text-lg font-semibold text-text-dark">Real Estate</p>
                <p class="text-text-muted-light text-xs mt-1">Value: +7% | Supply Risk: Med</p>
            </div>
            <div class="card industry-tile p-4 rounded-xl shadow-sm border-l-4 border-accent-secondary">
                <p class="text-lg font-semibold text-text-dark">Logistics</p>
                <p class="text-text-muted-light text-xs mt-1">Congestion: 20% | Freight cost: Stable</p>
            </div>
            <div class="card industry-tile p-4 rounded-xl shadow-sm border-l-4 border-accent-secondary">
                <p class="text-lg font-semibold text-text-dark">Fintech</p>
                <p class="text-text-muted-light text-xs mt-1">Adoption: 55% | Funding: $1.2B</p>
            </div>
            <div class="card industry-tile p-4 rounded-xl shadow-sm border-l-4 border-accent-secondary">
                <p class="text-lg font-semibold text-text-dark">Food Security</p>
                <p class="text-text-muted-light text-xs mt-1">Dependency: 85% | R&D Spend: High</p>
            </div>
        </div>
    </section>

    <!-- Dual Column Layout for Deep Dives (Sections 3-7) -->
    <!-- CRITICAL ALIGNMENT: items-stretch forces column heights to match -->
    <div class="grid grid-cols-1 xl:grid-cols-3 gap-8 items-stretch">

        <!-- Left Column (Risk, Sustainability, Tech) -->
        <div class="xl:col-span-2 space-y-8 flex flex-col">

            <!-- 3. GEOPOLITICAL RISK CONTROL TOWER -->
            <div class="card p-6 rounded-xl">
                <h3 class="text-lg section-title mb-4 flex items-center text-accent-danger">
                    <i data-lucide="shield-alert" class="h-5 w-5 mr-2"></i> 3. GEOPOLITICAL RISK CONTROL TOWER
                </h3>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div class="col-span-1 border-r border-border-light pr-4">
                        <p class="text-3xl font-bold text-accent-danger" id="risk-disruption">42%</p>
                        <p class="text-text-muted-light text-sm mt-1">Trade Route Disruption Index</p>
                    </div>
                    <div class="col-span-1 border-r border-border-light pr-4">
                        <p class="text-3xl font-bold text-yellow-500" id="risk-currency">3.5%</p>
                        <p class="text-text-muted-light text-sm mt-1">Currency Volatility Index</p>
                    </div>
                    <div class="col-span-1">
                        <p class="text-3xl font-bold text-accent-danger" id="risk-chokepoint">Hormuz Alert</p>
                        <p class="text-text-muted-light text-sm mt-1">Maritime Chokepoint Tension</p>
                    </div>
                </div>
                <!-- Placeholder for Geo-Heatmap / Risk Drivers -->
                <div class="mt-6 bg-border-light/50 p-4 rounded-xl text-center text-text-muted-light h-64 flex items-center justify-center border border-dashed border-text-muted-light/50">
                    [VISUALIZATION: Risk Trend Timeline & Drivers Waterfall Chart]
                </div>
            </div>

            <!-- 4. SUSTAINABILITY & NET ZERO DASHBOARD -->
            <div class="card p-6 rounded-xl">
                <h3 class="text-lg section-title mb-4 flex items-center text-accent-secondary">
                    <i data-lucide="leaf" class="h-5 w-5 mr-2"></i> 4. SUSTAINABILITY & NET ZERO DASHBOARD
                </h3>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6 items-center">
                    <div class="flex flex-col items-center">
                        <div class="w-32 h-32 md:w-40 md:h-40">
                            <canvas id="emissionGauge"></canvas>
                        </div>
                        <p class="text-center text-sm mt-2 text-text-muted-light">Emission Reduction Progress</p>
                    </div>
                    <div>
                        <p class="text-3xl font-bold text-accent-secondary" id="renewable-capacity">28 GW</p>
                        <p class="text-text-muted-light text-sm mt-1">Renewable Capacity Installed</p>
                        <div class="mt-4 bg-border-light/50 p-4 rounded-xl text-center text-text-muted-light h-36 flex items-center justify-center border border-dashed border-text-muted-light/50">
                            [VISUALIZATION: Water/Waste Metrics]
                        </div>
                    </div>
                    <div class="bg-border-light/50 p-4 rounded-xl text-center text-text-muted-light h-full flex items-center justify-center border border-dashed border-text-muted-light/50 min-h-[150px]">
                        [VISUALIZATION: ESG Compliance Treemap]
                    </div>
                </div>
            </div>

            <!-- 5. TECHNOLOGY MODERNIZATION & SMART ECONOMY PANEL -->
            <div class="card p-6 rounded-xl">
                <h3 class="text-lg section-title mb-4 flex items-center text-amber-600">
                    <i data-lucide="chip" class="h-5 w-5 mr-2"></i> 5. TECHNOLOGY MODERNIZATION & SMART ECONOMY
                </h3>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-center">
                    <div class="space-y-4">
                        <p class="text-3xl font-bold text-amber-600" id="ai-adoption-score">7.1/10</p>
                        <p class="text-text-muted-light text-sm mb-4">AI Adoption Index (GCC Average)</p>
                        <div class="progress-bar-container shadow-inner">
                            <div class="progress-bar" id="egov-progress" style="width: 85%; background: linear-gradient(90deg, #b8860b, #daa520);"></div>
                        </div>
                        <p class="text-sm text-text-muted-light">E-Government Readiness (85% progress)</p>
                        <div class="progress-bar-container shadow-inner">
                            <div class="progress-bar" id="cloud-progress" style="width: 72%; background: linear-gradient(90deg, #8b0000, #b22222);"></div>
                        </div>
                        <p class="text-sm text-text-muted-light">Cloud Usage Penetration (72% progress)</p>
                    </div>
                    <div class="min-h-[200px]">
                        <canvas id="techRadarChart"></canvas>
                    </div>
                </div>
            </div>
        </div>

        <!-- Right Column (Mega Projects, Supply Chain, Summary) -->
        <!-- MUST BE FLEX COLUMN TO ALLOW SECTION 8 TO GROW -->
        <div class="xl:col-span-1 space-y-8 flex flex-col">

            <!-- 6. MEGA PROJECTS & INFRASTRUCTURE TRACKER -->
            <div class="card p-6 rounded-xl">
                <h3 class="text-lg section-title mb-4 flex items-center text-gray-700">
                    <i data-lucide="hard-hat" class="h-5 w-5 mr-2"></i> 6. MEGA PROJECTS & INFRASTRUCTURE
                </h3>
                <!-- Project 1 -->
                <div class="mb-4 pb-3 border-b border-border-light">
                    <p class="font-semibold text-text-dark">NEOM (The Line)</p>
                    <p class="text-xs text-text-muted-light mb-1">Progress: <span id="neom-progress-label">25%</span> | Job Creation: 50K</p>
                    <div class="progress-bar-container">
                        <div class="progress-bar" id="neom-progress-bar" style="width: 25%; background: linear-gradient(90deg, #8b7355, #a0522d);"></div>
                    </div>
                </div>
                <!-- Project 2 -->
                <div class="mb-4 pb-3 border-b border-border-light">
                    <p class="font-semibold text-text-dark">Al Maktoum Int'l Expansion</p>
                    <p class="text-xs text-text-muted-light mb-1">Progress: <span id="alm-progress-label">68%</span> | Delay Risk: Low</p>
                    <div class="progress-bar-container">
                        <div class="progress-bar" id="alm-progress-bar" style="width: 68%; background: linear-gradient(90deg, #8b7355, #a0522d);"></div>
                    </div>
                </div>
                <!-- Project 3 -->
                <div class="mb-2">
                    <p class="font-semibold text-text-dark">Doha Metro Phase II</p>
                    <p class="text-xs text-text-muted-light mb-1">Progress: <span id="doha-progress-label">95%</span> | Budget: Under</p>
                    <div class="progress-bar-container">
                        <div class="progress-bar" id="doha-progress-bar" style="width: 95%; background: linear-gradient(90deg, #8b7355, #a0522d);"></div>
                    </div>
                </div>
            </div>

            <!-- 7. SUPPLY CHAIN & TRADE INTELLIGENCE PANEL -->
            <div class="card p-6 rounded-xl">
                <h3 class="text-lg section-title mb-4 flex items-center text-gray-700">
                    <i data-lucide="package" class="h-5 w-5 mr-2"></i> 7. SUPPLY CHAIN & TRADE INTELLIGENCE
                </h3>
                <div class="grid grid-cols-2 gap-4 mb-4">
                    <div>
                        <p class="text-3xl font-bold text-gray-700" id="lead-time">18 Days</p>
                        <p class="text-text-muted-light text-sm mt-1">Avg. Lead Time Volatility</p>
                    </div>
                    <div>
                        <p class="text-3xl font-bold text-accent-danger" id="import-dependency">92%</p>
                        <p class="text-text-muted-light text-sm mt-1">Food Import Dependency</p>
                    </div>
                </div>
                <!-- Placeholder for Sankey/Comparison Chart -->
                <div class="mt-4 bg-border-light/50 p-4 rounded-xl text-center text-text-muted-light h-32 flex items-center justify-center border border-dashed border-text-muted-light/50">
                    [VISUALIZATION: Import Sankey Diagram & Port Comparison]
                </div>
            </div>

            <!-- 8. CONSULTING SUMMARY PANEL (Final Output) - Dynamic Content & Scenario Selector -->
            <!-- CRITICAL: flex-grow ensures this panel fills all remaining vertical space to align with the left column -->
            <div id="consulting-summary-panel" class="card p-6 rounded-xl border-2 border-accent-secondary flex flex-col flex-grow">
                <h3 class="text-lg section-title mb-4 flex items-center text-accent-secondary">
                    <i data-lucide="eye" class="h-5 w-5 mr-2"></i> 8. CONSULTING SUMMARY PANEL
                </h3>
                
                <!-- Scenario Selector (Critical Feature) -->
                <div class="mb-4 flex items-center space-x-3 p-3 bg-border-light rounded-lg shadow-inner">
                    <span class="text-sm font-semibold text-text-dark">SCENARIO MODELING:</span>
                    <button id="scenario-a-btn" data-scenario="A" class="px-3 py-1 text-sm font-bold rounded-full bg-accent-secondary text-white hover:bg-opacity-80 transition-colors">
                        Accelerated Growth
                    </button>
                    <button id="scenario-b-btn" data-scenario="B" class="px-3 py-1 text-sm font-bold rounded-full bg-gray-500 text-white hover:bg-gray-600 transition-colors">
                        Geopolitical Friction
                    </button>
                </div>

                <div id="summary-content" class="w-full text-left flex-grow flex flex-col justify-center items-center p-4">
                    <!-- Loading State -->
                    <div id="loading-spinner" class="flex flex-col items-center justify-center text-text-muted-light">
                        <svg class="animate-spin h-8 w-8 text-accent-primary" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                            <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                            <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                        </svg>
                        <p class="mt-4 text-sm font-semibold text-accent-primary">Generating Real-time Strategic Insights using Gemini...</p>
                    </div>
                </div>
            </div>

        </div>

    </div>
    
    <!-- Icons initialization -->
    <script>
        lucide.createIcons();
    </script>
    
    <script>
        // --- Global State ---
        let activeScenario = 'A';
        let activeCountry = 'none';

        // --- Gemini API Configuration ---
        const MODEL_NAME = 'gemini-2.5-flash-preview-09-2025';
        const API_URL = `https://generativelanguage.googleapis.com/v1beta/models/${MODEL_NAME}:generateContent?key=`;
        const API_KEY = ""; 
        
        // --- Data Mocking for Scenarios and Countries ---
        const SCENARIO_DATA = {
            'A': { // Accelerated Growth (Optimistic)
                theme: { primary: '#b8860b', secondary: '#6b8e23', danger: '#8b0000' },
                gdp: { value: '+6.5%', color: '#6b8e23', icon: 'trending-up' },
                fdi: { value: '$55B', color: '#b8860b', icon: 'banknote' },
                risk: { value: '3.1/10', color: '#6b8e23', indicator: 'LOW RISK', class: 'risk-green' },
                risks: { disruption: '15%', currency: '1.2%', chokepoint: 'Stable' },
                mega: { neom: 40, alm: 75, doha: 98 },
                ai: 8.5, cloud: 85,
                gemini_prompt: "Based on a scenario of **Accelerated Diversification and Global Stability** in the GCC, summarize the key strategic outlook for foreign investors and major corporations.",
            },
            'B': { // Geopolitical Friction (Pessimistic)
                theme: { primary: '#b8860b', secondary: '#8b7355', danger: '#8b0000' },
                gdp: { value: '+3.2%', color: '#8b7355', icon: 'trending-down' },
                fdi: { value: '$25B', color: '#8b7355', icon: 'ban' },
                risk: { value: '7.8/10', color: '#8b0000', indicator: 'CRITICAL RISK', class: 'risk-red' },
                risks: { disruption: '75%', currency: '9.0%', chokepoint: 'High Tension' },
                mega: { neom: 15, alm: 55, doha: 90 },
                ai: 6.0, cloud: 55,
                gemini_prompt: "Based on a scenario of **Heightened Geopolitical Friction and Commodity Price Volatility** in the Middle East, summarize the critical risks and defensive strategic moves for foreign investors and major corporations.",
            }
        };

        const COUNTRY_FOCUS = {
            'ksa': {
                gdp: '+7.1%', fdi: '$28B', label: 'National GDP (KSA Focus)', icon: 'tower-stake'
            },
            'uae': {
                gdp: '+4.5%', fdi: '$15B', label: 'Non-Oil GDP (UAE Focus)', icon: 'ship'
            },
            'qatar': {
                gdp: '+2.5%', fdi: '$5B', label: 'LNG/Investment GDP (QAT Focus)', icon: 'gas-tank'
            },
            'oman': {
                gdp: '+5.1%', fdi: '$2B', label: 'Diversification Progress (OMAN Focus)', icon: 'compass'
            }
        };

        // --- Utility Functions ---

        async function exponentialBackoffFetch(url, options, maxRetries = 5) {
            for (let i = 0; i < maxRetries; i++) {
                try {
                    const response = await fetch(url, options);
                    if (response.status !== 429 && response.ok) {
                        return response;
                    } else if (response.status === 429) {
                        const delay = Math.pow(2, i) * 1000 + Math.random() * 1000;
                        await new Promise(resolve => setTimeout(resolve, delay));
                    } else {
                        throw new Error(`API Error: ${response.statusText}`);
                    }
                } catch (error) {
                    if (i === maxRetries - 1) throw error;
                    const delay = Math.pow(2, i) * 1000 + Math.random() * 1000;
                    await new Promise(resolve => setTimeout(resolve, delay));
                }
            }
        }

        /**
         * Updates the entire dashboard's mock data based on the active scenario.
         * @param {string} scenario 'A' or 'B'
         */
        function updateDashboardScenario(scenario) {
            const data = SCENARIO_DATA[scenario];

            // 1. Update Scenario Selector Button Style
            document.getElementById('scenario-a-btn').classList.remove('bg-accent-secondary', 'bg-gray-500');
            document.getElementById('scenario-b-btn').classList.remove('bg-accent-secondary', 'bg-gray-500');
            
            if (scenario === 'A') {
                document.getElementById('scenario-a-btn').classList.add('bg-accent-secondary');
                document.getElementById('scenario-b-btn').classList.add('bg-gray-500');
            } else {
                document.getElementById('scenario-a-btn').classList.add('bg-gray-500');
                document.getElementById('scenario-b-btn').classList.add('bg-accent-secondary');
            }

            // 2. Update KPI Panel (Section 1) - Revert country focus if active
            setActiveCountry('none'); // Resets KPI displays
            
            // 3. Update Risk Tower (Section 3)
            document.getElementById('risk-disruption').textContent = data.risks.disruption;
            document.getElementById('risk-currency').textContent = data.risks.currency;
            document.getElementById('risk-chokepoint').textContent = data.risks.chokepoint;
            
            // 4. Update Tech Panel (Section 5)
            const egovProgress = document.getElementById('egov-progress');
            if(egovProgress) egovProgress.style.width = `${data.ai}%`;

            const cloudProgress = document.getElementById('cloud-progress');
            if(cloudProgress) cloudProgress.style.width = `${data.cloud}%`;
            
            const aiAdoptionScore = document.getElementById('ai-adoption-score');
            if(aiAdoptionScore) aiAdoptionScore.textContent = `${data.ai.toFixed(1)}/10`;

            // 5. Update Mega Projects (Section 6)
            const neomProgress = document.getElementById('neom-progress-bar');
            if(neomProgress) neomProgress.style.width = `${data.mega.neom}%`;
            const neomLabel = document.getElementById('neom-progress-label');
            if(neomLabel) neomLabel.textContent = `${data.mega.neom}%`;

            const almProgress = document.getElementById('alm-progress-bar');
            if(almProgress) almProgress.style.width = `${data.mega.alm}%`;
            const almLabel = document.getElementById('alm-progress-label');
            if(almLabel) almLabel.textContent = `${data.mega.alm}%`;

            const dohaProgress = document.getElementById('doha-progress-bar');
            if(dohaProgress) dohaProgress.style.width = `${data.mega.doha}%`;
            const dohaLabel = document.getElementById('doha-progress-label');
            if(dohaLabel) dohaLabel.textContent = `${data.mega.doha}%`;


            // 6. Refetch Gemini Insights (Section 8)
            fetchConsultingInsights(data.gemini_prompt);
        }

        /**
         * Updates the primary KPI cards based on the selected country focus.
         * @param {string} countryId - 'ksa', 'uae', 'qatar', 'oman' or 'none'.
         */
        function setActiveCountry(countryId) {
            activeCountry = countryId;
            const scenario = SCENARIO_DATA[activeScenario];

            // Reset all map paths
            document.querySelectorAll('#gcc-map path').forEach(path => path.classList.remove('country-active'));
            
            // Set base values
            let kpi1 = scenario.gdp;
            let kpi2 = scenario.fdi;
            let kpi3 = scenario.risk;

            // Override if a specific country is active
            if (countryId !== 'none' && COUNTRY_FOCUS[countryId]) {
                const countryData = COUNTRY_FOCUS[countryId];
                const countryPath = document.getElementById(countryId);
                if(countryPath) countryPath.classList.add('country-active');

                kpi1 = { value: countryData.gdp, color: scenario.theme.secondary, icon: countryData.icon };
                kpi2 = { value: countryData.fdi, color: scenario.theme.primary, icon: 'banknote' };
            }
            
            // Apply KPI values and labels
            const kpiValue1 = document.getElementById('kpi-value-1');
            if(kpiValue1) kpiValue1.textContent = kpi1.value;
            const kpiLabel1 = document.getElementById('kpi-label-1');
            if(kpiLabel1) kpiLabel1.textContent = kpi1.label || 'Non-Oil GDP Growth (YoY)';
            if(kpiValue1) kpiValue1.style.color = kpi1.color;
            
            // --- FIX: Dynamic Icon Replacement ---
            const icon1Element = document.getElementById('kpi-icon-1');
            if(icon1Element) {
                icon1Element.innerHTML = ''; // Clear old SVG
                icon1Element.setAttribute('data-lucide', kpi1.icon || 'trending-up');
            }

            const kpiValue2 = document.getElementById('kpi-value-2');
            if(kpiValue2) kpiValue2.textContent = kpi2.value;
            const kpiLabel2 = document.getElementById('kpi-label-2');
            if(kpiLabel2) kpiLabel2.textContent = kpi2.label || 'FDI Inflows (LTM)';
            if(kpiValue2) kpiValue2.style.color = kpi2.color;

            const icon2Element = document.getElementById('kpi-icon-2');
            if(icon2Element) {
                icon2Element.innerHTML = ''; // Clear old SVG
                icon2Element.setAttribute('data-lucide', kpi2.icon || 'banknote');
            }
            
            // Re-render all icons that were just cleared
            lucide.createIcons();
            // --- FIX END ---

            // Risk KPI always uses scenario risk
            const kpiValue3 = document.getElementById('kpi-value-3');
            if(kpiValue3) kpiValue3.textContent = kpi3.value;
            const riskIndicator3 = document.getElementById('risk-indicator-3');
            if(riskIndicator3) {
                riskIndicator3.textContent = kpi3.indicator;
                riskIndicator3.className = `risk-indicator mt-3 text-center ${kpi3.class}`;
            }
        }

        /**
         * Fetches real-time strategic insights using the Gemini API with Google Search grounding.
         * @param {string} userQuery - The dynamic query based on the active scenario.
         */
        async function fetchConsultingInsights(userQuery) {
            const summaryContainer = document.getElementById('summary-content');
            
            // Show loading spinner
            const loadingSpinnerHtml = `
                <div id="loading-spinner" class="flex flex-col items-center justify-center text-text-muted-light">
                    <svg class="animate-spin h-8 w-8 text-accent-primary" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                        <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                    </svg>
                    <p class="mt-4 text-sm font-semibold text-accent-primary">Generating Real-time Strategic Insights using Gemini...</p>
                </div>
            `;
            summaryContainer.innerHTML = loadingSpinnerHtml;


            const systemPrompt = "Act as a senior strategy consultant specializing in the Gulf Cooperation Council (GCC) region. Generate a highly concise, 3-point summary in list format: 1. Top three current growth opportunities. 2. Top three critical risks. 3. A single, actionable strategic recommendation based on the data. Use only modern, high-impact consulting language.";
            
            const payload = {
                contents: [{ parts: [{ text: userQuery }] }],
                tools: [{ "google_search": {} }],
                systemInstruction: { parts: [{ text: systemPrompt }] },
            };

            try {
                const response = await exponentialBackoffFetch(API_URL + API_KEY, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                const result = await response.json();
                const candidate = result.candidates?.[0];

                if (!candidate || !candidate.content?.parts?.[0]?.text) {
                    throw new Error("Invalid response structure from Gemini API.");
                }

                const generatedText = candidate.content.parts[0].text;
                let sources = [];
                const groundingMetadata = candidate.groundingMetadata;
                
                if (groundingMetadata && groundingMetadata.groundingAttributions) {
                    sources = groundingMetadata.groundingAttributions
                        .map(attribution => ({
                            uri: attribution.web?.uri,
                            title: attribution.web?.title,
                        }))
                        .filter(source => source.uri && source.title);
                }

                // Format the output
                // Use a reliable way to replace list items and handle section titles
                const formattedText = generatedText
                    .replace(/1\. Top three current growth opportunities\s*:\s*/i, '<h4 class="font-bold mt-4 text-accent-secondary">1. Top Growth Opportunities:</h4><ul class="list-disc ml-5 text-sm space-y-1 text-text-dark">')
                    .replace(/2\. Top three critical risks\s*:\s*/i, '</ul><h4 class="font-bold mt-4 text-accent-danger">2. Critical Risks:</h4><ul class="list-disc ml-5 text-sm space-y-1 text-text-dark">')
                    .replace(/3\. A single, actionable strategic recommendation based on the data\s*:\s*/i, '</ul><h4 class="font-bold mt-4 text-accent-primary">3. Strategic Recommendation:</h4><p class="text-sm border-l-2 border-accent-primary pl-3 py-1 text-text-dark">')
                    .replace(/\n\s*-\s*/g, '<li>')
                    .replace(/\n\s*\*\s*/g, '<li>')
                    .replace(/\n/g, '<br>')
                    .replace(/:\s*<br>/g, ': ')
                    .replace(/<\/ul><br>/g, '</ul>');
                
                let htmlOutput = formattedText.endsWith('<br>') ? formattedText.slice(0, -4) + '</p>' : formattedText;
                if (!htmlOutput.includes('</p>')) {
                    htmlOutput += '</p>';
                }

                if (sources.length > 0) {
                    const uniqueSources = Array.from(new Map(sources.map(item => [item.uri, item])).values());
                    htmlOutput += `
                        <p class="text-xs font-semibold mt-6 text-text-muted-light">Source Grounding:</p>
                        <ul class="list-disc ml-4 text-xs text-text-muted-light space-y-0.5">
                            ${uniqueSources.slice(0, 3).map(s => `<li><a href="${s.uri}" target="_blank" class="hover:text-accent-primary transition-colors">${s.title}</a></li>`).join('')}
                        </ul>
                    `;
                }

                summaryContainer.innerHTML = htmlOutput;

            } catch (error) {
                console.error("Error fetching consulting insights:", error);
                summaryContainer.innerHTML = `
                    <p class="text-accent-danger font-semibold text-center">
                        Error retrieving live insights.<br>Please check console for details.
                    </p>
                `;
            }
        }


        // --- Chart.js Initialization ---
        function initCharts() {
            // Chart Defaults (Beige/Cream Mode)
            Chart.defaults.color = '#8b7355'; // text-muted-light
            Chart.defaults.font.family = 'Inter';

            // 1. Sustainability Emission Gauge (Section 4)
            const emissionGaugeCanvas = document.getElementById('emissionGauge');
            if (emissionGaugeCanvas) {
                const emissionGaugeCtx = emissionGaugeCanvas.getContext('2d');
                // Check if chart instance already exists to prevent duplication
                if (emissionGaugeCanvas.chart) {
                    emissionGaugeCanvas.chart.destroy();
                }
                emissionGaugeCanvas.chart = new Chart(emissionGaugeCtx, {
                    type: 'doughnut',
                    data: {
                        labels: ['Progress', 'Remaining'],
                        datasets: [{
                            data: [65, 35],
                            backgroundColor: [
                                '#6b8e23', // Progress (accent-secondary - Olive)
                                '#e0ddd5'
                            ],
                            borderWidth: 0,
                            circumference: 180,
                            rotation: 270
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: true,
                        cutout: '80%',
                        plugins: {
                            legend: { display: false },
                            tooltip: { enabled: false },
                        },
                        animation: {
                            onComplete: function(animation) {
                                const ctx = emissionGaugeCtx;
                                const chart = animation.chart;
                                const area = chart.chartArea;
                                const height = area.bottom - area.top;
                                ctx.restore();
                                const fontSize = (height / 114).toFixed(2);
                                ctx.font = fontSize + "em Inter";
                                ctx.textBaseline = "middle";

                                const text = '65%';
                                const textX = Math.round((area.left + area.right) / 2);
                                const textY = Math.round(area.bottom * 0.85);

                                ctx.fillStyle = '#3c2f2f';
                                ctx.textAlign = 'center';
                                ctx.fillText(text, textX, textY);
                                ctx.save();
                            }
                        }
                    }
                });
            }


            // 2. Tech Modernization Radar Chart (Section 5)
            const techRadarCanvas = document.getElementById('techRadarChart');
            if (techRadarCanvas) {
                const techRadarCtx = techRadarCanvas.getContext('2d');
                 // Check if chart instance already exists to prevent duplication
                if (techRadarCanvas.chart) {
                    techRadarCanvas.chart.destroy();
                }
                techRadarCanvas.chart = new Chart(techRadarCtx, {
                    type: 'radar',
                    data: {
                        labels: ['AI Adoption', 'Cloud Usage', 'Fintech Rate', 'Smart Cities', 'E-Govt', 'Cybersecurity'],
                        datasets: [{
                            label: 'UAE Readiness',
                            data: [8, 9, 7.5, 9, 8, 7],
                            fill: true,
                            backgroundColor: 'rgba(184, 134, 11, 0.2)',
                            borderColor: '#b8860b',
                            pointBackgroundColor: '#b8860b',
                            pointBorderColor: '#fff',
                            pointHoverBackgroundColor: '#fff',
                            pointHoverBorderColor: '#b8860b'
                        }, {
                            label: 'KSA Readiness',
                            data: [7, 7, 8, 7.5, 7, 6.5],
                            fill: true,
                            backgroundColor: 'rgba(218, 165, 32, 0.2)',
                            borderColor: '#daa520',
                            pointBackgroundColor: '#daa520',
                            pointBorderColor: '#fff',
                            pointHoverBackgroundColor: '#fff',
                            pointHoverBorderColor: '#daa520'
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: true,
                        plugins: {
                            legend: {
                                position: 'bottom',
                                labels: { color: '#3c2f2f' }
                            },
                            title: {
                                display: true,
                                text: 'Country Comparison (Scale 1-10)',
                                color: '#3c2f2f',
                                font: { size: 14, weight: '600' }
                            }
                        },
                        scales: {
                            r: {
                                angleLines: { color: '#e0ddd5' },
                                grid: { color: '#e0ddd5' },
                                pointLabels: { color: '#8b7355', font: { size: 11 } },
                                suggestedMin: 5,
                                suggestedMax: 10,
                                ticks: {
                                    backdropColor: '#fcf8f3',
                                    color: '#8b7355'
                                }
                            }
                        }
                    }
                });
            }
        }

        // --- Event Listeners and Initialization ---
        
        function setupEventListeners() {
            // Country Map Click Listener
            document.querySelectorAll('#gcc-map path').forEach(path => {
                path.addEventListener('click', function() {
                    const countryId = this.getAttribute('data-country');
                    setActiveCountry(countryId);
                });
            });

            // Scenario Button Listeners
            document.getElementById('scenario-a-btn').addEventListener('click', function() {
                activeScenario = 'A';
                updateDashboardScenario('A');
            });
            document.getElementById('scenario-b-btn').addEventListener('click', function() {
                activeScenario = 'B';
                updateDashboardScenario('B');
            });
        }

        function initializeApp() {
            // Re-initialize charts on load/resize if needed, or destroy them first to prevent duplication
            initCharts(); 
            setupEventListeners();
            
            // Set initial state (Scenario A, no country focus)
            updateDashboardScenario('A');
            setActiveCountry('none');
        }

        // Use DOMContentLoaded which fires when the HTML structure is loaded
        document.addEventListener('DOMContentLoaded', initializeApp);

    </script>
</body>
</html>
