<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Icon Server - Gallery</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
        }

        h1 {
            text-align: center;
            color: #667eea;
            font-size: 3em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }

        .subtitle {
            text-align: center;
            color: #666;
            margin-bottom: 40px;
            font-size: 1.2em;
        }

        .section {
            margin-bottom: 50px;
        }

        .section-title {
            font-size: 2em;
            color: #764ba2;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 3px solid #667eea;
        }

        .subsection-title {
            font-size: 1.5em;
            color: #555;
            margin: 30px 0 15px 0;
            padding-left: 15px;
            border-left: 4px solid #764ba2;
        }

        .icon-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .icon-card {
            background: white;
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            border: 2px solid transparent;
        }

        .icon-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);
            border-color: #667eea;
        }

        .icon-preview {
            width: 100%;
            height: 120px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            border-radius: 8px;
            margin-bottom: 15px;
            overflow: hidden;
        }

        .icon-preview img {
            max-width: 80%;
            max-height: 80%;
            object-fit: contain;
        }

        .icon-name {
            font-weight: 600;
            color: #333;
            margin-bottom: 10px;
            font-size: 0.95em;
            word-break: break-all;
        }

        .url-container {
            display: flex;
            gap: 5px;
            background: #f8f9fa;
            padding: 8px;
            border-radius: 6px;
            align-items: center;
        }

        .url-input {
            flex: 1;
            border: none;
            background: transparent;
            font-size: 0.85em;
            color: #555;
            outline: none;
            font-family: 'Courier New', monospace;
        }

        .copy-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.85em;
            font-weight: 600;
            transition: all 0.3s ease;
            white-space: nowrap;
        }

        .copy-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
        }

        .copy-btn:active {
            transform: scale(0.95);
        }

        .copied {
            background: linear-gradient(135deg, #56ab2f 0%, #a8e063 100%);
        }

        .video-section {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            padding: 20px;
            border-radius: 12px;
            color: white;
        }

        .video-section .subsection-title {
            color: white;
            border-left-color: white;
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 2em;
            }

            .icon-grid {
                grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            }

            .container {
                padding: 20px;
            }
        }

        .stats {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-bottom: 40px;
            flex-wrap: wrap;
        }

        .stat-box {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px 30px;
            border-radius: 12px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
        }

        .stat-number {
            font-size: 2.5em;
            font-weight: bold;
        }

        .stat-label {
            font-size: 0.9em;
            opacity: 0.9;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🎨 Icon Server Gallery</h1>
        <p class="subtitle">Haz clic en "Copiar" para obtener la URL de cualquier recurso</p>

        <div class="stats">
            <div class="stat-box">
                <div class="stat-number" id="totalIcons">0</div>
                <div class="stat-label">Iconos Totales</div>
            </div>
            <div class="stat-box">
                <div class="stat-number">8</div>
                <div class="stat-label">Categorías</div>
            </div>
        </div>

        <!-- MaskPages Section -->
        <div class="section">
            <h2 class="section-title">📚 MaskPages</h2>
            <div class="icon-grid" id="maskpages"></div>
        </div>

        <!-- SVG Icons Section -->
        <div class="section">
            <h2 class="section-title">✨ SVG Icons</h2>
            
            <h3 class="subsection-title">⚫ Black & White</h3>
            <div class="icon-grid" id="blacks-white"></div>

            <h3 class="subsection-title">🎯 Icons</h3>
            <div class="icon-grid" id="icons"></div>

            <h3 class="subsection-title">🌐 Redes Sociales</h3>
            <div class="icon-grid" id="redes"></div>

            <h3 class="subsection-title">💻 Tecnologías</h3>
            <div class="icon-grid" id="tecnologias"></div>
        </div>

        <!-- Videos Section -->
        <div class="section video-section">
            <h2 class="section-title" style="color: white; border-bottom-color: white;">🎬 Videos</h2>
            <div class="icon-grid" id="videos"></div>
        </div>
    </div>

    <script>
        const baseUrl = 'https://bemmoralesmora.github.io/Icons/';
        let totalCount = 0;

        const resources = {
            maskpages: [
                'assets/MaskPages/books.png',
                'assets/MaskPages/cart.svg',
                'assets/MaskPages/corazon.svg',
                'assets/MaskPages/libro_flor.png',
                'assets/MaskPages/libro_key.png',
                'assets/MaskPages/libro_tree.png',
                'assets/MaskPages/libro_winter.png',
                'assets/MaskPages/star.svg'
            ],
            'blacks-white': [
                'assets/svg/blacks and white/cisco.svg',
                'assets/svg/blacks and white/clevercloud.svg',
                'assets/svg/blacks and white/css.svg',
                'assets/svg/blacks and white/express.svg',
                'assets/svg/blacks and white/firebase.svg',
                'assets/svg/blacks and white/github.svg',
                'assets/svg/blacks and white/git.svg',
                'assets/svg/blacks and white/gnometerminal.svg',
                'assets/svg/blacks and white/html5.svg',
                'assets/svg/blacks and white/javascript.svg',
                'assets/svg/blacks and white/linux.svg',
                'assets/svg/blacks and white/micropython.svg',
                'assets/svg/blacks and white/mysql.svg',
                'assets/svg/blacks and white/nodedotjs.svg',
                'assets/svg/blacks and white/npm.svg',
                'assets/svg/blacks and white/python.svg',
                'assets/svg/blacks and white/react.svg',
                'assets/svg/blacks and white/render.svg'
            ],
            icons: [
                'assets/svg/icons/account_circle_24dp_E3E3E3_FILL0_wght400_GRAD0_opsz24.svg',
                'assets/svg/icons/account.svg',
                'assets/svg/icons/application.svg',
                'assets/svg/icons/biotech_24dp_E3E3E3_FILL0_wght400_GRAD0_opsz24.svg',
                'assets/svg/icons/brush_24dp_E3E3E3_FILL0_wght400_GRAD0_opsz24.svg',
                'assets/svg/icons/calendar.svg',
                'assets/svg/icons/check.svg',
                'assets/svg/icons/clock.svg',
                'assets/svg/icons/comment.svg',
                'assets/svg/icons/corona.svg',
                'assets/svg/icons/favorite_24dp_E3E3E3_FILL0_wght400_GRAD0_opsz24.svg',
                'assets/svg/icons/filter.svg',
                'assets/svg/icons/idea.svg',
                'assets/svg/icons/inbox.svg',
                'assets/svg/icons/lock.svg',
                'assets/svg/icons/logo.svg',
                'assets/svg/icons/mail.svg',
                'assets/svg/icons/mimo_24dp_E3E3E3_FILL0_wght400_GRAD0_opsz24.svg',
                'assets/svg/icons/monitoring_24dp_E3E3E3_FILL0_wght400_GRAD0_opsz24.svg',
                'assets/svg/icons/notifications.svg',
                'assets/svg/icons/palette.svg',
                'assets/svg/icons/pause.svg',
                'assets/svg/icons/play.svg',
                'assets/svg/icons/points.svg',
                'assets/svg/icons/search.svg',
                'assets/svg/icons/send.svg',
                'assets/svg/icons/settings.svg',
                'assets/svg/icons/terminal.svg',
                'assets/svg/icons/timer.svg',
                'assets/svg/icons/visibility_24dp_E3E3E3_FILL0_wght400_GRAD0_opsz24.svg'
            ],
            redes: [
                'assets/svg/redes/facebook.svg',
                'assets/svg/redes/instagram.svg',
                'assets/svg/redes/pinterest.svg',
                'assets/svg/redes/twitter.svg'
            ],
            tecnologias: [
                'assets/svg/tecnologias/CSS3.svg',
                'assets/svg/tecnologias/Docker.svg',
                'assets/svg/tecnologias/Express.svg',
                'assets/svg/tecnologias/facebook.svg',
                'assets/svg/tecnologias/HTML5.svg',
                'assets/svg/tecnologias/instagram.svg',
                'assets/svg/tecnologias/JavaScript.svg',
                'assets/svg/tecnologias/Java.svg',
                'assets/svg/tecnologias/Linux.svg',
                'assets/svg/tecnologias/MySQL.svg',
                'assets/svg/tecnologias/Next.js.svg',
                'assets/svg/tecnologias/Node.js.svg',
                'assets/svg/tecnologias/pinterest.svg',
                'assets/svg/tecnologias/PostgresSQL.svg',
                'assets/svg/tecnologias/Python.svg',
                'assets/svg/tecnologias/React.svg',
                'assets/svg/tecnologias/twitter.svg',
                'assets/svg/tecnologias/Vite.js.svg'
            ],
            videos: [
                'assets/videos/video1.mp4',
                'assets/videos/video.mp4'
            ]
        };

        function createIconCard(path) {
            totalCount++;
            const fileName = path.split('/').pop();
            const fullUrl = baseUrl + path;
            const isVideo = path.endsWith('.mp4');

            return `
                <div class="icon-card">
                    <div class="icon-preview">
                        ${isVideo ? 
                            `<video style="max-width: 100%; max-height: 100%;" controls>
                                <source src="${fullUrl}" type="video/mp4">
                            </video>` :
                            `<img src="${fullUrl}" alt="${fileName}">`
                        }
                    </div>
                    <div class="icon-name">${fileName}</div>
                    <div class="url-container">
                        <input type="text" class="url-input" value="${fullUrl}" readonly>
                        <button class="copy-btn" onclick="copyUrl(this, '${fullUrl}')">Copiar</button>
                    </div>
                </div>
            `;
        }

        function copyUrl(button, url) {
            navigator.clipboard.writeText(url).then(() => {
                const originalText = button.textContent;
                button.textContent = '✓ Copiado';
                button.classList.add('copied');
                
                setTimeout(() => {
                    button.textContent = originalText;
                    button.classList.remove('copied');
                }, 2000);
            });
        }

        Object.keys(resources).forEach(category => {
            const container = document.getElementById(category);
            if (container) {
                container.innerHTML = resources[category].map(path => createIconCard(path)).join('');
            }
        });

        document.getElementById('totalIcons').textContent = totalCount;
    </script>
</body>
</html>
