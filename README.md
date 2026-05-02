<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Periodic Table</title>
    <link rel="stylesheet" href="style.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
</head>
<body>
    <div class="background-decorations">
        <div class="blob blob-1"></div>
        <div class="blob blob-2"></div>
        <div class="blob blob-3"></div>
    </div>

    <div class="app-container">
        <!-- Main Periodic Table View -->
        <main class="table-area">
            <header>
                <h1>Tabel Periodik Unsur</h1>
            </header>
            
            <div id="periodic-table" class="periodic-table">
                <!-- Elements will be injected here via JavaScript -->
            </div>

            <!-- Hover Tooltip -->
            <div id="tooltip" class="element-tooltip hidden">
                <div class="tooltip-header">
                    <span class="tooltip-number" id="tt-number"></span>
                    <span class="tooltip-mass" id="tt-mass"></span>
                </div>
                <div class="tooltip-symbol" id="tt-symbol"></div>
                <div class="tooltip-name" id="tt-name"></div>
            </div>
        </main>

        <!-- Right Side Information Panel -->
        <aside class="info-panel" id="info-panel">
            <div class="info-content hidden" id="info-content">
                <h2 class="info-title">
                    <span id="panel-name">Actinium</span> 
                    (<span id="panel-symbol">Ac</span>)<sup id="panel-number" class="superscript">89</sup>
                </h2>
                <div class="info-category">
                    <span class="category-dot" id="panel-category-dot"></span>
                    <span id="panel-category-text">Actinide</span>
                </div>

                <div class="info-model">
                    <!-- Bohr model animation container -->
                    <div class="bohr-model" id="bohr-model">
                        <div class="nucleus" id="nucleus">
                            <span id="nucleus-symbol">Ac</span>
                        </div>
                        <div class="orbits" id="orbits">
                            <!-- Orbit rings and electrons will be injected here via JS -->
                        </div>
                    </div>
                </div>

                <div class="info-details">
                    <h3 class="detail-subtitle">Representasi Model Bohr</h3>
                    <p id="panel-description" class="detail-description">
                        Aktinium bersinar dalam gelap dengan cahaya biru pucat, yang berasal dari udara di sekitarnya yang terionisasi oleh partikel berenergi yang dipancarkan.
                    </p>
                    
                    <div class="detail-row">
                        <span class="detail-label">Simbol:</span>
                        <span class="detail-value" id="panel-detail-symbol">Ac</span>
                    </div>
                    <div class="detail-row">
                        <span class="detail-label">Massa atom:</span>
                        <span class="detail-value"><span id="panel-detail-mass">227</span> u</span>
                    </div>
                    <div class="detail-row">
                        <span class="detail-label">Massa jenis:</span>
                        <span class="detail-value" id="panel-density">10 g/cm³</span>
                    </div>
                    <div class="detail-row">
                        <span class="detail-label">Titik lebur:</span>
                        <span class="detail-value" id="panel-melt">1324 K</span>
                    </div>
                    <div class="detail-row">
                        <span class="detail-label">Titik didih:</span>
                        <span class="detail-value" id="panel-boil">3471 K</span>
                    </div>
                    <div class="detail-row">
                        <span class="detail-label">Konfigurasi Elektron:</span>
                        <span class="detail-value" id="panel-configuration">[Rn] 6d1 7s2</span>
                    </div>
                </div>
            </div>
            <div class="info-placeholder" id="info-placeholder">
                <p>Pilih salah satu unsur untuk melihat detailnya</p>
            </div>
        </aside>
    </div>

    <script src="script.js"></script>
</body>
</html>
:root {
    /* Color Palette for element categories */
    --alkali-metal: #ff6b6b;
    --alkaline-earth: #feca57;
    --transition-metal: #48dbfb;
    --post-transition: #0abde3;
    --metalloid: #1dd1a1;
    --nonmetal: #5f27cd;
    --halogen: #ff9ff3;
    --noble-gas: #e58e26;
    --lanthanide: #ffc048;
    --actinide: #ff5252;
    --unknown: #8395a7;

    /* Liquid Glass Variables */
    --glass-bg: rgba(255, 255, 255, 0.05);
    --glass-border: rgba(255, 255, 255, 0.1);
    --glass-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
    --glass-blur: blur(12px);

    /* Background Theme */
    --bg-color: #0f172a;
    --text-main: #f8fafc;
    --text-muted: #94a3b8;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Inter', sans-serif;
}

body {
    background-color: var(--bg-color);
    color: var(--text-main);
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow-x: hidden;
    position: relative;
}

/* Background Animated Blobs for Liquid Feel */
.background-decorations {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: -1;
    overflow: hidden;
}

.blob {
    position: absolute;
    border-radius: 50%;
    filter: blur(80px);
    opacity: 0.5;
    animation: float 20s infinite ease-in-out alternate;
}

.blob-1 {
    width: 500px;
    height: 500px;
    background: #4facfe;
    top: -100px;
    left: -100px;
    animation-delay: 0s;
}

.blob-2 {
    width: 400px;
    height: 400px;
    background: #00f2fe;
    bottom: -100px;
    right: 10%;
    animation-delay: -5s;
}

.blob-3 {
    width: 600px;
    height: 600px;
    background: #667eea;
    top: 30%;
    left: 40%;
    opacity: 0.3;
    animation-delay: -10s;
}

@keyframes float {
    0% { transform: translate(0, 0) scale(1); }
    100% { transform: translate(50px, 50px) scale(1.1); }
}

/* App Layout */
.app-container {
    display: flex;
    gap: 30px;
    width: 95%;
    max-width: 1600px;
    height: 90vh;
    padding: 20px;
    border-radius: 24px;
    background: var(--glass-bg);
    backdrop-filter: var(--glass-blur);
    border: 1px solid var(--glass-border);
    box-shadow: var(--glass-shadow);
}

.table-area {
    flex: 1;
    display: flex;
    flex-direction: column;
    position: relative;
}

header {
    margin-bottom: 20px;
    text-align: center;
}

h1 {
    font-weight: 300;
    letter-spacing: 2px;
    text-transform: uppercase;
    font-size: 1.5rem;
    color: rgba(255,255,255,0.8);
}

/* Periodic Table Grid */
.periodic-table {
    display: grid;
    grid-template-columns: repeat(18, 1fr);
    grid-template-rows: repeat(10, 1fr);
    gap: 4px;
    width: 100%;
    height: 100%;
    perspective: 1000px;
}

.element {
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 4px;
    border-radius: 8px;
    background: rgba(255,255,255,0.05); /* Base glass */
    backdrop-filter: blur(5px);
    border: 1px solid rgba(255,255,255,0.1);
    cursor: pointer;
    transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
    overflow: hidden;
}

/* Hover Liquid Glass Effect */
.element::before {
    content: '';
    position: absolute;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background: radial-gradient(circle, rgba(255,255,255,0.3) 0%, transparent 60%);
    opacity: 0;
    transition: opacity 0.3s ease;
    pointer-events: none;
    mix-blend-mode: overlay;
}

.element:hover {
    transform: translateY(-5px) scale(1.05) translateZ(20px);
    box-shadow: 0 10px 20px rgba(0,0,0,0.4), inset 0 0 15px rgba(255,255,255,0.2);
    z-index: 10;
    border-color: rgba(255,255,255,0.4);
}

.element:hover::before {
    opacity: 1;
}

.element.selected {
    transform: scale(1.05);
    box-shadow: 0 0 20px rgba(255,255,255,0.5), inset 0 0 15px rgba(255,255,255,0.4);
    z-index: 5;
    border-color: rgba(255,255,255,0.8);
}

.el-header {
    display: flex;
    justify-content: space-between;
    font-size: 0.65rem;
    font-weight: 600;
    color: rgba(255,255,255,0.8);
}

.el-symbol {
    font-size: 1.2rem;
    font-weight: 700;
    text-align: center;
    margin: auto 0;
}

.el-name {
    font-size: 0.55rem;
    text-align: center;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    opacity: 0.8;
}

/* Hover Tooltip (Image 2) */
.element-tooltip {
    position: absolute;
    pointer-events: none;
    z-index: 100;
    width: 120px;
    height: 120px;
    background: rgba(40, 20, 30, 0.85); /* Slightly reddish dark bg like in ref */
    backdrop-filter: blur(15px);
    border: 1px solid rgba(255,255,255,0.2);
    border-radius: 12px;
    box-shadow: 0 15px 30px rgba(0,0,0,0.5), inset 0 0 20px rgba(255,255,255,0.1);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 10px;
    transform: translate(-50%, -50%) scale(0);
    opacity: 0;
    transition: transform 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275), opacity 0.2s;
    transform-origin: center;
}

.element-tooltip.show {
    transform: translate(-50%, -50%) scale(1);
    opacity: 1;
}

.tooltip-header {
    display: flex;
    justify-content: space-between;
    font-size: 0.9rem;
    font-weight: 600;
    color: #e2e8f0;
}

.tooltip-symbol {
    font-size: 3rem;
    font-weight: 700;
    text-align: center;
    color: #fff;
    line-height: 1;
}

.tooltip-name {
    font-size: 0.85rem;
    text-align: center;
    color: #cbd5e1;
}

/* Right Side Panel (Image 1) */
.info-panel {
    width: 350px;
    background: var(--glass-bg);
    backdrop-filter: blur(20px);
    border-radius: 16px;
    border: 1px solid var(--glass-border);
    padding: 25px;
    display: flex;
    flex-direction: column;
    box-shadow: var(--glass-shadow);
    overflow-y: auto;
}

.info-panel::-webkit-scrollbar {
    width: 6px;
}
.info-panel::-webkit-scrollbar-thumb {
    background: rgba(255,255,255,0.2);
    border-radius: 3px;
}

.hidden {
    display: none !important;
}

.info-placeholder {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    color: var(--text-muted);
    font-size: 1.1rem;
    text-align: center;
}

.info-title {
    font-size: 2rem;
    font-weight: 300;
    margin-bottom: 5px;
}

.superscript {
    font-size: 1rem;
    vertical-align: super;
}

.info-category {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 0.9rem;
    color: var(--text-muted);
    margin-bottom: 25px;
}

.category-dot {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background: #fff;
    box-shadow: 0 0 10px currentColor; /* glow effect */
}

/* Bohr Model Container */
.info-model {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 200px;
    margin-bottom: 30px;
    position: relative;
}

.bohr-model {
    position: relative;
    width: 150px;
    height: 150px;
}

.nucleus {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 30px;
    height: 30px;
    background: radial-gradient(circle at 30% 30%, #ff4757, #ff6b81);
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 0.7rem;
    font-weight: bold;
    color: white;
    z-index: 10;
    box-shadow: 0 0 20px #ff4757;
}

.orbit {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border: 1px dashed rgba(255,255,255,0.2);
    border-radius: 50%;
    animation: rotate infinite linear;
}

.electron {
    position: absolute;
    width: 6px;
    height: 6px;
    background: #4facfe;
    border-radius: 50%;
    top: -3px;
    left: 50%;
    transform: translateX(-50%);
    box-shadow: 0 0 8px #4facfe;
}

@keyframes rotate {
    0% { transform: translate(-50%, -50%) rotate(0deg); }
    100% { transform: translate(-50%, -50%) rotate(360deg); }
}

.detail-subtitle {
    font-size: 0.8rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    color: var(--text-muted);
    margin-bottom: 10px;
}

.detail-description {
    font-size: 0.95rem;
    line-height: 1.5;
    margin-bottom: 25px;
    color: rgba(255,255,255,0.9);
}

.detail-row {
    display: flex;
    justify-content: space-between;
    padding: 10px 0;
    border-bottom: 1px solid rgba(255,255,255,0.1);
}

.detail-row:last-child {
    border-bottom: none;
}

.detail-label {
    color: var(--text-muted);
    font-size: 0.9rem;
}

.detail-value {
    font-weight: 600;
    font-size: 0.95rem;
}

/* Category Colors Classes */
.alkali-metal { background: rgba(255, 107, 107, 0.15); border-color: rgba(255, 107, 107, 0.3); }
.alkaline-earth { background: rgba(254, 202, 87, 0.15); border-color: rgba(254, 202, 87, 0.3); }
.transition-metal { background: rgba(72, 219, 251, 0.15); border-color: rgba(72, 219, 251, 0.3); }
.post-transition { background: rgba(10, 189, 227, 0.15); border-color: rgba(10, 189, 227, 0.3); }
.metalloid { background: rgba(29, 209, 161, 0.15); border-color: rgba(29, 209, 161, 0.3); }
.nonmetal { background: rgba(95, 39, 205, 0.15); border-color: rgba(95, 39, 205, 0.3); }
.halogen { background: rgba(255, 159, 243, 0.15); border-color: rgba(255, 159, 243, 0.3); }
.noble-gas { background: rgba(229, 142, 38, 0.15); border-color: rgba(229, 142, 38, 0.3); }
.lanthanide { background: rgba(255, 192, 72, 0.15); border-color: rgba(255, 192, 72, 0.3); }
.actinide { background: rgba(255, 82, 82, 0.15); border-color: rgba(255, 82, 82, 0.3); }
.unknown { background: rgba(131, 149, 167, 0.15); border-color: rgba(131, 149, 167, 0.3); }

/* Corresponding colors for dots */
.dot-alkali-metal { background: #ff6b6b; color: #ff6b6b; }
.dot-alkaline-earth { background: #feca57; color: #feca57; }
.dot-transition-metal { background: #48dbfb; color: #48dbfb; }
.dot-post-transition { background: #0abde3; color: #0abde3; }
.dot-metalloid { background: #1dd1a1; color: #1dd1a1; }
.dot-nonmetal { background: #5f27cd; color: #5f27cd; }
.dot-halogen { background: #ff9ff3; color: #ff9ff3; }
.dot-noble-gas { background: #e58e26; color: #e58e26; }
.dot-lanthanide { background: #ffc048; color: #ffc048; }
.dot-actinide { background: #ff5252; color: #ff5252; }
.dot-unknown { background: #8395a7; color: #8395a7; }

/* Responsive adjustments */
@media (max-width: 1200px) {
    .app-container {
        flex-direction: column;
        height: auto;
    }
    .info-panel {
        width: 100%;
        max-height: 400px;
    }
}
const elementsData = [
    {
        "number": 1,
        "symbol": "H",
        "name": "Hydrogen",
        "mass": "1.008",
        "col": 1,
        "row": 1,
        "category": "nonmetal",
        "desc": "Hidrogen adalah suatu unsur kimia dengan lambang kimia H dan nomor atom 1. Dengan berat atom 1,00794 u, hidrogen merupakan unsur paling ringan dalam tabel periodik. Bentuk monatomiknya (H) adalah zat kimia paling melimpah di Alam Semesta, yang mencakup sekitar 75% dari seluruh massa barionik.",
        "config": "1s1",
        "melt": "13.99 K",
        "boil": "20.271 K",
        "density": "0.08988 g/cm\u00b3"
    },
    {
        "number": 2,
        "symbol": "He",
        "name": "Helium",
        "mass": "4.0026022",
        "col": 18,
        "row": 1,
        "category": "noble-gas",
        "desc": "Helium adalah unsur kimia dengan simbol He dan nomor atom 2. Helium adalah gas monoatomik yang tidak berwarna, tidak berbau, tidak berasa, tidak beracun, inert, dan mengepalai kelompok gas mulia dalam tabel periodik. Titik didih dan titik lelehnya paling rendah diantara semua unsur.",
        "config": "1s2",
        "melt": "0.95 K",
        "boil": "4.222 K",
        "density": "0.1786 g/cm\u00b3"
    },
    {
        "number": 3,
        "symbol": "Li",
        "name": "Lithium",
        "mass": "6.94",
        "col": 1,
        "row": 2,
        "category": "alkali-metal",
        "desc": "Litium (dari bahasa Yunani:\u03bb\u03af\u03b8\u03bf\u03c2 lithos, \"batu\") adalah suatu unsur kimia dengan lambang Li dan nomor atom 3. Merupakan logam lunak berwarna putih keperakan yang termasuk dalam kelompok unsur kimia logam alkali. Dalam kondisi standar, ini adalah logam paling ringan dan unsur padat paling padat.",
        "config": "1s2 2s1",
        "melt": "453.65 K",
        "boil": "1603 K",
        "density": "0.534 g/cm\u00b3"
    },
    {
        "number": 4,
        "symbol": "Be",
        "name": "Beryllium",
        "mass": "9.01218315",
        "col": 2,
        "row": 2,
        "category": "alkaline-earth",
        "desc": "Berilium adalah unsur kimia dengan simbol Be dan nomor atom 4. Berilium tercipta melalui nukleosintesis bintang dan merupakan unsur yang relatif langka di alam semesta. Ini adalah unsur divalen yang terjadi secara alami hanya dalam kombinasi dengan unsur lain dalam mineral.",
        "config": "1s2 2s2",
        "melt": "1560 K",
        "boil": "2742 K",
        "density": "1.85 g/cm\u00b3"
    },
    {
        "number": 5,
        "symbol": "B",
        "name": "Boron",
        "mass": "10.81",
        "col": 13,
        "row": 2,
        "category": "metalloid",
        "desc": "Boron adalah unsur kimia metaloid dengan simbol B dan nomor atom 5. Diproduksi seluruhnya oleh spalasi sinar kosmik dan supernova dan bukan oleh nukleosintesis bintang, boron merupakan unsur dengan kelimpahan rendah di Tata Surya dan kerak bumi. Boron terkonsentrasi di Bumi karena kelarutan dalam air dari senyawa alami yang lebih umum, yaitu mineral borat.",
        "config": "1s2 2s2 2p1",
        "melt": "2349 K",
        "boil": "4200 K",
        "density": "2.08 g/cm\u00b3"
    },
    {
        "number": 6,
        "symbol": "C",
        "name": "Carbon",
        "mass": "12.011",
        "col": 14,
        "row": 2,
        "category": "nonmetal",
        "desc": "Karbon (dari bahasa Latin:carbo \"batubara\") adalah suatu unsur kimia dengan lambang C dan nomor atom 6. Pada tabel periodik, karbon merupakan unsur pertama (baris 2) dari enam unsur dalam kolom (golongan) 14, yang memiliki komposisi kulit elektron terluar yang sama. Ini bukan logam dan tetravalen \u2014 membuat empat elektron tersedia untuk membentuk ikatan kimia kovalen.",
        "config": "1s2 2s2 2p2",
        "melt": "Unknown",
        "boil": "Unknown",
        "density": "1.821 g/cm\u00b3"
    },
    {
        "number": 7,
        "symbol": "N",
        "name": "Nitrogen",
        "mass": "14.007",
        "col": 15,
        "row": 2,
        "category": "nonmetal",
        "desc": "Nitrogen adalah unsur kimia dengan simbol N dan nomor atom 7. Nitrogen adalah pniktogen paling ringan dan pada suhu kamar, merupakan gas diatomik transparan dan tidak berbau. Nitrogen adalah unsur umum di alam semesta, diperkirakan berada pada urutan ketujuh dalam kelimpahan total di Bima Sakti dan Tata Surya.",
        "config": "1s2 2s2 2p3",
        "melt": "63.15 K",
        "boil": "77.355 K",
        "density": "1.251 g/cm\u00b3"
    },
    {
        "number": 8,
        "symbol": "O",
        "name": "Oxygen",
        "mass": "15.999",
        "col": 16,
        "row": 2,
        "category": "nonmetal",
        "desc": "Oksigen adalah unsur kimia dengan simbol O dan nomor atom 8. Ia adalah anggota kelompok kalkogen pada tabel periodik dan merupakan zat bukan logam dan pengoksidasi yang sangat reaktif yang mudah membentuk senyawa (terutama oksida) dengan sebagian besar unsur. Berdasarkan massanya, oksigen adalah unsur ketiga terbanyak di alam semesta, setelah hidrogen dan helium.",
        "config": "1s2 2s2 2p4",
        "melt": "54.36 K",
        "boil": "90.188 K",
        "density": "1.429 g/cm\u00b3"
    },
    {
        "number": 9,
        "symbol": "F",
        "name": "Fluorine",
        "mass": "18.9984031636",
        "col": 17,
        "row": 2,
        "category": "nonmetal",
        "desc": "Fluor adalah unsur kimia dengan simbol F dan nomor atom 9. Ini adalah halogen paling ringan dan terdapat sebagai gas diatomik kuning pucat yang sangat beracun pada kondisi standar. Sebagai unsur yang paling elektronegatif, ia sangat reaktif: hampir semua unsur lainnya, termasuk beberapa gas mulia, membentuk senyawa dengan fluor.",
        "config": "1s2 2s2 2p5",
        "melt": "53.48 K",
        "boil": "85.03 K",
        "density": "1.696 g/cm\u00b3"
    },
    {
        "number": 10,
        "symbol": "Ne",
        "name": "Neon",
        "mass": "20.17976",
        "col": 18,
        "row": 2,
        "category": "noble-gas",
        "desc": "Neon adalah suatu unsur kimia dengan lambang Ne dan nomor atom 10. Ia termasuk dalam golongan 18 (gas mulia) pada tabel periodik. Neon adalah gas monatomik inert yang tidak berwarna, tidak berbau, dalam kondisi standar, dengan kepadatan sekitar dua pertiga udara.",
        "config": "1s2 2s2 2p6",
        "melt": "24.56 K",
        "boil": "27.104 K",
        "density": "0.9002 g/cm\u00b3"
    },
    {
        "number": 11,
        "symbol": "Na",
        "name": "Sodium",
        "mass": "22.989769282",
        "col": 1,
        "row": 3,
        "category": "alkali-metal",
        "desc": "Natrium /\u02c8so\u028adi\u0259m/ adalah suatu unsur kimia dengan simbol Na (dari bahasa Yunani Kuno \u039d\u03ac\u03c4\u03c1\u03b9\u03bf) dan nomor atom 11. Merupakan logam lunak, berwarna putih keperakan, dan sangat reaktif. Dalam tabel periodik unsur ini berada di kolom 1 (logam alkali), dan sama dengan enam unsur lain dalam kolom tersebut bahwa ia mempunyai satu elektron pada kulit terluarnya, yang siap didonasikannya, sehingga menghasilkan atom bermuatan positif - kation.",
        "config": "1s2 2s2 2p6 3s1",
        "melt": "370.944 K",
        "boil": "1156.09 K",
        "density": "0.968 g/cm\u00b3"
    },
    {
        "number": 12,
        "symbol": "Mg",
        "name": "Magnesium",
        "mass": "24.305",
        "col": 2,
        "row": 3,
        "category": "alkaline-earth",
        "desc": "Magnesium adalah suatu unsur kimia dengan simbol Mg dan nomor atom 12. Magnesium merupakan padatan berwarna abu-abu mengkilat yang memiliki kemiripan fisik dengan lima unsur lainnya pada kolom kedua (golongan 2, atau logam alkali tanah) pada tabel periodik: masing-masing unsur tersebut mempunyai konfigurasi elektron yang sama pada kulit elektron terluarnya yang menghasilkan struktur kristal serupa. Magnesium adalah unsur paling melimpah kesembilan di alam semesta.",
        "config": "1s2 2s2 2p6 3s2",
        "melt": "923 K",
        "boil": "1363 K",
        "density": "1.738 g/cm\u00b3"
    },
    {
        "number": 13,
        "symbol": "Al",
        "name": "Aluminium",
        "mass": "26.98153857",
        "col": 13,
        "row": 3,
        "category": "transition-metal",
        "desc": "Aluminium (atau aluminium; lihat akhiran yang berbeda) adalah suatu unsur kimia dalam golongan boron dengan simbol Al dan nomor atom 13. Aluminium adalah logam berwarna putih keperakan, lunak, nonmagnetik, dan ulet. Aluminium adalah unsur paling melimpah ketiga (setelah oksigen dan silikon), dan logam paling melimpah di kerak bumi.",
        "config": "1s2 2s2 2p6 3s2 3p1",
        "melt": "933.47 K",
        "boil": "2743 K",
        "density": "2.7 g/cm\u00b3"
    },
    {
        "number": 14,
        "symbol": "Si",
        "name": "Silicon",
        "mass": "28.085",
        "col": 14,
        "row": 3,
        "category": "metalloid",
        "desc": "Silikon adalah unsur kimia dengan simbol Si dan nomor atom 14. Ini adalah metaloid tetravalen, lebih reaktif daripada germanium, metaloid tepat di bawahnya dalam tabel. Kontroversi tentang karakter silikon berawal dari penemuannya.",
        "config": "1s2 2s2 2p6 3s2 3p2",
        "melt": "1687 K",
        "boil": "3538 K",
        "density": "2.329 g/cm\u00b3"
    },
    {
        "number": 15,
        "symbol": "P",
        "name": "Phosphorus",
        "mass": "30.9737619985",
        "col": 15,
        "row": 3,
        "category": "nonmetal",
        "desc": "Fosfor adalah unsur kimia dengan simbol P dan nomor atom 15. Sebagai suatu unsur, fosfor terdapat dalam dua bentuk utama\u2014fosfor putih dan fosfor merah\u2014tetapi karena reaktivitasnya yang tinggi, fosfor tidak pernah ditemukan sebagai unsur bebas di Bumi. Sebaliknya mineral yang mengandung fosfor hampir selalu ada dalam keadaan teroksidasi maksimal, seperti batuan fosfat anorganik.",
        "config": "1s2 2s2 2p6 3s2 3p3",
        "melt": "Unknown",
        "boil": "Unknown",
        "density": "1.823 g/cm\u00b3"
    },
    {
        "number": 16,
        "symbol": "S",
        "name": "Sulfur",
        "mass": "32.06",
        "col": 16,
        "row": 3,
        "category": "nonmetal",
        "desc": "Belerang atau belerang (lihat perbedaan ejaan) adalah unsur kimia dengan simbol S dan nomor atom 16. Ia merupakan unsur non-logam multivalen yang berlimpah. Dalam kondisi normal, atom belerang membentuk molekul oktatom siklik dengan rumus kimia S8.",
        "config": "1s2 2s2 2p6 3s2 3p4",
        "melt": "388.36 K",
        "boil": "717.8 K",
        "density": "2.07 g/cm\u00b3"
    },
    {
        "number": 17,
        "symbol": "Cl",
        "name": "Chlorine",
        "mass": "35.45",
        "col": 17,
        "row": 3,
        "category": "nonmetal",
        "desc": "Klorin adalah unsur kimia dengan lambang Cl dan nomor atom 17. Ia juga memiliki massa atom relatif 35,5. Klorin berada dalam kelompok halogen (17) dan merupakan halogen paling ringan kedua setelah fluor.",
        "config": "1s2 2s2 2p6 3s2 3p5",
        "melt": "171.6 K",
        "boil": "239.11 K",
        "density": "3.2 g/cm\u00b3"
    },
    {
        "number": 18,
        "symbol": "Ar",
        "name": "Argon",
        "mass": "39.9481",
        "col": 18,
        "row": 3,
        "category": "noble-gas",
        "desc": "Argon adalah suatu unsur kimia dengan lambang Ar dan nomor atom 18. Argon berada pada golongan 18 tabel periodik dan merupakan gas mulia. Argon adalah gas paling umum ketiga di atmosfer bumi, dengan kandungan 0,934% (9,340 ppmv), menjadikannya dua kali lebih banyak dari gas atmosfer paling umum berikutnya, uap air (yang rata-rata sekitar 4000 ppmv, namun sangat bervariasi), dan 23 kali lebih banyak dari gas atmosfer non-kondensasi paling umum berikutnya, karbon dioksida (400 ppmv), dan lebih dari 500 kali lebih banyak dari gas mulia paling umum berikutnya, neon (18 ppmv).",
        "config": "1s2 2s2 2p6 3s2 3p6",
        "melt": "83.81 K",
        "boil": "87.302 K",
        "density": "1.784 g/cm\u00b3"
    },
    {
        "number": 19,
        "symbol": "K",
        "name": "Potassium",
        "mass": "39.09831",
        "col": 1,
        "row": 4,
        "category": "alkali-metal",
        "desc": "Kalium adalah unsur kimia dengan simbol K (berasal dari Neo-Latin, kalium) dan nomor atom 19. Kalium pertama kali diisolasi dari kalium, abu tanaman, yang menjadi asal mula namanya. Dalam tabel periodik, kalium adalah salah satu dari tujuh unsur dalam kolom (golongan) 1 (logam alkali): semuanya mempunyai satu elektron valensi di kulit elektron terluarnya, yang siap dilepaskan untuk membentuk atom bermuatan positif - kation, dan bergabung dengan anion membentuk garam.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s1",
        "melt": "336.7 K",
        "boil": "1032 K",
        "density": "0.862 g/cm\u00b3"
    },
    {
        "number": 20,
        "symbol": "Ca",
        "name": "Calcium",
        "mass": "40.0784",
        "col": 2,
        "row": 4,
        "category": "alkaline-earth",
        "desc": "Kalsium adalah unsur kimia dengan simbol Ca dan nomor atom 20. Kalsium adalah logam alkali tanah berwarna abu-abu lembut, unsur kelima paling melimpah berdasarkan massa di kerak bumi. Ion Ca2+ juga merupakan ion terlarut kelima terbanyak dalam air laut berdasarkan molaritas dan massa, setelah natrium, klorida, magnesium, dan sulfat.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2",
        "melt": "1115 K",
        "boil": "1757 K",
        "density": "1.55 g/cm\u00b3"
    },
    {
        "number": 21,
        "symbol": "Sc",
        "name": "Scandium",
        "mass": "44.9559085",
        "col": 3,
        "row": 4,
        "category": "transition-metal",
        "desc": "Skandium adalah suatu unsur kimia dengan simbol Sc dan nomor atom 21. Merupakan unsur blok d metalik berwarna putih keperakan, secara historis kadang-kadang diklasifikasikan sebagai unsur tanah jarang, bersama dengan yttrium dan lantanoid. Ditemukan pada tahun 1879 melalui analisis spektral mineral euxenite dan gadolinite dari Skandinavia.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d1",
        "melt": "1814 K",
        "boil": "3109 K",
        "density": "2.985 g/cm\u00b3"
    },
    {
        "number": 22,
        "symbol": "Ti",
        "name": "Titanium",
        "mass": "47.8671",
        "col": 4,
        "row": 4,
        "category": "transition-metal",
        "desc": "Titanium adalah unsur kimia dengan simbol Ti dan nomor atom 22. Merupakan logam transisi berkilau dengan warna perak, kepadatan rendah dan kekuatan tinggi. Sangat tahan terhadap korosi pada air laut, aqua regia dan klorin.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d2",
        "melt": "1941 K",
        "boil": "3560 K",
        "density": "4.506 g/cm\u00b3"
    },
    {
        "number": 23,
        "symbol": "V",
        "name": "Vanadium",
        "mass": "50.94151",
        "col": 5,
        "row": 4,
        "category": "transition-metal",
        "desc": "Vanadium adalah unsur kimia dengan simbol V dan nomor atom 23. Merupakan logam transisi yang keras, berwarna abu-abu keperakan, ulet, dan mudah dibentuk. Unsur ini hanya ditemukan dalam bentuk gabungan kimia di alam, tetapi setelah diisolasi secara artifisial, pembentukan lapisan oksida akan menstabilkan logam bebas terhadap oksidasi lebih lanjut.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d3",
        "melt": "2183 K",
        "boil": "3680 K",
        "density": "6 g/cm\u00b3"
    },
    {
        "number": 24,
        "symbol": "Cr",
        "name": "Chromium",
        "mass": "51.99616",
        "col": 6,
        "row": 4,
        "category": "transition-metal",
        "desc": "Kromium adalah suatu unsur kimia dengan simbol Cr dan nomor atom 24. Kromium adalah unsur pertama dalam Golongan 6. Kromium merupakan logam berwarna abu-abu baja, berkilau, keras dan rapuh, mudah dipoles, tahan noda, dan memiliki titik leleh tinggi.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s1 3d5",
        "melt": "2180 K",
        "boil": "2944 K",
        "density": "7.19 g/cm\u00b3"
    },
    {
        "number": 25,
        "symbol": "Mn",
        "name": "Manganese",
        "mass": "54.9380443",
        "col": 7,
        "row": 4,
        "category": "transition-metal",
        "desc": "Mangan adalah suatu unsur kimia dengan simbol Mn dan nomor atom 25. Ia tidak ditemukan sebagai unsur bebas di alam; sering ditemukan dalam kombinasi dengan zat besi, dan banyak mineral. Mangan adalah logam dengan kegunaan paduan logam industri yang penting, khususnya pada baja tahan karat.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d5",
        "melt": "1519 K",
        "boil": "2334 K",
        "density": "7.21 g/cm\u00b3"
    },
    {
        "number": 26,
        "symbol": "Fe",
        "name": "Iron",
        "mass": "55.8452",
        "col": 8,
        "row": 4,
        "category": "transition-metal",
        "desc": "Besi adalah suatu unsur kimia dengan lambang Fe (dari bahasa Latin:ferrum) dan nomor atom 26. Merupakan logam pada deret transisi pertama. Berdasarkan massanya, unsur ini merupakan unsur paling umum di Bumi, yang membentuk sebagian besar inti luar dan dalam Bumi.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d6",
        "melt": "1811 K",
        "boil": "3134 K",
        "density": "7.874 g/cm\u00b3"
    },
    {
        "number": 27,
        "symbol": "Co",
        "name": "Cobalt",
        "mass": "58.9331944",
        "col": 9,
        "row": 4,
        "category": "transition-metal",
        "desc": "Cobalt adalah unsur kimia dengan simbol Co dan nomor atom 27. Seperti nikel, kobalt di kerak bumi hanya ditemukan dalam bentuk gabungan kimia, kecuali endapan kecil yang ditemukan pada paduan besi meteorik alami. Unsur bebas, yang dihasilkan melalui peleburan reduktif, adalah logam keras, berkilau, berwarna abu-abu keperakan.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d7",
        "melt": "1768 K",
        "boil": "3200 K",
        "density": "8.9 g/cm\u00b3"
    },
    {
        "number": 28,
        "symbol": "Ni",
        "name": "Nickel",
        "mass": "58.69344",
        "col": 10,
        "row": 4,
        "category": "transition-metal",
        "desc": "Nikel adalah unsur kimia dengan simbol Ni dan nomor atom 28. Nikel merupakan logam berkilau berwarna putih keperakan dengan sedikit semburat emas. Nikel termasuk dalam logam transisi dan bersifat keras serta ulet.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d8",
        "melt": "1728 K",
        "boil": "3003 K",
        "density": "8.908 g/cm\u00b3"
    },
    {
        "number": 29,
        "symbol": "Cu",
        "name": "Copper",
        "mass": "63.5463",
        "col": 11,
        "row": 4,
        "category": "transition-metal",
        "desc": "Tembaga adalah unsur kimia dengan simbol Cu (dari bahasa Latin: tembaga) dan nomor atom 29. Tembaga merupakan logam lunak, mudah dibentuk, dan ulet dengan konduktivitas termal dan listrik yang sangat tinggi. Permukaan tembaga murni yang baru terpapar memiliki warna oranye kemerahan.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s1 3d10",
        "melt": "1357.77 K",
        "boil": "2835 K",
        "density": "8.96 g/cm\u00b3"
    },
    {
        "number": 30,
        "symbol": "Zn",
        "name": "Zinc",
        "mass": "65.382",
        "col": 12,
        "row": 4,
        "category": "transition-metal",
        "desc": "Seng, dalam perdagangan juga spelter, adalah suatu unsur kimia dengan simbol Zn dan nomor atom 30. Seng adalah unsur pertama golongan 12 pada tabel periodik. Dalam beberapa hal seng secara kimiawi mirip dengan magnesium: ionnya berukuran sama dan satu-satunya bilangan oksidasi yang umum adalah +2.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10",
        "melt": "692.68 K",
        "boil": "1180 K",
        "density": "7.14 g/cm\u00b3"
    },
    {
        "number": 31,
        "symbol": "Ga",
        "name": "Gallium",
        "mass": "69.7231",
        "col": 13,
        "row": 4,
        "category": "transition-metal",
        "desc": "Gallium adalah unsur kimia dengan simbol Ga dan nomor atom 31. Unsur galium tidak terdapat dalam bentuk bebas di alam, tetapi sebagai senyawa galium(III) yang terdapat dalam jumlah kecil pada bijih seng dan bauksit. Gallium adalah logam lunak berwarna keperakan, dan unsur galium adalah padatan rapuh pada suhu rendah, dan meleleh pada suhu 29,76 \u00b0C (85,57 \u00b0F) (sedikit di atas suhu kamar).",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p1",
        "melt": "302.9146 K",
        "boil": "2673 K",
        "density": "5.91 g/cm\u00b3"
    },
    {
        "number": 32,
        "symbol": "Ge",
        "name": "Germanium",
        "mass": "72.6308",
        "col": 14,
        "row": 4,
        "category": "metalloid",
        "desc": "Germanium adalah unsur kimia dengan simbol Ge dan nomor atom 32. Merupakan metaloid putih keabu-abuan yang berkilau, keras, dalam gugus karbon, secara kimia mirip dengan tetangganya, timah dan silikon. Germanium yang dimurnikan adalah semikonduktor, dengan penampilan paling mirip dengan unsur silikon.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p2",
        "melt": "1211.4 K",
        "boil": "3106 K",
        "density": "5.323 g/cm\u00b3"
    },
    {
        "number": 33,
        "symbol": "As",
        "name": "Arsenic",
        "mass": "74.9215956",
        "col": 15,
        "row": 4,
        "category": "metalloid",
        "desc": "Arsenik adalah unsur kimia dengan simbol As dan nomor atom 33. Arsenik terdapat di banyak mineral, biasanya bersama dengan belerang dan logam, dan juga sebagai kristal unsur murni. Arsenik adalah metaloid.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p3",
        "melt": "Unknown",
        "boil": "Unknown",
        "density": "5.727 g/cm\u00b3"
    },
    {
        "number": 34,
        "symbol": "Se",
        "name": "Selenium",
        "mass": "78.9718",
        "col": 16,
        "row": 4,
        "category": "nonmetal",
        "desc": "Selenium adalah suatu unsur kimia dengan simbol Se dan nomor atom 34. Selenium merupakan unsur bukan logam yang sifat-sifatnya berada di antara sifat-sifat unsur kalkogen yang bersebelahan dengan kolom tabel periodik, belerang dan telurium. Jarang terjadi dalam bentuk unsur di alam, atau sebagai senyawa bijih murni.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p4",
        "melt": "494 K",
        "boil": "958 K",
        "density": "4.81 g/cm\u00b3"
    },
    {
        "number": 35,
        "symbol": "Br",
        "name": "Bromine",
        "mass": "79.904",
        "col": 17,
        "row": 4,
        "category": "nonmetal",
        "desc": "Brom (dari bahasa Yunani Kuno:\u03b2\u03c1\u1ff6\u03bc\u03bf\u03c2, br\u00f3mos, yang berarti \"bau busuk\") adalah suatu unsur kimia dengan simbol Br, dan nomor atom 35. Merupakan unsur halogen. Unsur ini diisolasi secara independen oleh dua ahli kimia, Carl Jacob L\u00f6wig dan Antoine Jerome Balard, pada tahun 1825\u20131826.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p5",
        "melt": "265.8 K",
        "boil": "332 K",
        "density": "3.1028 g/cm\u00b3"
    },
    {
        "number": 36,
        "symbol": "Kr",
        "name": "Krypton",
        "mass": "83.7982",
        "col": 18,
        "row": 4,
        "category": "noble-gas",
        "desc": "Kripton (dari bahasa Yunani:\u03ba\u03c1\u03c5\u03c0\u03c4\u03cc\u03c2 kryptos \"yang tersembunyi\") adalah suatu unsur kimia dengan simbol Kr dan nomor atom 36. Ia adalah anggota unsur golongan 18 (gas mulia). Sebuah gas mulia yang tidak berwarna, tidak berbau, dan tidak berasa, kripton terdapat dalam jumlah kecil di atmosfer, diisolasi dengan penyulingan fraksional udara cair, dan sering digunakan dengan gas langka lainnya dalam lampu neon.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6",
        "melt": "115.78 K",
        "boil": "119.93 K",
        "density": "3.749 g/cm\u00b3"
    },
    {
        "number": 37,
        "symbol": "Rb",
        "name": "Rubidium",
        "mass": "85.46783",
        "col": 1,
        "row": 5,
        "category": "alkali-metal",
        "desc": "Rubidium adalah suatu unsur kimia dengan lambang Rb dan nomor atom 37. Rubidium adalah unsur logam lunak berwarna putih keperakan dari golongan logam alkali, dengan massa atom 85,4678. Unsur rubidium sangat reaktif, dengan sifat yang mirip dengan logam alkali lainnya, seperti oksidasi yang sangat cepat di udara.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s1",
        "melt": "312.45 K",
        "boil": "961 K",
        "density": "1.532 g/cm\u00b3"
    },
    {
        "number": 38,
        "symbol": "Sr",
        "name": "Strontium",
        "mass": "87.621",
        "col": 2,
        "row": 5,
        "category": "alkaline-earth",
        "desc": "Strontium adalah suatu unsur kimia dengan lambang Sr dan nomor atom 38. Merupakan logam alkali tanah, strontium adalah unsur logam lunak berwarna putih keperakan atau kekuningan yang sangat reaktif secara kimia. Logam menjadi kuning ketika terkena udara.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2",
        "melt": "1050 K",
        "boil": "1650 K",
        "density": "2.64 g/cm\u00b3"
    },
    {
        "number": 39,
        "symbol": "Y",
        "name": "Yttrium",
        "mass": "88.905842",
        "col": 3,
        "row": 5,
        "category": "transition-metal",
        "desc": "Yttrium adalah unsur kimia dengan simbol Y dan nomor atom 39. Ini adalah logam transisi keperakan-logam yang secara kimia mirip dengan lantanida dan sering diklasifikasikan sebagai \"unsur tanah jarang\". Yttrium hampir selalu ditemukan dikombinasikan dengan lantanida dalam mineral tanah jarang dan tidak pernah ditemukan di alam sebagai unsur bebas.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d1",
        "melt": "1799 K",
        "boil": "3203 K",
        "density": "4.472 g/cm\u00b3"
    },
    {
        "number": 40,
        "symbol": "Zr",
        "name": "Zirconium",
        "mass": "91.2242",
        "col": 4,
        "row": 5,
        "category": "transition-metal",
        "desc": "Zirkonium adalah suatu unsur kimia dengan lambang Zr dan nomor atom 40. Nama zirkonium diambil dari nama mineral zirkon, sumber zirkonium terpenting. Kata zirkon berasal dari kata Persia zargun \u0632\u0631\u06af\u0648\u0646, yang berarti \"berwarna emas\".",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d2",
        "melt": "2128 K",
        "boil": "4650 K",
        "density": "6.52 g/cm\u00b3"
    },
    {
        "number": 41,
        "symbol": "Nb",
        "name": "Niobium",
        "mass": "92.906372",
        "col": 5,
        "row": 5,
        "category": "transition-metal",
        "desc": "Niobium, sebelumnya columbium, adalah suatu unsur kimia dengan simbol Nb (sebelumnya Cb) dan nomor atom 41. Merupakan logam transisi lunak, abu-abu, dan ulet, yang sering ditemukan dalam mineral piroklor, sumber komersial utama niobium, dan kolumbita. Nama tersebut berasal dari mitologi Yunani: Niobe, putri Tantalus karena sangat mirip dengan tantalum.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s1 4d4",
        "melt": "2750 K",
        "boil": "5017 K",
        "density": "8.57 g/cm\u00b3"
    },
    {
        "number": 42,
        "symbol": "Mo",
        "name": "Molybdenum",
        "mass": "95.951",
        "col": 6,
        "row": 5,
        "category": "transition-metal",
        "desc": "Molibdenum adalah suatu unsur kimia dengan simbol Mo dan nomor atom 42. Namanya berasal dari Neo-Latin molybdaenum, dari bahasa Yunani Kuno \u039c\u03cc\u03bb\u03c5\u03b2\u03b4\u03bf\u03c2 molybdos, yang berarti timbal, karena bijihnya disalahartikan sebagai bijih timah. Mineral molibdenum telah dikenal sepanjang sejarah, namun unsur tersebut ditemukan (dalam arti membedakannya sebagai entitas baru dari garam mineral logam lain) pada tahun 1778 oleh Carl Wilhelm Scheele.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s1 4d5",
        "melt": "2896 K",
        "boil": "4912 K",
        "density": "10.28 g/cm\u00b3"
    },
    {
        "number": 43,
        "symbol": "Tc",
        "name": "Technetium",
        "mass": "98",
        "col": 7,
        "row": 5,
        "category": "transition-metal",
        "desc": "Technetium (/t\u025bk\u02c8ni\u02d0\u0283i\u0259m/) adalah suatu unsur kimia dengan simbol Tc dan nomor atom 43. Ini adalah unsur dengan nomor atom terendah dalam tabel periodik yang tidak memiliki isotop stabil: setiap bentuknya bersifat radioaktif. Hampir semua teknesium diproduksi secara sintetis, dan hanya dalam jumlah kecil yang ditemukan di alam.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d5",
        "melt": "2430 K",
        "boil": "4538 K",
        "density": "11 g/cm\u00b3"
    },
    {
        "number": 44,
        "symbol": "Ru",
        "name": "Ruthenium",
        "mass": "101.072",
        "col": 8,
        "row": 5,
        "category": "transition-metal",
        "desc": "Rutenium adalah unsur kimia dengan simbol Ru dan nomor atom 44. Ini adalah logam transisi langka yang termasuk dalam kelompok platina pada tabel periodik. Seperti logam lain dari kelompok platina, rutenium bersifat inert terhadap sebagian besar bahan kimia lainnya.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s1 4d7",
        "melt": "2607 K",
        "boil": "4423 K",
        "density": "12.45 g/cm\u00b3"
    },
    {
        "number": 45,
        "symbol": "Rh",
        "name": "Rhodium",
        "mass": "102.905502",
        "col": 9,
        "row": 5,
        "category": "transition-metal",
        "desc": "Rhodium adalah unsur kimia dengan simbol Rh dan nomor atom 45. Merupakan logam transisi langka, berwarna putih keperakan, keras, dan inert secara kimia. Ini adalah anggota grup platinum.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s1 4d8",
        "melt": "2237 K",
        "boil": "3968 K",
        "density": "12.41 g/cm\u00b3"
    },
    {
        "number": 46,
        "symbol": "Pd",
        "name": "Palladium",
        "mass": "106.421",
        "col": 10,
        "row": 5,
        "category": "transition-metal",
        "desc": "Paladium adalah unsur kimia dengan simbol Pd dan nomor atom 46. Merupakan logam putih keperakan langka dan berkilau yang ditemukan pada tahun 1803 oleh William Hyde Wollaston. Dia menamainya setelah asteroid Pallas, yang diambil dari julukan dewi Yunani Athena, yang diperolehnya saat dia membunuh Pallas.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 4d10",
        "melt": "1828.05 K",
        "boil": "3236 K",
        "density": "12.023 g/cm\u00b3"
    },
    {
        "number": 47,
        "symbol": "Ag",
        "name": "Silver",
        "mass": "107.86822",
        "col": 11,
        "row": 5,
        "category": "transition-metal",
        "desc": "Perak adalah suatu unsur kimia dengan simbol Ag (Yunani:\u03ac\u03c1\u03b3\u03c5\u03c1\u03bf\u03c2 \u00e1rguros, Latin:argentum, berasal dari akar bahasa Indo-Eropa *h\u2082er\u01f5- untuk \"abu-abu\" atau \"bersinar\") dan nomor atom 47. Merupakan logam transisi lunak, putih, berkilau, ia memiliki konduktivitas listrik, konduktivitas termal, dan reflektifitas tertinggi dibandingkan logam mana pun. Logam ini terdapat secara alami dalam bentuknya yang murni dan bebas (perak asli), sebagai paduan dengan emas dan logam lainnya, dan dalam mineral seperti argentit dan klorargyrit.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s1 4d10",
        "melt": "1234.93 K",
        "boil": "2435 K",
        "density": "10.49 g/cm\u00b3"
    },
    {
        "number": 48,
        "symbol": "Cd",
        "name": "Cadmium",
        "mass": "112.4144",
        "col": 12,
        "row": 5,
        "category": "transition-metal",
        "desc": "Kadmium adalah suatu unsur kimia dengan lambang Cd dan nomor atom 48. Logam lunak berwarna putih kebiruan ini secara kimiawi mirip dengan dua logam stabil lainnya pada golongan 12, seng dan merkuri. Seperti seng, ia lebih menyukai bilangan oksidasi +2 di sebagian besar senyawanya dan seperti merkuri, ia menunjukkan titik leleh yang rendah dibandingkan dengan logam transisi.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10",
        "melt": "594.22 K",
        "boil": "1040 K",
        "density": "8.65 g/cm\u00b3"
    },
    {
        "number": 49,
        "symbol": "In",
        "name": "Indium",
        "mass": "114.8181",
        "col": 13,
        "row": 5,
        "category": "transition-metal",
        "desc": "Indium adalah suatu unsur kimia dengan lambang In dan nomor atom 49. Merupakan unsur logam pasca transisi yang jarang ditemukan di kerak bumi. Logam ini sangat lunak, mudah ditempa, dan mudah melebur, dengan titik leleh lebih tinggi dari natrium, tetapi lebih rendah dari litium atau timah.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p1",
        "melt": "429.7485 K",
        "boil": "2345 K",
        "density": "7.31 g/cm\u00b3"
    },
    {
        "number": 50,
        "symbol": "Sn",
        "name": "Tin",
        "mass": "118.7107",
        "col": 14,
        "row": 5,
        "category": "transition-metal",
        "desc": "Timah adalah suatu unsur kimia dengan lambang Sn (bahasa Latin:stannum) dan nomor atom 50. Timah merupakan logam golongan utama pada golongan 14 tabel periodik. Timah menunjukkan kemiripan kimia dengan unsur tetangganya golongan-14, germanium dan timbal, dan memiliki dua kemungkinan bilangan oksidasi, +2 dan +4 yang sedikit lebih stabil.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p2",
        "melt": "505.08 K",
        "boil": "2875 K",
        "density": "7.365 g/cm\u00b3"
    },
    {
        "number": 51,
        "symbol": "Sb",
        "name": "Antimony",
        "mass": "121.7601",
        "col": 15,
        "row": 5,
        "category": "metalloid",
        "desc": "Antimon adalah unsur kimia dengan simbol Sb (dari bahasa Latin:stibium) dan nomor atom 51. Merupakan metaloid abu-abu berkilau, ditemukan di alam terutama sebagai mineral sulfida stibnite (Sb2S3). Senyawa antimon telah dikenal sejak zaman dahulu dan digunakan untuk kosmetik; antimon logam juga diketahui, namun secara keliru diidentifikasi sebagai timbal pada penemuannya.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p3",
        "melt": "903.78 K",
        "boil": "1908 K",
        "density": "6.697 g/cm\u00b3"
    },
    {
        "number": 52,
        "symbol": "Te",
        "name": "Tellurium",
        "mass": "127.603",
        "col": 16,
        "row": 5,
        "category": "metalloid",
        "desc": "Telurium adalah unsur kimia dengan simbol Te dan nomor atom 52. Merupakan metaloid putih keperakan yang rapuh, agak beracun, langka. Telurium secara kimia berhubungan dengan selenium dan belerang.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p4",
        "melt": "722.66 K",
        "boil": "1261 K",
        "density": "6.24 g/cm\u00b3"
    },
    {
        "number": 53,
        "symbol": "I",
        "name": "Iodine",
        "mass": "126.904473",
        "col": 17,
        "row": 5,
        "category": "nonmetal",
        "desc": "Yodium adalah suatu unsur kimia dengan lambang I dan nomor atom 53. Namanya berasal dari bahasa Yunani \u1f30\u03bf\u03b5\u03b9\u03b4\u03ae\u03c2 ioeid\u0113s, artinya ungu atau ungu, karena warna uap yodium. Yodium dan senyawanya terutama digunakan dalam nutrisi, dan industri dalam produksi asam asetat dan polimer tertentu.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p5",
        "melt": "386.85 K",
        "boil": "457.4 K",
        "density": "4.933 g/cm\u00b3"
    },
    {
        "number": 54,
        "symbol": "Xe",
        "name": "Xenon",
        "mass": "131.2936",
        "col": 18,
        "row": 5,
        "category": "noble-gas",
        "desc": "Xenon adalah unsur kimia dengan simbol Xe dan nomor atom 54. Ini adalah gas mulia yang tidak berwarna, padat, dan tidak berbau, yang terdapat di atmosfer bumi dalam jumlah kecil. Meskipun umumnya tidak reaktif, xenon dapat mengalami beberapa reaksi kimia seperti pembentukan xenon hexafluoroplatinate, senyawa gas mulia pertama yang disintesis.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6",
        "melt": "161.4 K",
        "boil": "165.051 K",
        "density": "5.894 g/cm\u00b3"
    },
    {
        "number": 55,
        "symbol": "Cs",
        "name": "Cesium",
        "mass": "132.905451966",
        "col": 1,
        "row": 6,
        "category": "alkali-metal",
        "desc": "Cesium atau cesium adalah unsur kimia dengan simbol Cs dan nomor atom 55. Ini adalah logam alkali lunak berwarna emas keperakan dengan titik leleh 28 \u00b0C (82 \u00b0F), yang menjadikannya salah satu dari hanya lima unsur logam yang berbentuk cair pada atau mendekati suhu kamar. Cesium merupakan logam alkali dan memiliki sifat fisik dan kimia yang mirip dengan rubidium dan kalium.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s1",
        "melt": "301.7 K",
        "boil": "944 K",
        "density": "1.93 g/cm\u00b3"
    },
    {
        "number": 56,
        "symbol": "Ba",
        "name": "Barium",
        "mass": "137.3277",
        "col": 2,
        "row": 6,
        "category": "alkaline-earth",
        "desc": "Barium adalah unsur kimia dengan simbol Ba dan nomor atom 56. Ini adalah unsur kelima dalam Golongan 2, logam alkali tanah lunak berwarna keperakan. Karena reaktivitas kimianya yang tinggi, barium tidak pernah ditemukan di alam sebagai unsur bebas.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2",
        "melt": "1000 K",
        "boil": "2118 K",
        "density": "3.51 g/cm\u00b3"
    },
    {
        "number": 57,
        "symbol": "La",
        "name": "Lanthanum",
        "mass": "138.905477",
        "col": 3,
        "row": 9,
        "category": "lanthanide",
        "desc": "Lantanum adalah unsur kimia metalik berwarna putih keperakan yang lembut, ulet, dengan simbol La dan nomor atom 57. Lantanum cepat memudar jika terkena udara dan cukup lunak untuk dipotong dengan pisau. Ia memberi namanya pada deret lantanida, sekelompok 15 unsur serupa antara lantanum dan lutetium dalam tabel periodik: ia juga kadang-kadang dianggap sebagai unsur pertama dari logam transisi periode ke-6.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 5d1",
        "melt": "1193 K",
        "boil": "3737 K",
        "density": "6.162 g/cm\u00b3"
    },
    {
        "number": 58,
        "symbol": "Ce",
        "name": "Cerium",
        "mass": "140.1161",
        "col": 4,
        "row": 9,
        "category": "lanthanide",
        "desc": "Cerium adalah suatu unsur kimia dengan lambang Ce dan nomor atom 58. Cerium merupakan logam lunak, berwarna keperakan, ulet yang mudah teroksidasi di udara. Nama Cerium diambil dari nama planet kerdil Ceres (namanya diambil dari nama dewi pertanian Romawi).",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 5d1 4f1",
        "melt": "1068 K",
        "boil": "3716 K",
        "density": "6.77 g/cm\u00b3"
    },
    {
        "number": 59,
        "symbol": "Pr",
        "name": "Praseodymium",
        "mass": "140.907662",
        "col": 5,
        "row": 9,
        "category": "lanthanide",
        "desc": "Praseodymium adalah suatu unsur kimia dengan lambang Pr dan nomor atom 59. Praseodymium adalah logam lunak, berwarna keperakan, mudah dibentuk, dan ulet dalam golongan lantanida. Ia dihargai karena sifat magnetik, listrik, kimia, dan optiknya.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f3",
        "melt": "1208 K",
        "boil": "3403 K",
        "density": "6.77 g/cm\u00b3"
    },
    {
        "number": 60,
        "symbol": "Nd",
        "name": "Neodymium",
        "mass": "144.2423",
        "col": 6,
        "row": 9,
        "category": "lanthanide",
        "desc": "Neodymium adalah unsur kimia dengan simbol Nd dan nomor atom 60. Merupakan logam lunak berwarna keperakan yang mudah ternoda di udara. Neodymium ditemukan pada tahun 1885 oleh ahli kimia Austria Carl Auer von Welsbach.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f4",
        "melt": "1297 K",
        "boil": "3347 K",
        "density": "7.01 g/cm\u00b3"
    },
    {
        "number": 61,
        "symbol": "Pm",
        "name": "Promethium",
        "mass": "145",
        "col": 7,
        "row": 9,
        "category": "lanthanide",
        "desc": "Promethium, aslinya prometheum, adalah suatu unsur kimia dengan simbol Pm dan nomor atom 61. Semua isotopnya bersifat radioaktif; ia adalah salah satu dari hanya dua unsur yang dalam tabel periodik diikuti oleh unsur-unsur dengan bentuk stabil, perbedaan yang sama dengan teknesium. Secara kimia, prometium adalah lantanida, yang membentuk garam jika digabungkan dengan unsur lain.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f5",
        "melt": "1315 K",
        "boil": "3273 K",
        "density": "7.26 g/cm\u00b3"
    },
    {
        "number": 62,
        "symbol": "Sm",
        "name": "Samarium",
        "mass": "150.362",
        "col": 8,
        "row": 9,
        "category": "lanthanide",
        "desc": "Samarium adalah suatu unsur kimia dengan simbol Sm dan nomor atom 62. Merupakan logam keperakan agak keras yang mudah teroksidasi di udara. Menjadi anggota khas deret lantanida, samarium biasanya mengasumsikan bilangan oksidasi +3.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f6",
        "melt": "1345 K",
        "boil": "2173 K",
        "density": "7.52 g/cm\u00b3"
    },
    {
        "number": 63,
        "symbol": "Eu",
        "name": "Europium",
        "mass": "151.9641",
        "col": 9,
        "row": 9,
        "category": "lanthanide",
        "desc": "Europium adalah suatu unsur kimia dengan simbol Eu dan nomor atom 63. Ia diisolasi pada tahun 1901 dan dinamai menurut benua Eropa. Ini adalah logam keperakan yang cukup keras dan mudah teroksidasi di udara dan air.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f7",
        "melt": "1099 K",
        "boil": "1802 K",
        "density": "5.264 g/cm\u00b3"
    },
    {
        "number": 64,
        "symbol": "Gd",
        "name": "Gadolinium",
        "mass": "157.253",
        "col": 10,
        "row": 9,
        "category": "lanthanide",
        "desc": "Gadolinium adalah unsur kimia dengan simbol Gd dan nomor atom 64. Merupakan logam tanah jarang berwarna putih keperakan, mudah dibentuk, dan ulet. Itu ditemukan di alam hanya dalam bentuk gabungan (garam).",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f7 5d1",
        "melt": "1585 K",
        "boil": "3273 K",
        "density": "7.9 g/cm\u00b3"
    },
    {
        "number": 65,
        "symbol": "Tb",
        "name": "Terbium",
        "mass": "158.925352",
        "col": 11,
        "row": 9,
        "category": "lanthanide",
        "desc": "Terbium adalah suatu unsur kimia dengan lambang Tb dan nomor atom 65. Merupakan logam tanah jarang berwarna putih keperakan yang mudah dibentuk, ulet, dan cukup lunak untuk dipotong dengan pisau. Terbium tidak pernah ditemukan di alam sebagai unsur bebas, namun terkandung dalam banyak mineral, termasuk cerite, gadolinit, monasit, xenotime, dan euxenite.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f9",
        "melt": "1629 K",
        "boil": "3396 K",
        "density": "8.23 g/cm\u00b3"
    },
    {
        "number": 66,
        "symbol": "Dy",
        "name": "Dysprosium",
        "mass": "162.5001",
        "col": 12,
        "row": 9,
        "category": "lanthanide",
        "desc": "Disprosium adalah suatu unsur kimia dengan lambang Dy dan nomor atom 66. Merupakan unsur tanah jarang dengan kilau perak metalik. Disprosium tidak pernah ditemukan di alam sebagai unsur bebas, meskipun ditemukan dalam berbagai mineral, seperti xenotime.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f10",
        "melt": "1680 K",
        "boil": "2840 K",
        "density": "8.54 g/cm\u00b3"
    },
    {
        "number": 67,
        "symbol": "Ho",
        "name": "Holmium",
        "mass": "164.930332",
        "col": 13,
        "row": 9,
        "category": "lanthanide",
        "desc": "Holmium adalah suatu unsur kimia dengan lambang Ho dan nomor atom 67. Bagian dari deret lantanida, holmium merupakan unsur tanah jarang. Holmium ditemukan oleh ahli kimia Swedia Per Theodor Cleve.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f11",
        "melt": "1734 K",
        "boil": "2873 K",
        "density": "8.79 g/cm\u00b3"
    },
    {
        "number": 68,
        "symbol": "Er",
        "name": "Erbium",
        "mass": "167.2593",
        "col": 14,
        "row": 9,
        "category": "lanthanide",
        "desc": "Erbium adalah unsur kimia dalam deret lantanida, dengan lambang Er dan nomor atom 68. Merupakan logam padat berwarna putih keperakan jika diisolasi secara buatan, erbium alami selalu ditemukan dalam kombinasi kimia dengan unsur lain di Bumi. Dengan demikian, ini adalah unsur tanah jarang yang berasosiasi dengan beberapa unsur langka lainnya dalam mineral gadolinit dari Ytterby di Swedia, tempat ditemukannya yttrium, ytterbium, dan terbium.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f12",
        "melt": "1802 K",
        "boil": "3141 K",
        "density": "9.066 g/cm\u00b3"
    },
    {
        "number": 69,
        "symbol": "Tm",
        "name": "Thulium",
        "mass": "168.934222",
        "col": 15,
        "row": 9,
        "category": "lanthanide",
        "desc": "Thulium adalah unsur kimia dengan simbol Tm dan nomor atom 69. Merupakan unsur ketiga belas dan antepenultimate (ketiga terakhir) dalam deret lantanida. Seperti lantanida lainnya, bilangan oksidasi yang paling umum adalah +3, terlihat pada oksida, halida, dan senyawa lainnya.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f13",
        "melt": "1818 K",
        "boil": "2223 K",
        "density": "9.32 g/cm\u00b3"
    },
    {
        "number": 70,
        "symbol": "Yb",
        "name": "Ytterbium",
        "mass": "173.0451",
        "col": 16,
        "row": 9,
        "category": "lanthanide",
        "desc": "Ytterbium adalah unsur kimia dengan simbol Yb dan nomor atom 70. Ini adalah unsur keempat belas dan kedua dari belakang dalam deret lantanida, yang merupakan dasar dari stabilitas relatif bilangan oksidasi +2. Namun, seperti lantanida lainnya, bilangan oksidasi yang paling umum adalah +3, terlihat pada oksida, halida, dan senyawa lainnya.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14",
        "melt": "1097 K",
        "boil": "1469 K",
        "density": "6.9 g/cm\u00b3"
    },
    {
        "number": 71,
        "symbol": "Lu",
        "name": "Lutetium",
        "mass": "174.96681",
        "col": 17,
        "row": 9,
        "category": "lanthanide",
        "desc": "Lutetium adalah unsur kimia dengan simbol Lu dan nomor atom 71. Merupakan logam berwarna putih keperakan, tahan korosi di udara kering, tetapi tidak di udara lembab. Ia dianggap sebagai unsur pertama dari logam transisi periode ke-6 dan unsur terakhir dalam deret lantanida, dan secara tradisional termasuk di antara tanah jarang.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d1",
        "melt": "1925 K",
        "boil": "3675 K",
        "density": "9.841 g/cm\u00b3"
    },
    {
        "number": 72,
        "symbol": "Hf",
        "name": "Hafnium",
        "mass": "178.492",
        "col": 4,
        "row": 6,
        "category": "transition-metal",
        "desc": "Hafnium adalah unsur kimia dengan simbol Hf dan nomor atom 72. Merupakan logam transisi tetravalen berwarna abu-abu keperakan, hafnium secara kimia menyerupai zirkonium dan ditemukan dalam mineral zirkonium. Keberadaannya telah diprediksi oleh Dmitri Mendeleev pada tahun 1869, meskipun ia baru teridentifikasi pada tahun 1923, menjadikannya unsur stabil kedua dari belakang yang ditemukan (renium diidentifikasi dua tahun kemudian).",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d2",
        "melt": "2506 K",
        "boil": "4876 K",
        "density": "13.31 g/cm\u00b3"
    },
    {
        "number": 73,
        "symbol": "Ta",
        "name": "Tantalum",
        "mass": "180.947882",
        "col": 5,
        "row": 6,
        "category": "transition-metal",
        "desc": "Tantalum adalah suatu unsur kimia dengan lambang Ta dan nomor atom 73. Sebelumnya dikenal dengan nama tantalium, namanya berasal dari Tantalus, seorang antihero dari mitologi Yunani. Tantalum adalah logam transisi langka, keras, biru keabu-abuan, berkilau dan sangat tahan korosi.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d3",
        "melt": "3290 K",
        "boil": "5731 K",
        "density": "16.69 g/cm\u00b3"
    },
    {
        "number": 74,
        "symbol": "W",
        "name": "Tungsten",
        "mass": "183.841",
        "col": 6,
        "row": 6,
        "category": "transition-metal",
        "desc": "Tungsten, juga dikenal sebagai wolfram, adalah suatu unsur kimia dengan simbol W dan nomor atom 74. Kata tungsten berasal dari bahasa Swedia tung sten, yang artinya batu berat. Namanya dalam bahasa Swedia adalah volfram, namun untuk membedakannya dari scheelite, yang dalam bahasa Swedia disebut tungsten.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d4",
        "melt": "3695 K",
        "boil": "6203 K",
        "density": "19.25 g/cm\u00b3"
    },
    {
        "number": 75,
        "symbol": "Re",
        "name": "Rhenium",
        "mass": "186.2071",
        "col": 7,
        "row": 6,
        "category": "transition-metal",
        "desc": "Renium adalah unsur kimia dengan simbol Re dan nomor atom 75. Merupakan logam transisi baris ketiga berwarna putih keperakan, berat, dalam golongan 7 tabel periodik. Dengan perkiraan konsentrasi rata-rata 1 bagian per miliar (ppb), renium merupakan salah satu unsur paling langka di kerak bumi.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d5",
        "melt": "3459 K",
        "boil": "5869 K",
        "density": "21.02 g/cm\u00b3"
    },
    {
        "number": 76,
        "symbol": "Os",
        "name": "Osmium",
        "mass": "190.233",
        "col": 8,
        "row": 6,
        "category": "transition-metal",
        "desc": "Osmium (dari bahasa Yunani osme (\u1f40\u03c3\u03bc\u03ae) yang berarti \"bau\") adalah suatu unsur kimia dengan simbol Os dan nomor atom 76. Osmium adalah logam transisi yang keras, rapuh, berwarna putih kebiruan dalam golongan platina yang ditemukan sebagai unsur jejak dalam paduan, sebagian besar dalam bijih platina. Osmium adalah unsur alami terpadat, dengan massa jenis 22,59 g/cm3.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d6",
        "melt": "3306 K",
        "boil": "5285 K",
        "density": "22.59 g/cm\u00b3"
    },
    {
        "number": 77,
        "symbol": "Ir",
        "name": "Iridium",
        "mass": "192.2173",
        "col": 9,
        "row": 6,
        "category": "transition-metal",
        "desc": "Iridium adalah suatu unsur kimia dengan simbol Ir dan nomor atom 77. Merupakan logam transisi yang sangat keras, rapuh, berwarna putih keperakan dari golongan platina, iridium umumnya dianggap sebagai unsur terpadat kedua (setelah osmium) berdasarkan massa jenis yang diukur, meskipun perhitungan yang melibatkan kisi ruang unsur-unsur tersebut menunjukkan bahwa iridium lebih padat. Ini juga merupakan logam yang paling tahan korosi, bahkan pada suhu setinggi 2000 \u00b0C. Meskipun hanya garam cair dan halogen tertentu yang bersifat korosif terhadap iridium padat, debu iridium yang terbagi halus jauh lebih reaktif dan mudah terbakar.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d7",
        "melt": "2719 K",
        "boil": "4403 K",
        "density": "22.56 g/cm\u00b3"
    },
    {
        "number": 78,
        "symbol": "Pt",
        "name": "Platinum",
        "mass": "195.0849",
        "col": 10,
        "row": 6,
        "category": "transition-metal",
        "desc": "Platinum adalah unsur kimia dengan simbol Pt dan nomor atom 78. Platinum merupakan logam transisi padat, mudah dibentuk, ulet, sangat tidak reaktif, berharga, berwarna putih abu-abu. Namanya berasal dari istilah Spanyol platina, yang secara harfiah diterjemahkan menjadi \"perak kecil\".",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s1 4f14 5d9",
        "melt": "2041.4 K",
        "boil": "4098 K",
        "density": "21.45 g/cm\u00b3"
    },
    {
        "number": 79,
        "symbol": "Au",
        "name": "Gold",
        "mass": "196.9665695",
        "col": 11,
        "row": 6,
        "category": "transition-metal",
        "desc": "Emas adalah suatu unsur kimia dengan simbol Au (dari bahasa Latin:aurum) dan nomor atom 79. Dalam bentuknya yang paling murni, emas merupakan logam berwarna kuning cerah, agak kemerahan, padat, lunak, mudah dibentuk, dan ulet. Secara kimia, emas merupakan logam transisi dan unsur golongan 11.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s1 4f14 5d10",
        "melt": "1337.33 K",
        "boil": "3243 K",
        "density": "19.3 g/cm\u00b3"
    },
    {
        "number": 80,
        "symbol": "Hg",
        "name": "Mercury",
        "mass": "200.5923",
        "col": 12,
        "row": 6,
        "category": "transition-metal",
        "desc": "Merkuri adalah suatu unsur kimia dengan lambang Hg dan nomor atom 80. Umumnya dikenal dengan nama air raksa dan sebelumnya bernama hydrargyrum (/ha\u026a\u02c8dr\u0251\u02d0rd\u0292\u0259r\u0259m/). Sebagai unsur blok d yang berat dan berwarna keperakan, merkuri adalah satu-satunya unsur logam yang berbentuk cair pada kondisi suhu dan tekanan standar; satu-satunya unsur lain yang berbentuk cair pada kondisi ini adalah brom, meskipun logam seperti sesium, galium, dan rubidium meleleh tepat di atas suhu kamar.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10",
        "melt": "234.321 K",
        "boil": "629.88 K",
        "density": "13.534 g/cm\u00b3"
    },
    {
        "number": 81,
        "symbol": "Tl",
        "name": "Thallium",
        "mass": "204.38",
        "col": 13,
        "row": 6,
        "category": "transition-metal",
        "desc": "Talium adalah unsur kimia dengan simbol Tl dan nomor atom 81. Logam pasca transisi berwarna abu-abu lembut ini tidak ditemukan bebas di alam. Jika diisolasi, bentuknya menyerupai timah, namun berubah warna jika terkena udara.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p1",
        "melt": "577 K",
        "boil": "1746 K",
        "density": "11.85 g/cm\u00b3"
    },
    {
        "number": 82,
        "symbol": "Pb",
        "name": "Lead",
        "mass": "207.21",
        "col": 14,
        "row": 6,
        "category": "transition-metal",
        "desc": "Timbal (/l\u025bd/) adalah suatu unsur kimia dalam golongan karbon dengan lambang Pb (dari bahasa Latin:plumbum) dan nomor atom 82. Timbal merupakan logam pasca transisi yang lunak, mudah dibentuk, dan berat. Timbal metalik memiliki warna putih kebiruan setelah baru dipotong, namun segera memudar menjadi warna keabu-abuan kusam jika terkena udara.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p2",
        "melt": "600.61 K",
        "boil": "2022 K",
        "density": "11.34 g/cm\u00b3"
    },
    {
        "number": 83,
        "symbol": "Bi",
        "name": "Bismuth",
        "mass": "208.980401",
        "col": 15,
        "row": 6,
        "category": "transition-metal",
        "desc": "Bismut adalah suatu unsur kimia dengan lambang Bi dan nomor atom 83. Bismut, suatu logam pasca transisi pentavalen, secara kimia menyerupai arsenik dan antimon. Unsur bismut dapat terbentuk secara alami, meskipun sulfida dan oksidanya membentuk bijih komersial yang penting.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p3",
        "melt": "544.7 K",
        "boil": "1837 K",
        "density": "9.78 g/cm\u00b3"
    },
    {
        "number": 84,
        "symbol": "Po",
        "name": "Polonium",
        "mass": "209",
        "col": 16,
        "row": 6,
        "category": "transition-metal",
        "desc": "Polonium adalah unsur kimia dengan simbol Po dan nomor atom 84, ditemukan pada tahun 1898 oleh Marie Curie dan Pierre Curie. Unsur langka dan sangat radioaktif tanpa isotop stabil, polonium secara kimia mirip dengan bismut dan telurium, dan terdapat pada bijih uranium. Penerapan polonium sedikit.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p4",
        "melt": "527 K",
        "boil": "1235 K",
        "density": "9.196 g/cm\u00b3"
    },
    {
        "number": 85,
        "symbol": "At",
        "name": "Astatine",
        "mass": "210",
        "col": 17,
        "row": 6,
        "category": "metalloid",
        "desc": "Astatin adalah unsur kimia radioaktif yang sangat langka dengan simbol kimia At dan nomor atom 85. Astatin terdapat di Bumi sebagai produk peluruhan berbagai unsur yang lebih berat. Semua isotopnya berumur pendek; yang paling stabil adalah astatin-210, dengan waktu paruh 8,1 jam.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p5",
        "melt": "575 K",
        "boil": "610 K",
        "density": "6.35 g/cm\u00b3"
    },
    {
        "number": 86,
        "symbol": "Rn",
        "name": "Radon",
        "mass": "222",
        "col": 18,
        "row": 6,
        "category": "noble-gas",
        "desc": "Radon adalah unsur kimia dengan simbol Rn dan nomor atom 86. Radon adalah gas mulia radioaktif, tidak berwarna, tidak berbau, tidak berasa, terjadi secara alami sebagai produk peluruhan radium. Isotopnya yang paling stabil, 222Rn, mempunyai waktu paruh 3,8 hari.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6",
        "melt": "202 K",
        "boil": "211.5 K",
        "density": "9.73 g/cm\u00b3"
    },
    {
        "number": 87,
        "symbol": "Fr",
        "name": "Francium",
        "mass": "223",
        "col": 1,
        "row": 7,
        "category": "alkali-metal",
        "desc": "Fransium adalah unsur kimia dengan simbol Fr dan nomor atom 87. Dulunya dikenal sebagai eka-cesium dan aktinium K. Ini adalah unsur elektronegatif terkecil kedua, setelah sesium. Fransium adalah logam sangat radioaktif yang terurai menjadi astatin, radium, dan radon.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s1",
        "melt": "300 K",
        "boil": "950 K",
        "density": "1.87 g/cm\u00b3"
    },
    {
        "number": 88,
        "symbol": "Ra",
        "name": "Radium",
        "mass": "226",
        "col": 2,
        "row": 7,
        "category": "alkaline-earth",
        "desc": "Radium adalah suatu unsur kimia dengan lambang Ra dan nomor atom 88. Merupakan unsur keenam dalam golongan 2 tabel periodik, juga dikenal sebagai logam alkali tanah. Radium murni hampir tidak berwarna, namun mudah bergabung dengan nitrogen (bukan oksigen) jika terkena udara, membentuk lapisan permukaan hitam radium nitrida (Ra3N2).",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2",
        "melt": "1233 K",
        "boil": "2010 K",
        "density": "5.5 g/cm\u00b3"
    },
    {
        "number": 89,
        "symbol": "Ac",
        "name": "Actinium",
        "mass": "227",
        "col": 3,
        "row": 10,
        "category": "actinide",
        "desc": "Aktinium adalah unsur kimia radioaktif dengan simbol Ac (jangan bingung dengan singkatan gugus asetil) dan nomor atom 89, yang ditemukan pada tahun 1899. Ini adalah unsur radioaktif non-primordial pertama yang diisolasi. Polonium, radium dan radon diamati sebelum aktinium, tetapi mereka tidak diisolasi sampai tahun 1902.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 6d1",
        "melt": "1500 K",
        "boil": "3500 K",
        "density": "10 g/cm\u00b3"
    },
    {
        "number": 90,
        "symbol": "Th",
        "name": "Thorium",
        "mass": "232.03774",
        "col": 4,
        "row": 10,
        "category": "actinide",
        "desc": "Torium adalah suatu unsur kimia dengan simbol Th dan nomor atom 90. Merupakan logam aktinida radioaktif, torium adalah salah satu dari hanya dua unsur radioaktif signifikan yang masih terdapat secara alami dalam jumlah besar sebagai unsur primordial (yang lainnya adalah uranium). Ditemukan pada tahun 1828 oleh Pendeta Norwegia dan ahli mineralogi amatir Morten Thrane Esmark dan diidentifikasi oleh ahli kimia Swedia J\u00f6ns Jakob Berzelius, yang menamainya dengan nama Thor, dewa guntur Norse.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 6d2",
        "melt": "2023 K",
        "boil": "5061 K",
        "density": "11.724 g/cm\u00b3"
    },
    {
        "number": 91,
        "symbol": "Pa",
        "name": "Protactinium",
        "mass": "231.035882",
        "col": 5,
        "row": 10,
        "category": "actinide",
        "desc": "Protaktinium adalah unsur kimia dengan simbol Pa dan nomor atom 91. Merupakan logam padat berwarna abu-abu keperakan yang mudah bereaksi dengan oksigen, uap air, dan asam anorganik. Ia membentuk berbagai senyawa kimia di mana protaktinium biasanya terdapat dalam bilangan oksidasi +5, tetapi juga dapat mengambil bilangan +4 dan bahkan +2 atau +3.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f2 6d1",
        "melt": "1841 K",
        "boil": "4300 K",
        "density": "15.37 g/cm\u00b3"
    },
    {
        "number": 92,
        "symbol": "U",
        "name": "Uranium",
        "mass": "238.028913",
        "col": 6,
        "row": 10,
        "category": "actinide",
        "desc": "Uranium adalah suatu unsur kimia dengan simbol U dan nomor atom 92. Merupakan logam berwarna putih keperakan dalam deret aktinida pada tabel periodik. Sebuah atom uranium memiliki 92 proton dan 92 elektron, 6 di antaranya adalah elektron valensi.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f3 6d1",
        "melt": "1405.3 K",
        "boil": "4404 K",
        "density": "19.1 g/cm\u00b3"
    },
    {
        "number": 93,
        "symbol": "Np",
        "name": "Neptunium",
        "mass": "237",
        "col": 7,
        "row": 10,
        "category": "actinide",
        "desc": "Neptunium adalah suatu unsur kimia dengan simbol Np dan nomor atom 93. Merupakan logam aktinida radioaktif, neptunium adalah unsur transuranik pertama. Posisinya dalam tabel periodik tepat setelah uranium, dinamai menurut nama planet Uranus, menyebabkan ia dinamai menurut Neptunus, planet berikutnya setelah Uranus.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f4 6d1",
        "melt": "912 K",
        "boil": "4447 K",
        "density": "20.45 g/cm\u00b3"
    },
    {
        "number": 94,
        "symbol": "Pu",
        "name": "Plutonium",
        "mass": "244",
        "col": 8,
        "row": 10,
        "category": "actinide",
        "desc": "Plutonium adalah unsur kimia radioaktif transuranik dengan lambang Pu dan nomor atom 94. Merupakan logam aktinida berwarna abu-abu keperakan yang memudar bila terkena udara, dan membentuk lapisan kusam bila teroksidasi. Unsur ini biasanya menunjukkan enam alotrop dan empat bilangan oksidasi.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f6",
        "melt": "912.5 K",
        "boil": "3505 K",
        "density": "19.816 g/cm\u00b3"
    },
    {
        "number": 95,
        "symbol": "Am",
        "name": "Americium",
        "mass": "243",
        "col": 9,
        "row": 10,
        "category": "actinide",
        "desc": "Amerisium adalah unsur kimia transuranium radioaktif dengan simbol Am dan nomor atom 95. Anggota deret aktinida ini terletak dalam tabel periodik di bawah unsur lantanida europium, dan dengan analogi dinamai menurut nama Amerika. Americium pertama kali diproduksi pada tahun 1944 oleh kelompok Glenn T.Seaborg dari Berkeley, California, di laboratorium metalurgi Universitas Chicago.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f7",
        "melt": "1449 K",
        "boil": "2880 K",
        "density": "12 g/cm\u00b3"
    },
    {
        "number": 96,
        "symbol": "Cm",
        "name": "Curium",
        "mass": "247",
        "col": 10,
        "row": 10,
        "category": "actinide",
        "desc": "Curium adalah unsur kimia radioaktif transuranik dengan simbol Cm dan nomor atom 96. Unsur seri aktinida ini dinamai Marie dan Pierre Curie \u2013 keduanya dikenal karena penelitian mereka tentang radioaktivitas. Curium pertama kali sengaja diproduksi dan diidentifikasi pada bulan Juli 1944 oleh kelompok Glenn T. Seaborg di Universitas California, Berkeley.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f7 6d1",
        "melt": "1613 K",
        "boil": "3383 K",
        "density": "13.51 g/cm\u00b3"
    },
    {
        "number": 97,
        "symbol": "Bk",
        "name": "Berkelium",
        "mass": "247",
        "col": 11,
        "row": 10,
        "category": "actinide",
        "desc": "Berkelium adalah unsur kimia radioaktif transuranik dengan lambang Bk dan nomor atom 97. Ia merupakan anggota rangkaian unsur aktinida dan transuranium. Namanya diambil dari kota Berkeley, California, lokasi Laboratorium Radiasi Universitas California di mana ia ditemukan pada bulan Desember 1949.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f9",
        "melt": "1259 K",
        "boil": "2900 K",
        "density": "14.78 g/cm\u00b3"
    },
    {
        "number": 98,
        "symbol": "Cf",
        "name": "Californium",
        "mass": "251",
        "col": 12,
        "row": 10,
        "category": "actinide",
        "desc": "Kalifornium adalah unsur kimia logam radioaktif dengan lambang Cf dan nomor atom 98. Unsur ini pertama kali dibuat pada tahun 1950 di Laboratorium Radiasi Universitas California di Berkeley, dengan membombardir curium dengan partikel alfa (ion helium-4). Ini adalah unsur aktinida, unsur transuranium keenam yang disintesis, dan memiliki massa atom tertinggi kedua dari semua unsur yang telah diproduksi dalam jumlah yang cukup besar untuk dilihat dengan mata telanjang (setelah einsteinium).",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f10",
        "melt": "1173 K",
        "boil": "1743 K",
        "density": "15.1 g/cm\u00b3"
    },
    {
        "number": 99,
        "symbol": "Es",
        "name": "Einsteinium",
        "mass": "252",
        "col": 13,
        "row": 10,
        "category": "actinide",
        "desc": "Einsteinium adalah unsur sintetik dengan simbol Es dan nomor atom 99. Ia adalah unsur transuranium ketujuh, dan merupakan aktinida. Einsteinium ditemukan sebagai komponen puing-puing ledakan bom hidrogen pertama pada tahun 1952, dan dinamai menurut nama Albert Einstein.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f11",
        "melt": "1133 K",
        "boil": "1269 K",
        "density": "8.84 g/cm\u00b3"
    },
    {
        "number": 100,
        "symbol": "Fm",
        "name": "Fermium",
        "mass": "257",
        "col": 14,
        "row": 10,
        "category": "actinide",
        "desc": "Fermium adalah unsur sintetik dengan simbol Fm dan nomor atom 100. Fermium merupakan anggota deret aktinida. Ini adalah unsur terberat yang dapat dibentuk melalui bombardir neutron terhadap unsur yang lebih ringan, dan karenanya merupakan unsur terakhir yang dapat dibuat dalam jumlah makroskopis, meskipun logam fermium murni belum dapat dibuat.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f12",
        "melt": "1800 K",
        "boil": "Unknown",
        "density": "Unknown"
    },
    {
        "number": 101,
        "symbol": "Md",
        "name": "Mendelevium",
        "mass": "258",
        "col": 15,
        "row": 10,
        "category": "actinide",
        "desc": "Mendelevium adalah unsur sintetik dengan simbol kimia Md (sebelumnya Mv) dan nomor atom 101. Unsur transuranik radioaktif logam dalam deret aktinida, merupakan unsur pertama yang saat ini tidak dapat diproduksi dalam jumlah makroskopis melalui pemboman neutron terhadap unsur yang lebih ringan. Ini adalah aktinida antepenultimate dan elemen transuranik kesembilan.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f13",
        "melt": "1100 K",
        "boil": "Unknown",
        "density": "Unknown"
    },
    {
        "number": 102,
        "symbol": "No",
        "name": "Nobelium",
        "mass": "259",
        "col": 16,
        "row": 10,
        "category": "actinide",
        "desc": "Nobelium adalah unsur kimia sintetik dengan simbol No dan nomor atom 102. Nama ini diambil untuk menghormati Alfred Nobel, penemu dinamit dan dermawan ilmu pengetahuan. Merupakan logam radioaktif, merupakan unsur transuranik kesepuluh dan merupakan anggota kedua dari belakang deret aktinida.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14",
        "melt": "1100 K",
        "boil": "Unknown",
        "density": "Unknown"
    },
    {
        "number": 103,
        "symbol": "Lr",
        "name": "Lawrencium",
        "mass": "266",
        "col": 17,
        "row": 10,
        "category": "actinide",
        "desc": "Lawrencium adalah unsur kimia sintetis dengan simbol kimia Lr (sebelumnya Lw) dan nomor atom 103. Nama ini diambil untuk menghormati Ernest Lawrence, penemu siklotron, perangkat yang digunakan untuk menemukan banyak unsur radioaktif buatan. Sebuah logam radioaktif, lawrencium adalah unsur transuranik kesebelas dan juga merupakan anggota terakhir dari deret aktinida.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 7p1",
        "melt": "1900 K",
        "boil": "Unknown",
        "density": "Unknown"
    },
    {
        "number": 104,
        "symbol": "Rf",
        "name": "Rutherfordium",
        "mass": "267",
        "col": 4,
        "row": 7,
        "category": "transition-metal",
        "desc": "Rutherfordium adalah unsur kimia dengan simbol Rf dan nomor atom 104, dinamai untuk menghormati fisikawan Ernest Rutherford. Merupakan unsur sintetik (unsur yang dapat dibuat di laboratorium tetapi tidak ditemukan di alam) dan radioaktif; isotop paling stabil yang diketahui, 267Rf, memiliki waktu paruh sekitar 1,3 jam. Dalam tabel periodik unsur, unsur ini merupakan unsur blok d dan unsur transisi baris kedua dari baris keempat.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d2",
        "melt": "2400 K",
        "boil": "5800 K",
        "density": "23.2 g/cm\u00b3"
    },
    {
        "number": 105,
        "symbol": "Db",
        "name": "Dubnium",
        "mass": "268",
        "col": 5,
        "row": 7,
        "category": "transition-metal",
        "desc": "Dubnium adalah suatu unsur kimia dengan simbol Db dan nomor atom 105. Namanya diambil dari nama kota Dubna di Rusia (utara Moskow), tempat ia pertama kali diproduksi. Merupakan unsur sintetik (unsur yang dapat dibuat di laboratorium tetapi tidak ditemukan di alam) dan radioaktif; isotop paling stabil yang diketahui, dubnium-268, memiliki waktu paruh sekitar 28 jam.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d3",
        "melt": "Unknown",
        "boil": "Unknown",
        "density": "29.3 g/cm\u00b3"
    },
    {
        "number": 106,
        "symbol": "Sg",
        "name": "Seaborgium",
        "mass": "269",
        "col": 6,
        "row": 7,
        "category": "transition-metal",
        "desc": "Seaborgium adalah unsur sintetik dengan simbol Sg dan nomor atom 106. Isotop paling stabilnya, 271Sg, memiliki waktu paruh 1,9 menit. Isotop 269Sg yang baru ditemukan berpotensi memiliki waktu paruh yang sedikit lebih lama (ca.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d4",
        "melt": "Unknown",
        "boil": "Unknown",
        "density": "35 g/cm\u00b3"
    },
    {
        "number": 107,
        "symbol": "Bh",
        "name": "Bohrium",
        "mass": "270",
        "col": 7,
        "row": 7,
        "category": "transition-metal",
        "desc": "Bohrium adalah suatu unsur kimia dengan simbol Bh dan nomor atom 107. Namanya diambil dari nama fisikawan Denmark Niels Bohr. Merupakan unsur sintetik (unsur yang dapat dibuat di laboratorium tetapi tidak ditemukan di alam) dan radioaktif; isotop paling stabil yang diketahui, 270Bh, memiliki waktu paruh sekitar 61 detik.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d5",
        "melt": "Unknown",
        "boil": "Unknown",
        "density": "37.1 g/cm\u00b3"
    },
    {
        "number": 108,
        "symbol": "Hs",
        "name": "Hassium",
        "mass": "269",
        "col": 8,
        "row": 7,
        "category": "transition-metal",
        "desc": "Hassium adalah unsur kimia dengan simbol Hs dan nomor atom 108, dinamai berdasarkan nama negara bagian Hesse di Jerman. Merupakan unsur sintetik (unsur yang dapat dibuat di laboratorium tetapi tidak ditemukan di alam) dan radioaktif; isotop paling stabil yang diketahui, 269Hs, memiliki waktu paruh sekitar 9,7 detik, meskipun keadaan metastabil yang belum dikonfirmasi, 277mHs, mungkin memiliki waktu paruh lebih lama sekitar 130 detik. Lebih dari 100 atom hassium telah disintesis hingga saat ini.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d6",
        "melt": "126 K",
        "boil": "Unknown",
        "density": "40.7 g/cm\u00b3"
    },
    {
        "number": 109,
        "symbol": "Mt",
        "name": "Meitnerium",
        "mass": "278",
        "col": 9,
        "row": 7,
        "category": "transition-metal",
        "desc": "Meitnerium adalah unsur kimia dengan simbol Mt dan nomor atom 109. Meitnerium adalah unsur sintetik yang sangat radioaktif (unsur yang tidak ditemukan di alam dan dapat dibuat di laboratorium). Isotop paling stabil yang diketahui, meitnerium-278, memiliki waktu paruh 7,6 detik.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d7",
        "melt": "Unknown",
        "boil": "Unknown",
        "density": "37.4 g/cm\u00b3"
    },
    {
        "number": 110,
        "symbol": "Ds",
        "name": "Darmstadtium",
        "mass": "281",
        "col": 10,
        "row": 7,
        "category": "transition-metal",
        "desc": "Darmstadtium adalah suatu unsur kimia dengan simbol Ds dan nomor atom 110. Merupakan unsur sintetik yang sangat radioaktif. Isotop paling stabil yang diketahui, darmstadtium-281, memiliki waktu paruh sekitar 10 detik.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d8",
        "melt": "Unknown",
        "boil": "Unknown",
        "density": "34.8 g/cm\u00b3"
    },
    {
        "number": 111,
        "symbol": "Rg",
        "name": "Roentgenium",
        "mass": "282",
        "col": 11,
        "row": 7,
        "category": "transition-metal",
        "desc": "Roentgenium adalah unsur kimia dengan simbol Rg dan nomor atom 111. Merupakan unsur sintetik yang sangat radioaktif (unsur yang dapat dibuat di laboratorium tetapi tidak ditemukan di alam); isotop paling stabil yang diketahui, roentgenium-282, memiliki waktu paruh 2,1 menit. Roentgenium pertama kali dibuat pada tahun 1994 oleh Pusat Penelitian Ion Berat GSI Helmholtz dekat Darmstadt, Jerman.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d9",
        "melt": "Unknown",
        "boil": "Unknown",
        "density": "28.7 g/cm\u00b3"
    },
    {
        "number": 112,
        "symbol": "Cn",
        "name": "Copernicium",
        "mass": "285",
        "col": 12,
        "row": 7,
        "category": "transition-metal",
        "desc": "Copernicium adalah unsur kimia dengan simbol Cn dan nomor atom 112. Merupakan unsur sintetik yang sangat radioaktif yang hanya dapat dibuat di laboratorium. Isotop paling stabil yang diketahui, copernicium-285, memiliki waktu paruh sekitar 29 detik, namun ada kemungkinan bahwa isotop copernicium ini memiliki isomer nuklir dengan waktu paruh lebih lama, 8,9 menit.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d10",
        "melt": "Unknown",
        "boil": "3570 K",
        "density": "14.0 g/cm\u00b3"
    },
    {
        "number": 113,
        "symbol": "Nh",
        "name": "Nihonium",
        "mass": "286",
        "col": 13,
        "row": 7,
        "category": "transition-metal",
        "desc": "Nihonium adalah unsur kimia dengan nomor atom 113. Ia memiliki simbol Nh. Ini adalah unsur sintetis (unsur yang dapat dibuat di laboratorium tetapi tidak ditemukan di alam) dan sangat radioaktif; isotop paling stabil yang diketahui, nihonium-286, memiliki waktu paruh 20 detik.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d10 7p1",
        "melt": "700 K",
        "boil": "1430 K",
        "density": "16 g/cm\u00b3"
    },
    {
        "number": 114,
        "symbol": "Fl",
        "name": "Flerovium",
        "mass": "289",
        "col": 14,
        "row": 7,
        "category": "transition-metal",
        "desc": "Flerovium adalah unsur kimia buatan superberat dengan simbol Fl dan nomor atom 114. Ini adalah unsur sintetis yang sangat radioaktif. Nama unsur ini diambil dari Laboratorium Reaksi Nuklir Flerov dari Institut Gabungan untuk Penelitian Nuklir di Dubna, Rusia, tempat unsur tersebut ditemukan pada tahun 1998.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d10 7p2",
        "melt": "340 K",
        "boil": "420 K",
        "density": "14 g/cm\u00b3"
    },
    {
        "number": 115,
        "symbol": "Mc",
        "name": "Moscovium",
        "mass": "289",
        "col": 15,
        "row": 7,
        "category": "transition-metal",
        "desc": "Moscovium adalah nama unsur superberat sintetik dalam tabel periodik yang memiliki simbol Mc dan memiliki nomor atom 115. Merupakan unsur yang sangat radioaktif; isotop paling stabil yang diketahui, moscovium-289, memiliki waktu paruh hanya 220 milidetik. Ia juga dikenal sebagai eka-bismut atau hanya unsur 115.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d10 7p3",
        "melt": "670 K",
        "boil": "1400 K",
        "density": "13.5 g/cm\u00b3"
    },
    {
        "number": 116,
        "symbol": "Lv",
        "name": "Livermorium",
        "mass": "293",
        "col": 16,
        "row": 7,
        "category": "transition-metal",
        "desc": "Livermorium adalah unsur superberat sintetik dengan simbol Lv dan nomor atom 116. Ini adalah unsur yang sangat radioaktif yang hanya dibuat di laboratorium dan belum pernah diamati di alam. Nama unsur ini diambil dari nama Laboratorium Nasional Lawrence Livermore di Amerika Serikat, yang bekerja sama dengan Institut Gabungan untuk Penelitian Nuklir di Dubna, Rusia untuk menemukan livermorium pada tahun 2000.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d10 7p4",
        "melt": "709 K",
        "boil": "1085 K",
        "density": "12.9 g/cm\u00b3"
    },
    {
        "number": 117,
        "symbol": "Ts",
        "name": "Tennessine",
        "mass": "294",
        "col": 17,
        "row": 7,
        "category": "metalloid",
        "desc": "Tennessine adalah unsur kimia buatan superberat dengan nomor atom 117 dan simbol Ts. Juga dikenal sebagai eka-astatin atau unsur 117, unsur ini merupakan unsur terberat kedua dan unsur kedua dari belakang pada periode ke-7 tabel periodik. Pada tahun 2016, lima belas atom tennessine telah diamati: enam saat pertama kali disintesis pada tahun 2010, tujuh pada tahun 2012, dan dua pada tahun 2014.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d10 7p5",
        "melt": "723 K",
        "boil": "883 K",
        "density": "7.17 g/cm\u00b3"
    },
    {
        "number": 118,
        "symbol": "Og",
        "name": "Oganesson",
        "mass": "294",
        "col": 18,
        "row": 7,
        "category": "noble-gas",
        "desc": "Oganesson adalah nama IUPAC untuk unsur transaktinida dengan nomor atom 118 dan lambang unsur Og. Ia juga dikenal sebagai eka-radon atau unsur 118, dan pada tabel periodik unsur-unsur tersebut merupakan unsur blok p dan terakhir pada periode ke-7. Oganesson saat ini menjadi satu-satunya anggota sintetik di grup 18.",
        "config": "1s2 2s2 2p6 3s2 3p6 4s2 3d10 4p6 5s2 4d10 5p6 6s2 4f14 5d10 6p6 7s2 5f14 6d10 7p6",
        "melt": "Unknown",
        "boil": "350 K",
        "density": "4.95 g/cm\u00b3"
    }
];

const tableContainer = document.getElementById('periodic-table');
const tooltip = document.getElementById('tooltip');
const infoPanel = document.getElementById('info-panel');

// Tooltip elements
const ttNum = document.getElementById('tt-number');
const ttMass = document.getElementById('tt-mass');
const ttSymbol = document.getElementById('tt-symbol');
const ttName = document.getElementById('tt-name');

function renderTable() {
    elementsData.forEach(element => {
        const elDiv = document.createElement('div');
        elDiv.classList.add('element', element.category);
        elDiv.style.gridColumn = element.col;
        elDiv.style.gridRow = element.row;
        
        elDiv.innerHTML = `
            <div class="el-header">
                <span>${element.number}</span>
                <span>${parseFloat(element.mass).toFixed(3)}</span>
            </div>
            <div class="el-symbol">${element.symbol}</div>
            <div class="el-name">${element.name}</div>
        `;

        // Event Listeners
        elDiv.addEventListener('mouseenter', (e) => showTooltip(e, element));
        elDiv.addEventListener('mouseleave', hideTooltip);
        elDiv.addEventListener('click', () => selectElement(element, elDiv));
        
        tableContainer.appendChild(elDiv);
    });
}

function showTooltip(event, elData) {
    // Populate Data
    ttNum.textContent = elData.number;
    ttMass.textContent = parseFloat(elData.mass).toFixed(4);
    ttSymbol.textContent = elData.symbol;
    ttName.textContent = elData.name;
    
    // Clear and set background class based on category
    tooltip.className = 'element-tooltip show ' + elData.category;
    // Overwrite class name style manually for the tooltip specific glass effect
    const categoryBg = getComputedStyle(event.target).backgroundColor;
    const categoryBorder = getComputedStyle(event.target).borderColor;
    tooltip.style.background = categoryBg.replace('0.15', '0.85'); // make it more opaque but keep color
    tooltip.style.border = `1px solid ${categoryBorder}`;

    // Position tooltip
    const cellRect = event.target.getBoundingClientRect();
    const tableRect = tableContainer.getBoundingClientRect();

    let top = cellRect.top - tableRect.top + cellRect.height / 2;
    let left = cellRect.left - tableRect.left + cellRect.width / 2;
    
    // Ensure it doesn't go off screen
    tooltip.style.top = `${top}px`;
    tooltip.style.left = `${left}px`;
    // Slight offset to not block mouse completely
    tooltip.style.transform = `translate(-10px, -110%) scale(1)`; 
}

function hideTooltip() {
    tooltip.style.transform = `translate(-10px, -110%) scale(0)`;
    tooltip.style.opacity = '0';
    setTimeout(() => {
        tooltip.classList.remove('show');
    }, 200);
}

function selectElement(elData, elementNode) {
    // Remove selected class from all
    document.querySelectorAll('.element').forEach(el => el.classList.remove('selected'));
    elementNode.classList.add('selected');

    document.getElementById('info-placeholder').classList.add('hidden');
    document.getElementById('info-content').classList.remove('hidden');

    document.getElementById('panel-name').textContent = elData.name;
    document.getElementById('panel-symbol').textContent = elData.symbol;
    document.getElementById('panel-number').textContent = elData.number;
    
    const categoryName = elData.category.split('-').map(w => w.charAt(0).toUpperCase() + w.slice(1)).join(' ');
    document.getElementById('panel-category-text').textContent = categoryName;
    document.getElementById('panel-category-dot').className = 'category-dot dot-' + elData.category;

    document.getElementById('nucleus-symbol').textContent = elData.symbol;
    document.getElementById('panel-description').textContent = elData.desc;
    
    document.getElementById('panel-detail-symbol').textContent = elData.symbol;
    document.getElementById('panel-detail-mass').textContent = elData.mass;
    document.getElementById('panel-density').textContent = elData.density;
    document.getElementById('panel-melt').textContent = elData.melt;
    document.getElementById('panel-boil').textContent = elData.boil;
    document.getElementById('panel-configuration').textContent = elData.config;

    renderBohrModel(elData.number);
}

function renderBohrModel(atomicNumber) {
    const orbitsContainer = document.getElementById('orbits');
    orbitsContainer.innerHTML = ''; // clear previous

    // Simplified shells representation (2, 8, 18, 32, 32, 18, 8)
    let electrons = atomicNumber;
    const shells = [2, 8, 18, 32, 32, 18, 8];
    const actualShells = [];
    
    for (const capacity of shells) {
        if (electrons > 0) {
            const inThisShell = Math.min(electrons, capacity);
            actualShells.push(inThisShell);
            electrons -= inThisShell;
        } else {
            break;
        }
    }

    // Maximum 7 shells. Draw rings inside the 150x150 container.
    actualShells.forEach((numElectrons, index) => {
        const radius = 25 + (index * 15); // growing radius
        const orbit = document.createElement('div');
        orbit.className = 'orbit';
        orbit.style.width = `${radius * 2}px`;
        orbit.style.height = `${radius * 2}px`;

        orbit.style.animationDuration = `${10 + (index * 5)}s`;
        if (index % 2 !== 0) {
            orbit.style.animationDirection = 'reverse';
        }

        for (let e = 0; e < numElectrons; e++) {
            const electron = document.createElement('div');
            electron.className = 'electron';
            // Evenly distribute electrons on the ring
            const angle = (e / numElectrons) * 360;
            // Position them on the border of the ring
            electron.style.transform = `rotate(${angle}deg) translate(${radius}px) rotate(-${angle}deg)`;
            electron.style.top = '50%';
            electron.style.left = '50%';
            electron.style.marginTop = '-3px';
            electron.style.marginLeft = '-3px';
            orbit.appendChild(electron);
        }

        orbitsContainer.appendChild(orbit);
    });
}

// Initialize
renderTable();
