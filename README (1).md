# forumCSM
     <!DOCTYPE html>
    <html lang="ru">
     <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>cult/csm · архив разработчика</title>
    <!-- Стиль в духе archive.vn: минимализм, моноширинность, нейтральные тона, акцент на контент -->
    <style>
        /* Глобальный сброс и база — как у архивных зеркал */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: #f5f5f7;   /* чуть теплый серый фон, как у старых интерфейсов */
            font-family: 'Courier New', Courier, 'Liberation Mono', monospace;
            line-height: 1.5;
            color: #1e1e1e;
            padding: 20px;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* главный контейнер — узкая колонка, как снимок страницы */
        .archive-frame {
            max-width: 860px;
            margin: 0 auto;
            width: 100%;
            background-color: #ffffff;
            border: 1px solid #777;
            box-shadow: 6px 6px 0 rgba(0,0,0,0.1);
            padding: 2rem 2rem 1.5rem;
            position: relative;
        }

        /* шапка в духе archive.today / vn — строка браузера/метаданные */
        .browser-meta {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: baseline;
            border-bottom: 1px dashed #888;
            padding-bottom: 0.75rem;
            margin-bottom: 2rem;
            font-size: 0.95rem;
            color: #333;
            letter-spacing: -0.02em;
        }

        .browser-meta .domain {
            font-weight: bold;
            background: #eaeaea;
            padding: 0.2rem 0.6rem;
            border: 1px solid #aaa;
            font-size: 0.9rem;
        }

        .browser-meta .timestamp {
            color: #505050;
            border: 1px solid #ccc;
            padding: 0.2rem 0.6rem;
            background: #f0f0f0;
        }

        /* "сохранено в культуре" — как архивная метка */
        .archive-badge {
            background-color: #d9d2b3;
            border: 1px solid #7a6a4a;
            padding: 0.5rem 1rem;
            margin-bottom: 2rem;
            font-size: 0.9rem;
            display: inline-block;
            text-transform: uppercase;
            letter-spacing: 2px;
            font-weight: 600;
            color: #2d2d2d;
            border-left: 6px solid #5e4b3a;
        }

        /* автор/разработчик */
        .dev-header {
            display: flex;
            align-items: center;
            gap: 1rem;
            margin-bottom: 2.5rem;
            background: #fafafa;
            padding: 1rem 1.2rem;
            border: 1px solid #b0b0b0;
        }

        .dev-avatar {
            width: 64px;
            height: 64px;
            background: #b3b3b3;
            border-radius: 0;
            border: 2px solid #1e1e1e;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            font-weight: bold;
            color: #0f0f0f;
            background: #cfcfcf;
        }

        .dev-info h1 {
            font-size: 1.8rem;
            font-weight: 600;
            letter-spacing: -0.5px;
            line-height: 1.2;
        }

        .dev-info .handle {
            font-size: 1.1rem;
            color: #3a3a3a;
            background: #e8e8e8;
            padding: 0.1rem 0.4rem;
            border: 1px solid #6d6d6d;
        }

        /* навигация — табы как archive.org */
        .nav-links {
            display: flex;
            gap: 0;
            margin-bottom: 2.5rem;
            border-bottom: 2px solid #333;
            flex-wrap: wrap;
        }

        .nav-links a {
            padding: 0.5rem 1.2rem;
            background: #ddd;
            border: 1px solid #333;
            border-bottom: none;
            margin-right: 4px;
            text-decoration: none;
    color: #1e1e1e;
            font-weight: bold;
            font-size: 0.9rem;
            transition: 0.1s ease;
        }

        .nav-links a.active {
            background: #fff;
            border-bottom: 2px solid #fff;
            margin-bottom: -2px;
            position: relative;
            z-index: 1;
            color: #000;
        }

        .nav-links a:hover {
            background: #b0b0b0;
            color: #000;
        }

        /* секция постов — как список захваченных урлов */
        .post-list {
            list-style: none;
            margin: 2rem 0 2.5rem 0;
            border-top: 1px solid #aaa;
        }

        .post-item {
            display: flex;
            flex-wrap: wrap;
            align-items: baseline;
            padding: 1rem 0.5rem;
            border-bottom: 1px dotted #6f6f6f;
            transition: background 0.1s;
        }

        .post-item:hover {
            background: #f1f1e8;
        }

        .post-date {
            font-family: 'Courier New', monospace;
            min-width: 120px;
            color: #5f5f5f;
            font-size: 0.85rem;
            letter-spacing: -0.5px;
            border-right: 1px solid #acacac;
            padding-right: 1rem;
            margin-right: 1.2rem;
        }

        .post-title {
            flex: 1;
            font-weight: 600;
            font-size: 1.3rem;
        }

        .post-title a {
            text-decoration: none;
            color: #1f2a3f;
            border-bottom: 1px dashed #6f6f6f;
        }

        .post-title a:hover {
            border-bottom: 2px solid #b30000;
            color: #000;
        }

        .post-meta {
            width: 100%;
            margin-top: 0.4rem;
            margin-left: 0;
            padding-left: calc(120px + 1.2rem); /* выравнивание под дату */
            font-size: 0.85rem;
            color: #4f4f4f;
        }

        .post-meta .tag {
            background: #dbdbdb;
            border: 1px solid #717171;
            padding: 0.1rem 0.4rem;
            margin-right: 0.5rem;
        }

        /* блок с фичей «заархивировано разработчиком» — как архивные ссылки */
        .action-bar {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin: 2rem 0 1.5rem;
            background: #ecece0;
            border: 1px solid #6a5f4e;
            padding: 1rem 1.5rem;
            align-items: center;
        }

        .action-bar input {
            background: #fff;
            border: 1px solid #666;
            padding: 0.5rem 1rem;
            font-family: 'Courier New', monospace;
            flex: 2 1 250px;
            font-size: 0.9rem;
        }

        .action-bar button {
            background: #cfcfcf;
            border: 2px solid #3b3b3b;
            padding: 0.5rem 1.8rem;
            font-family: 'Courier New', monospace;
            font-weight: bold;
            cursor: pointer;
            transition: 0.1s;
            box-shadow: 3px 3px 0 #6b6b6b;
        }

        .action-bar button:hover {
            background: #b3b3b3;
            box-shadow: 1px 1px 0 #3b3b3b;
            transform: translate(2px, 2px);
        }

        /* подвал с архивной метаинформацией */
        .footer-archive {
            margin-top: 2.5rem;
            border-top: 3px double #484848;
            padding-top: 1.2rem;
            font-size: 0.8rem;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            color: #454545;
        }

        .footer-archive .capture-info {
            background: #e3e3d3;
            padding: 0.2rem 0.8rem;
            border: 1px solid #6f6f6f;
        }

        .footer-archive .github-domain {
            font-weight: bold;
            background: #000;
            color: #eee;
            padding: 0.2rem 0.8rem;
            border: 1px solid #b3b3b3;
        }

        /* код сниппет — имитация захвата */
        .pre-code {
            background: #1e1e1e;
            color: #f1f1f1;
            padding: 1.2rem;
     border-left: 8px solid #6d6d6d;
            margin: 2rem 0;
            font-size: 0.85rem;
            overflow-x: auto;
        }

        .pre-code .comment {
            color: #9e9e9e;
        }

        /* адаптив */
        @media (max-width: 650px) {
            .archive-frame { padding: 1rem; }
            .post-date { min-width: 90px; }
            .post-meta { padding-left: calc(90px + 0.8rem); }
            .dev-header { flex-wrap: wrap; }
        }
    </style>
     </head>
     <body>
    <div class="archive-frame">
        <!-- верхняя панель как в archive.vn — URL и время захвата -->
        <div class="browser-meta">
            <span class="domain">cultcsm.github.io</span>
            <span class="timestamp">захват произведён 2026-03-16 21:34 UTC</span>
            </div>

        <!-- характерный архивный значок "сохранено в ..." -->
        <div class="archive-badge">
            ⚡ CULT/CSM · PERMANENT DEVELOPER LOG ⚡
        </div>

        <!-- шапка разработчика -->
        <div class="dev-header">
            <div class="dev-avatar">{ c}</div>
            <div class="dev-info">
                <h1>cult/csm developer</h1>
                <span class="handle">@cult_csm · разработчик, реверс‑инженер, хранитель логов</span>
                <div style="margin-top: 0.4rem; font-size: 0.9rem;">✷ посты, заметки, сниппеты ✷</div>
            </div>
        </div>

        <!-- навигация в духе архивных снапшотов -->
        <div class="nav-links">
            <a href="#" class="active">[ записи ]</a>
            <a href="#">поток</a>
            <a href="#">загрузки</a>
            <a href="#">исходный код</a>
            <a href="#">static</a>
        </div>

        <!-- СПИСОК ПОСТОВ (разработчик публикует) -->
        <h2 style="margin-bottom: 0.75rem; font-size: 1.4rem; border-left: 6px solid #3e3e3e; padding-left: 0.8rem;">🗄️ недавние публикации</h2>
        <ul class="post-list">
            <li class="post-item">
                <span class="post-date">2026‑03‑15 / 22:04</span>
                <span class="post-title"><a href="#">Отладчик внутри archive.vn: эмуляция legacy-окружений</a></span>
                <div class="post-meta">
                    <span class="tag">#reverse</span> <span class="tag">#debug</span> · 18 комментариев
                </div>
            </li>
            <li class="post-item">
                <span class="post-date">2026‑03‑12 / 13:31</span>
                <span class="post-title"><a href="#">Снимки DOM — сохраняем интерактив как в archive.today</a></span>
                <div class="post-meta">
                    <span class="tag">#js</span> <span class="tag">#archive</span> · 7 комментариев
                </div>
            </li>
            <li class="post-item">
                <span class="post-date">2026‑03‑09 / 09:17</span>
                <span class="post-title"><a href="#">Сборка cultcsm.github.io: статика и моноширинный уют</a></span>
                <div class="post-meta">
                    <span class="tag">#meta</span> <span class="tag">#github-pages</span> · 23 комментария
                </div>
            </li>
            <li class="post-item">
                <span class="post-date">2026‑03‑05 / 19:48</span>
                <span class="post-title"><a href="#">Пагинация по сниппетам: си с блэкджеком и sigaction</a></span>
                <div class="post-meta">
                    <span class="tag">#c</span> <span class="tag">#posix</span> · 5 комментариев
                </div>
            </li>
            <li class="post-item">
                <span class="post-date">2026‑03‑02 / 11:02</span>
                <span class="post-title"><a href="#">Как я поднимал этот блог на GitHub Pages (и никакого jekyll)</a></span>
                <div class="post-meta">
                    <span class="tag">#howto</span> <span class="tag">#meta</span> · 31 комментарий
                </div>
            </li>
        </ul>

        <!-- блок с «архивированием» — имитация добавления поста, как snapshot -->
        <div class="action-bar">
<span style="font-weight: bold;">✎ новый пост / сниппет:</span>
            <input type="text" placeholder="например: 2026-03-16 / рефакторинг ядра..." value="2026-03-16 / минимализм archive.vn">
            <button>сохранить снимок</button>
        </div>

        <!-- пример архивного куска кода (потому что я разработчик) -->
        <div class="pre-code">
            <span class="comment"># архивный стиль: культура минимализма</span><br>
            &gt; git clone https://github.com/cultcsm/archive-blog<br>
            &gt; cd archive-blog &amp;&amp; make serve<br>
            <span class="comment">// теперь доступно на http://cultcsm.github.io</span><br>
            &gt; curl -I https://cultcsm.github.io | grep "X-Archive-Orig"
        </div>

        <!-- ещё немного meta — сниппеты записей (прямо как сохраненные URL) -->
        <div style="margin: 2rem 0 0 0; border: 1px dashed #7a7a7a; padding: 1rem;">
            <p style="font-weight: bold; margin-bottom: 0.5rem;">⏱️ недавно добавленные / черновики:</p>
            <ul style="list-style: none;">
                <li style="display: flex; gap: 2rem;"><span style="color:#555;">00:21</span> <span>reverse-инжиниринг archive.today (capture)</span></li>
                <li style="display: flex; gap: 2rem;"><span style="color:#555;">мар 14</span> <span>культура: почему архивные сайты выглядят как из 90х</span></li>
                <li style="display: flex; gap: 2rem;"><span style="color:#555;">мар 13</span> <span>github pages + свой домен: cultcsm.github.io — бесплатно</span></li>
            </ul>
        </div>

        <!-- подвал с архивной информацией и доменом github.io -->
        <div class="footer-archive">
            <span class="capture-info">захвачено для культуры / cult csm</span>
            <span class="github-domain">cultcsm.github.io — бесплатный домен GitHub Pages</span>
            <span style="color:#2b2b2b;">зеркало: archive.vn/*</span>
        </div>

        <!-- скрытое примечание — архивные метки для поисковиков, как у archive.vn -->
        <div style="margin-top: 1rem; font-size: 0.7rem; color: #747474; border-top: 1px dotted #888; padding-top: 0.5rem; display: flex; gap: 2rem;">
            <span>🔗 original URL: https://cultcsm.github.io/devlog</span>
            <span>🕸️ 2026-03-16 21:34 @cult_csm</span>
        </div>
    </div>
    <!-- небольшой поясняющий текст для пользователя (опционально) -->
    <div style="max-width:860px; margin:1rem auto 0; font-size:0.8rem; background:transparent; color:#4e4e4e; border:1px solid #bdbdbd; padding:0.5rem 1rem;">
        ⚙️ <strong>культура csm</strong> — блог разработчика в стиле archive.vn. все посты настоящие (когда-нибудь). домен cultcsm.github.io (бесплатный, github pages).
    </div>
    </body>
    </html>
