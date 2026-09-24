[index.html](https://github.com/user-attachments/files/32612909/index.html)
<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>El Faro Digital | Periódico Digital e Independiente</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#fef2f2',
                            100: '#fee2e2',
                            600: '#dc2626',
                            700: '#b91c1c',
                            900: '#7f1d1d',
                        },
                        paper: '#fbf9f5',
                        paperDark: '#121824'
                    },
                    fontFamily: {
                        headline: ['Merriweather', 'Georgia', 'serif'],
                        sans: ['Inter', '-apple-system', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts for Editorial Aesthetics -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Merriweather:ital,wght@0,300;0,400;0,700;0,900;1,300;1,400&display=swap" rel="stylesheet">
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        body { font-family: 'Inter', sans-serif; }
        h1, h2, h3, .font-headline { font-family: 'Merriweather', Georgia, serif; }
        .line-clamp-2 { display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; }
        .line-clamp-3 { display: -webkit-box; -webkit-line-clamp: 3; -webkit-box-orient: vertical; overflow: hidden; }
    </style>
</head>
<body class="bg-paper dark:bg-paperDark text-slate-800 dark:text-slate-100 min-h-screen transition-colors duration-200">

    <!-- Top Utility Bar -->
    <div class="border-b border-slate-200 dark:border-slate-800 bg-white dark:bg-slate-900 text-xs text-slate-600 dark:text-slate-400 py-2 px-4 sm:px-8">
        <div class="max-w-7xl mx-auto flex flex-col sm:flex-row items-center justify-between gap-2">
            <div class="flex items-center gap-4">
                <span id="currentDate" class="font-medium text-slate-700 dark:text-slate-300">Cargando fecha...</span>
                <span class="hidden md:inline text-slate-300 dark:text-slate-700">•</span>
                <span class="hidden md:flex items-center gap-1.5"><i data-lucide="globe" class="w-3.5 h-3.5 text-brand-600"></i> Edición Global</span>
            </div>
            <div class="flex items-center gap-4">
                <button id="themeToggle" onclick="toggleTheme()" class="flex items-center gap-1 hover:text-brand-600 transition-colors">
                    <i data-lucide="moon" class="w-3.5 h-3.5 dark:hidden"></i>
                    <i data-lucide="sun" class="w-3.5 h-3.5 hidden dark:block"></i>
                    <span class="dark:hidden">Modo Oscuro</span>
                    <span class="hidden dark:block">Modo Claro</span>
                </button>
                <span class="text-slate-300 dark:text-slate-700">|</span>
                <button onclick="openPublishModal()" class="flex items-center gap-1 font-semibold text-brand-600 hover:text-brand-700 dark:text-brand-500">
                    <i data-lucide="plus-circle" class="w-3.5 h-3.5"></i> Publicar Artículo
                </button>
            </div>
        </div>
    </div>

    <!-- Editorial Header / Masthead -->
    <header class="border-b-4 border-slate-900 dark:border-slate-100 bg-white dark:bg-slate-900 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-8 py-6 text-center relative">
            <a href="#" onclick="filterCategory('Todas'); return false;" class="inline-block group">
                <h1 class="text-4xl sm:text-6xl md:text-7xl font-black font-headline tracking-tight text-slate-900 dark:text-white uppercase">
                    El Faro <span class="text-brand-600 dark:text-brand-500">Digital</span>
                </h1>
                <p class="text-xs sm:text-sm font-headline italic tracking-widest text-slate-500 dark:text-slate-400 mt-1 uppercase">
                    Diario Independiente de Noticias & Opinión
                </p>
            </a>
        </div>

        <!-- Navigation Bar -->
        <nav class="border-t border-b border-slate-200 dark:border-slate-800 bg-slate-50 dark:bg-slate-900/80 sticky top-0 z-30 backdrop-blur-md">
            <div class="max-w-7xl mx-auto px-4 sm:px-8 flex items-center justify-between overflow-x-auto no-scrollbar">
                <div class="flex items-center gap-1 sm:gap-2 py-3 text-xs sm:text-sm font-bold uppercase tracking-wider text-slate-700 dark:text-slate-300 whitespace-nowrap" id="categoryNav"></div>

                <div class="flex items-center gap-3 pl-4 border-l border-slate-300 dark:border-slate-700 my-2">
                    <div class="relative hidden lg:block">
                        <input type="text" id="searchInput" onkeyup="handleSearch(this.value)" placeholder="Buscar noticia..." class="pl-8 pr-3 py-1.5 text-xs rounded-full border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-800 text-slate-800 dark:text-slate-100 focus:outline-none focus:ring-2 focus:ring-brand-600 w-44 transition-all focus:w-60">
                        <i data-lucide="search" class="w-3.5 h-3.5 text-slate-400 absolute left-2.5 top-2.5"></i>
                    </div>
                    <button onclick="openPublishModal()" class="hidden sm:flex items-center gap-1.5 bg-brand-600 hover:bg-brand-700 text-white text-xs font-bold px-3 py-2 rounded-md shadow transition-colors uppercase tracking-wider">
                        <i data-lucide="pen-tool" class="w-3.5 h-3.5"></i> Publicar
                    </button>
                </div>
            </div>
        </nav>
    </header>

    <!-- Main Content Container -->
    <main class="max-w-7xl mx-auto px-4 sm:px-8 py-8">
        <!-- Mobile Search Bar -->
        <div class="block lg:hidden mb-6">
            <div class="relative">
                <input type="text" id="searchInputMobile" onkeyup="handleSearch(this.value)" placeholder="Buscar noticia..." class="w-full pl-9 pr-4 py-2.5 text-sm rounded-xl border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-800 text-slate-800 dark:text-slate-100 focus:outline-none focus:ring-2 focus:ring-brand-600 shadow-sm">
                <i data-lucide="search" class="w-4 h-4 text-slate-400 absolute left-3 top-3.5"></i>
            </div>
        </div>

        <!-- Section Title / Active Filter Indicator -->
        <div class="flex items-center justify-between mb-6 pb-2 border-b-2 border-brand-600">
            <h2 id="activeCategoryTitle" class="text-xl sm:text-2xl font-bold font-headline uppercase text-slate-900 dark:text-white flex items-center gap-2">
                <i data-lucide="newspaper" class="w-6 h-6 text-brand-600"></i> Últimas Noticias
            </h2>
            <span id="newsCountBadge" class="text-xs font-semibold px-2.5 py-1 rounded-full bg-slate-200 dark:bg-slate-800 text-slate-700 dark:text-slate-300">
                0 Noticias
            </span>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
            <!-- Main News Feed (8 cols) -->
            <div class="lg:col-span-8 space-y-8">
                <div id="featuredNewsContainer"></div>
                <div>
                    <h3 class="text-lg font-bold font-headline mb-4 pb-2 border-b border-slate-200 dark:border-slate-800 text-slate-900 dark:text-white flex items-center justify-between">
                        <span>Otras Publicaciones</span>
                        <span class="text-xs font-normal text-slate-500">Actualizado recientemente</span>
                    </h3>
                    <div id="recentNewsGrid" class="grid grid-cols-1 sm:grid-cols-2 gap-6"></div>
                </div>
            </div>

            <!-- Sidebar (4 cols) -->
            <aside class="lg:col-span-4 space-y-8">
                <div class="bg-brand-50 dark:bg-slate-900/90 border border-brand-200 dark:border-brand-900/50 rounded-xl p-5 shadow-sm">
                    <div class="flex items-center justify-between mb-4">
                        <span class="flex items-center gap-2 text-brand-700 dark:text-brand-500 font-bold text-xs uppercase tracking-wider">
                            <span class="w-2.5 h-2.5 rounded-full bg-brand-600 animate-ping"></span>
                            Última Hora
                        </span>
                        <i data-lucide="zap" class="w-4 h-4 text-brand-600"></i>
                    </div>
                    <div id="breakingNewsSidebar" class="space-y-3 divide-y divide-brand-100 dark:divide-slate-800"></div>
                </div>

                <div class="bg-gradient-to-br from-slate-900 to-slate-800 text-white rounded-xl p-6 shadow-md relative overflow-hidden">
                    <div class="relative z-10">
                        <span class="text-brand-400 text-xs font-bold uppercase tracking-wider">Periodismo Ciudadano</span>
                        <h4 class="font-headline font-bold text-xl mt-1 mb-2">¿Tienes una noticia que compartir?</h4>
                        <p class="text-slate-300 text-xs leading-relaxed mb-4">
                            Súmate como colaborador. Publica primicias, eventos o artículos de tu interés en segundos.
                        </p>
                        <button onclick="openPublishModal()" class="w-full bg-brand-600 hover:bg-brand-700 text-white font-bold py-2.5 px-4 rounded-lg text-xs uppercase tracking-wider transition-colors shadow flex items-center justify-center gap-2">
                            <i data-lucide="plus-circle" class="w-4 h-4"></i> Redactar Noticia Ahora
                        </button>
                    </div>
                    <i data-lucide="newspaper" class="w-32 h-32 text-slate-800/40 absolute -right-6 -bottom-6 pointer-events-none"></i>
                </div>
            </aside>
        </div>
    </main>

    <!-- MODAL 1: Publicar Noticia -->
    <div id="publishModal" class="fixed inset-0 bg-slate-900/70 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden overflow-y-auto">
        <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-2xl w-full max-w-2xl shadow-2xl overflow-hidden my-8 transform transition-all">
            <div class="bg-slate-900 text-white px-6 py-4 flex items-center justify-between">
                <div class="flex items-center gap-2">
                    <i data-lucide="pen-tool" class="w-5 h-5 text-brand-500"></i>
                    <h3 class="font-headline font-bold text-lg">Publicar Nueva Noticia</h3>
                </div>
                <button onclick="closePublishModal()" class="text-slate-400 hover:text-white transition-colors">
                    <i data-lucide="x" class="w-6 h-6"></i>
                </button>
            </div>

            <form id="publishForm" onsubmit="handlePublishArticle(event)" class="p-6 space-y-4 max-h-[80vh] overflow-y-auto">
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div class="sm:col-span-2">
                        <label class="block text-xs font-bold uppercase text-slate-700 dark:text-slate-300 mb-1">Título de la Noticia *</label>
                        <input type="text" id="postTitle" required placeholder="Ej: Nuevas novedades en la comunidad" class="w-full px-3 py-2.5 text-sm rounded-lg border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-800 text-slate-900 dark:text-white focus:ring-2 focus:ring-brand-600 outline-none">
                    </div>

                    <div>
                        <label class="block text-xs font-bold uppercase text-slate-700 dark:text-slate-300 mb-1">Categoría *</label>
                        <select id="postCategory" required class="w-full px-3 py-2.5 text-sm rounded-lg border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-800 text-slate-900 dark:text-white focus:ring-2 focus:ring-brand-600 outline-none">
                            <option value="Comunidad">Comunidad</option>
                            <option value="Tecnología">Tecnología</option>
                            <option value="Cultura">Cultura</option>
                            <option value="Economía">Economía</option>
                            <option value="Deportes">Deportes</option>
                            <option value="Ciencia">Ciencia</option>
                            <option value="Opinión">Opinión</option>
                        </select>
                    </div>

                    <div>
                        <label class="block text-xs font-bold uppercase text-slate-700 dark:text-slate-300 mb-1">Autor / Reportero *</label>
                        <input type="text" id="postAuthor" required placeholder="Ej: Redacción Central" class="w-full px-3 py-2.5 text-sm rounded-lg border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-800 text-slate-900 dark:text-white focus:ring-2 focus:ring-brand-600 outline-none">
                    </div>

                    <div class="sm:col-span-2">
                        <label class="block text-xs font-bold uppercase text-slate-700 dark:text-slate-300 mb-1">URL de Imagen (Opcional)</label>
                        <input type="url" id="postImage" placeholder="https://..." class="w-full px-3 py-2.5 text-sm rounded-lg border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-800 text-slate-900 dark:text-white focus:ring-2 focus:ring-brand-600 outline-none">
                    </div>

                    <div class="sm:col-span-2">
                        <label class="block text-xs font-bold uppercase text-slate-700 dark:text-slate-300 mb-1">Resumen / Copete *</label>
                        <textarea id="postSummary" rows="2" required placeholder="Breve síntesis..." class="w-full px-3 py-2 text-sm rounded-lg border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-800 text-slate-900 dark:text-white focus:ring-2 focus:ring-brand-600 outline-none"></textarea>
                    </div>

                    <div class="sm:col-span-2">
                        <label class="block text-xs font-bold uppercase text-slate-700 dark:text-slate-300 mb-1">Cuerpo Completo *</label>
                        <textarea id="postContent" rows="6" required placeholder="Escribe el desarrollo completo..." class="w-full px-3 py-2 text-sm rounded-lg border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-800 text-slate-900 dark:text-white focus:ring-2 focus:ring-brand-600 outline-none font-sans"></textarea>
                    </div>

                    <div class="sm:col-span-2 flex items-center gap-3 py-2">
                        <input type="checkbox" id="postIsBreaking" class="w-4 h-4 text-brand-600 rounded focus:ring-brand-500 border-slate-300">
                        <label for="postIsBreaking" class="text-xs font-bold uppercase text-slate-800 dark:text-slate-200 cursor-pointer flex items-center gap-1.5">
                            <i data-lucide="zap" class="w-4 h-4 text-brand-600"></i> Marcar como "Última Hora"
                        </label>
                    </div>
                </div>

                <div class="pt-4 border-t border-slate-200 dark:border-slate-800 flex justify-end gap-3">
                    <button type="button" onclick="closePublishModal()" class="px-4 py-2 text-xs font-bold uppercase tracking-wider text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 rounded-lg">Cancelar</button>
                    <button type="submit" class="px-6 py-2 bg-brand-600 hover:bg-brand-700 text-white text-xs font-bold uppercase tracking-wider rounded-lg shadow transition-colors flex items-center gap-2">
                        <i data-lucide="check" class="w-4 h-4"></i> Publicar Ahora
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL 2: Reader / Article Detail Modal -->
    <div id="readerModal" class="fixed inset-0 bg-slate-900/80 backdrop-blur-md z-50 flex items-center justify-center p-2 sm:p-4 hidden overflow-y-auto">
        <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-2xl w-full max-w-4xl shadow-2xl overflow-hidden my-6 max-h-[92vh] flex flex-col">
            <div class="px-6 py-3 border-b border-slate-200 dark:border-slate-800 flex items-center justify-between bg-slate-50 dark:bg-slate-900/90">
                <div class="flex items-center gap-2">
                    <span id="readerCategory" class="px-2.5 py-0.5 rounded-full text-xs font-bold uppercase bg-brand-100 text-brand-700 dark:bg-brand-900/40 dark:text-brand-400">Categoría</span>
                    <span id="readerBreakingBadge" class="hidden px-2.5 py-0.5 rounded-full text-xs font-bold uppercase bg-red-600 text-white flex items-center gap-1">
                        <i data-lucide="zap" class="w-3 h-3"></i> Última Hora
                    </span>
                </div>
                <button onclick="closeReaderModal()" class="p-1 rounded-full text-slate-400 hover:text-slate-800 dark:hover:text-white transition-colors">
                    <i data-lucide="x" class="w-6 h-6"></i>
                </button>
            </div>

            <div class="p-6 sm:p-10 overflow-y-auto space-y-6">
                <h1 id="readerTitle" class="text-2xl sm:text-4xl font-extrabold font-headline leading-tight text-slate-900 dark:text-white">Título de la noticia</h1>

                <div class="flex flex-wrap items-center justify-between gap-4 py-3 border-y border-slate-200 dark:border-slate-800 text-xs text-slate-500 dark:text-slate-400">
                    <div class="flex items-center gap-3">
                        <div class="w-9 h-9 rounded-full bg-slate-200 dark:bg-slate-700 flex items-center justify-center font-bold text-slate-700 dark:text-slate-200 uppercase" id="readerAuthorAvatar">EF</div>
                        <div>
                            <p class="font-bold text-slate-800 dark:text-slate-200" id="readerAuthor">Por Redacción</p>
                            <p id="readerDate">Publicado hoy</p>
                        </div>
                    </div>
                    <div class="flex items-center gap-4">
                        <span class="flex items-center gap-1"><i data-lucide="clock" class="w-4 h-4"></i> <span id="readerReadTime">3 min lectura</span></span>
                        <span class="flex items-center gap-1"><i data-lucide="eye" class="w-4 h-4"></i> <span id="readerViews">0 vistas</span></span>
                    </div>
                </div>

                <div class="rounded-xl overflow-hidden max-h-[400px] bg-slate-100 dark:bg-slate-800">
                    <img id="readerImage" src="" alt="Noticia" class="w-full h-full object-cover">
                </div>

                <p id="readerSummary" class="text-lg font-headline italic font-medium text-slate-700 dark:text-slate-300 leading-relaxed border-l-4 border-brand-600 pl-4 py-1">Resumen de la noticia...</p>

                <div id="readerContent" class="text-base sm:text-lg text-slate-800 dark:text-slate-200 leading-relaxed space-y-4 font-sans whitespace-pre-line">Cuerpo del artículo...</div>

                <!-- Comments Section -->
                <div class="pt-8 border-t border-slate-200 dark:border-slate-800">
                    <h3 class="text-xl font-bold font-headline mb-6 text-slate-900 dark:text-white flex items-center gap-2">
                        <i data-lucide="message-square" class="w-5 h-5 text-brand-600"></i> Comentarios (<span id="commentCount">0</span>)
                    </h3>

                    <form onsubmit="handleAddComment(event)" class="mb-8 bg-slate-50 dark:bg-slate-800/50 p-4 rounded-xl border border-slate-200 dark:border-slate-700">
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 mb-3">
                            <input type="text" id="commentAuthor" required placeholder="Tu nombre *" class="px-3 py-2 text-xs rounded-lg border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-800 focus:ring-2 focus:ring-brand-600 outline-none">
                        </div>
                        <textarea id="commentText" rows="3" required placeholder="Opina sobre esta noticia..." class="w-full px-3 py-2 text-xs rounded-lg border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-800 focus:ring-2 focus:ring-brand-600 outline-none mb-3"></textarea>
                        <button type="submit" class="px-4 py-2 bg-brand-600 hover:bg-brand-700 text-white text-xs font-bold uppercase rounded-lg shadow transition-colors">
                            Publicar Comentario
                        </button>
                    </form>

                    <div id="commentsList" class="space-y-4"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- Notification Toast -->
    <div id="toast" class="fixed bottom-5 right-5 bg-slate-900 text-white px-5 py-3 rounded-xl shadow-2xl z-50 flex items-center gap-3 transform translate-y-20 opacity-0 transition-all duration-300 border border-slate-700">
        <i data-lucide="check-circle" class="w-5 h-5 text-emerald-400"></i>
        <span id="toastMessage" class="text-sm font-medium">Notificación</span>
    </div>

    <script>
        const INITIAL_ARTICLES = [
            {
                id: 'art-neuro-ix',
                title: 'Últimas noticias en el grupo Neurodivergentes IX: avances, proyectos y novedades comunitarias',
                category: 'Comunidad',
                author: 'Redacción Central',
                date: new Date().toISOString(),
                summary: 'El grupo Neurodivergentes IX presenta sus actualizaciones recientes, iniciativas colaborativas y próximos espacios de integración.',
                content: `En esta nueva actualización, el grupo Neurodivergentes IX comparte sus avances más recientes en la creación de espacios inclusivos y colaborativos.\n\nDurante los últimos días, los integrantes han coordinado diferentes dinámicas de participación para fortalecer la comunidad, promoviendo el intercambio de ideas, recursos educativos y espacios de apoyo mutuo.\n\nEntre los puntos más destacados se encuentran nuevas propuestas de integración, talleres de aprendizaje y la consolidación de canales abiertos para la libre expresión y colaboración ciudadana.`,
                image: 'https://images.unsplash.com/photo-1522071820081-009f0129c71c?q=80&w=1000&auto=format&fit=crop',
                isBreaking: true,
                views: 2890,
                comments: [
                    { author: 'Mateo G.', date: 'Hace 30 minutos', text: 'Excelente noticia y grandes avances para la comunidad.' }
                ]
            }
        ];

        // State
        let articles = INITIAL_ARTICLES;
        let activeCategory = 'Todas';
        let searchQuery = '';
        let activeArticle = null;

        // Init
        document.addEventListener('DOMContentLoaded', () => {
            updateDate();
            renderCategoryNav();
            renderNews();
            lucide.createIcons();
        });

        function updateDate() {
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const today = new Date().toLocaleDateString('es-ES', options);
            document.getElementById('currentDate').textContent = today.charAt(0).toUpperCase() + today.slice(1);
        }

        function toggleTheme() {
            document.documentElement.classList.toggle('dark');
        }

        function getCategories() {
            return ['Todas', ...new Set(articles.map(a => a.category))];
        }

        function renderCategoryNav() {
            const nav = document.getElementById('categoryNav');
            const categories = getCategories();
            nav.innerHTML = categories.map(cat => `
                <button onclick="filterCategory('${cat}')" class="px-3 py-1.5 rounded-full transition-colors ${activeCategory === cat ? 'bg-brand-600 text-white font-bold' : 'hover:bg-slate-200 dark:hover:bg-slate-800'}">
                    ${cat}
                </button>
            `).join('');
        }

        function filterCategory(cat) {
            activeCategory = cat;
            renderCategoryNav();
            renderNews();
        }

        function handleSearch(query) {
            searchQuery = query.toLowerCase().trim();
            renderNews();
        }

        function getFilteredArticles() {
            return articles.filter(art => {
                const matchesCat = activeCategory === 'Todas' || art.category === activeCategory;
                const matchesSearch = !searchQuery || 
                    art.title.toLowerCase().includes(searchQuery) || 
                    art.summary.toLowerCase().includes(searchQuery) ||
                    art.content.toLowerCase().includes(searchQuery);
                return matchesCat && matchesSearch;
            });
        }

        function renderNews() {
            const filtered = getFilteredArticles();
            document.getElementById('newsCountBadge').textContent = `${filtered.length} Noticias`;
            document.getElementById('activeCategoryTitle').innerHTML = `
                <i data-lucide="newspaper" class="w-6 h-6 text-brand-600"></i>
                ${activeCategory === 'Todas' ? 'Últimas Noticias' : activeCategory}
            `;

            if (filtered.length === 0) {
                document.getElementById('featuredNewsContainer').innerHTML = `
                    <div class="text-center py-12 bg-white dark:bg-slate-900 rounded-xl border border-slate-200 dark:border-slate-800">
                        <i data-lucide="search-x" class="w-12 h-12 text-slate-400 mx-auto mb-3"></i>
                        <h3 class="font-headline font-bold text-lg">No se encontraron noticias</h3>
                        <p class="text-xs text-slate-500 mt-1">Prueba filtrando por otra categoría o búsqueda.</p>
                    </div>
                `;
                document.getElementById('recentNewsGrid').innerHTML = '';
                document.getElementById('breakingNewsSidebar').innerHTML = '';
                lucide.createIcons();
                return;
            }

            const featured = filtered.find(a => a.isBreaking) || filtered[0];
            const recent = filtered.filter(a => a.id !== featured.id);

            // Featured
            document.getElementById('featuredNewsContainer').innerHTML = `
                <div class="bg-white dark:bg-slate-900 rounded-2xl overflow-hidden border border-slate-200 dark:border-slate-800 shadow-sm hover:shadow-md transition-shadow group cursor-pointer" onclick="openReaderModal('${featured.id}')">
                    <div class="relative h-64 sm:h-80 overflow-hidden">
                        <img src="${featured.image}" alt="${featured.title}" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500">
                        <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 via-slate-950/20 to-transparent"></div>
                        <div class="absolute top-4 left-4 flex gap-2">
                            <span class="px-3 py-1 bg-brand-600 text-white text-xs font-bold uppercase rounded-full tracking-wider">${featured.category}</span>
                            ${featured.isBreaking ? '<span class="px-3 py-1 bg-red-600 text-white text-xs font-bold uppercase rounded-full tracking-wider flex items-center gap-1"><i data-lucide="zap" class="w-3 h-3"></i> Última Hora</span>' : ''}
                        </div>
                    </div>
                    <div class="p-6">
                        <h3 class="text-2xl sm:text-3xl font-extrabold font-headline text-slate-900 dark:text-white group-hover:text-brand-600 dark:group-hover:text-brand-400 transition-colors leading-tight mb-3">${featured.title}</h3>
                        <p class="text-sm text-slate-600 dark:text-slate-300 line-clamp-3 mb-4 leading-relaxed">${featured.summary}</p>
                        <div class="flex items-center justify-between text-xs text-slate-500 dark:text-slate-400 pt-3 border-t border-slate-100 dark:border-slate-800">
                            <span>Por ${featured.author}</span>
                            <span>${featured.views} vistas</span>
                        </div>
                    </div>
                </div>
            `;

            // Recent Grid
            const recentGrid = document.getElementById('recentNewsGrid');
            if (recent.length === 0) {
                recentGrid.innerHTML = `<p class="text-xs text-slate-500 italic col-span-2">No hay más publicaciones en esta sección por el momento.</p>`;
            } else {
                recentGrid.innerHTML = recent.map(art => `
                    <article class="bg-white dark:bg-slate-900 rounded-xl overflow-hidden border border-slate-200 dark:border-slate-800 shadow-sm hover:shadow-md transition-shadow group cursor-pointer flex flex-col" onclick="openReaderModal('${art.id}')">
                        <div class="relative h-44 overflow-hidden">
                            <img src="${art.image}" alt="${art.title}" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500">
                            <span class="absolute top-3 left-3 px-2.5 py-0.5 bg-slate-900/80 backdrop-blur-md text-white text-[10px] font-bold uppercase rounded-full">${art.category}</span>
                        </div>
                        <div class="p-4 flex-1 flex flex-col justify-between">
                            <div>
                                <h4 class="font-headline font-bold text-base text-slate-900 dark:text-white group-hover:text-brand-600 dark:group-hover:text-brand-400 transition-colors line-clamp-2 mb-2">${art.title}</h4>
                                <p class="text-xs text-slate-600 dark:text-slate-400 line-clamp-2 leading-relaxed mb-3">${art.summary}</p>
                            </div>
                            <div class="flex items-center justify-between text-[11px] text-slate-400 pt-2 border-t border-slate-100 dark:border-slate-800">
                                <span>Por ${art.author}</span>
                                <span>${art.views} vistas</span>
                            </div>
                        </div>
                    </article>
                `).join('');
            }

            renderSidebarWidgets();
            lucide.createIcons();
        }

        function renderSidebarWidgets() {
            const breaking = articles.filter(a => a.isBreaking);
            const breakingSidebar = document.getElementById('breakingNewsSidebar');
            
            if (breaking.length === 0) {
                breakingSidebar.innerHTML = `<p class="text-xs text-slate-500 py-2">No hay alertas de última hora en este momento.</p>`;
            } else {
                breakingSidebar.innerHTML = breaking.map(item => `
                    <div class="pt-3 first:pt-0 cursor-pointer group" onclick="openReaderModal('${item.id}')">
                        <span class="text-[10px] font-bold uppercase text-brand-600 dark:text-brand-400">${item.category}</span>
                        <h5 class="text-xs font-bold font-headline text-slate-900 dark:text-white group-hover:text-brand-600 dark:group-hover:text-brand-400 transition-colors line-clamp-2 mt-0.5">${item.title}</h5>
                    </div>
                `).join('');
            }
        }

        // Modals & Interactivity
        function openPublishModal() {
            document.getElementById('publishModal').classList.remove('hidden');
        }

        function closePublishModal() {
            document.getElementById('publishModal').classList.add('hidden');
            document.getElementById('publishForm').reset();
        }

        function handlePublishArticle(e) {
            e.preventDefault();
            const newArt = {
                id: 'art-' + Date.now(),
                title: document.getElementById('postTitle').value.trim(),
                category: document.getElementById('postCategory').value,
                author: document.getElementById('postAuthor').value.trim(),
                date: new Date().toISOString(),
                summary: document.getElementById('postSummary').value.trim(),
                content: document.getElementById('postContent').value.trim(),
                image: document.getElementById('postImage').value.trim() || 'https://images.unsplash.com/photo-1504711434969-e33886168f5c?q=80&w=1000&auto=format&fit=crop',
                isBreaking: document.getElementById('postIsBreaking').checked,
                views: 1,
                comments: []
            };

            articles.unshift(newArt);
            closePublishModal();
            renderCategoryNav();
            renderNews();
            showToast('¡Artículo publicado con éxito!');
        }

        function openReaderModal(id) {
            const art = articles.find(a => a.id === id);
            if (!art) return;
            
            activeArticle = art;
            art.views += 1;

            document.getElementById('readerCategory').textContent = art.category;
            
            const breakingBadge = document.getElementById('readerBreakingBadge');
            if (art.isBreaking) {
                breakingBadge.classList.remove('hidden');
            } else {
                breakingBadge.classList.add('hidden');
            }

            document.getElementById('readerTitle').textContent = art.title;
            document.getElementById('readerAuthor').textContent = `Por ${art.author}`;
            document.getElementById('readerAuthorAvatar').textContent = art.author.slice(0, 2).toUpperCase();
            document.getElementById('readerDate').textContent = new Date(art.date).toLocaleDateString('es-ES', { day: 'numeric', month: 'short', year: 'numeric' });
            
            const wordCount = art.content.split(/\s+/).length;
            const readMinutes = Math.max(1, Math.ceil(wordCount / 200));
            document.getElementById('readerReadTime').textContent = `${readMinutes} min lectura`;
            document.getElementById('readerViews').textContent = `${art.views} vistas`;
            
            document.getElementById('readerImage').src = art.image;
            document.getElementById('readerSummary').textContent = art.summary;
            document.getElementById('readerContent').textContent = art.content;

            renderComments();
            document.getElementById('readerModal').classList.remove('hidden');
            renderNews();
        }

        function closeReaderModal() {
            document.getElementById('readerModal').classList.add('hidden');
            activeArticle = null;
        }

        function renderComments() {
            if (!activeArticle) return;
            document.getElementById('commentCount').textContent = activeArticle.comments.length;
            const list = document.getElementById('commentsList');

            if (activeArticle.comments.length === 0) {
                list.innerHTML = `<p class="text-xs text-slate-400 italic">Aún no hay comentarios. Sé el primero en opinar.</p>`;
                return;
            }

            list.innerHTML = activeArticle.comments.map(c => `
                <div class="bg-slate-50 dark:bg-slate-800/40 p-3 rounded-lg border border-slate-100 dark:border-slate-800 text-xs">
                    <div class="flex items-center justify-between font-bold text-slate-800 dark:text-slate-200 mb-1">
                        <span>${c.author}</span>
                        <span class="text-[10px] font-normal text-slate-400">${c.date}</span>
                    </div>
                    <p class="text-slate-600 dark:text-slate-300 leading-relaxed">${c.text}</p>
                </div>
            `).join('');
        }

        function handleAddComment(e) {
            e.preventDefault();
            if (!activeArticle) return;

            const author = document.getElementById('commentAuthor').value.trim();
            const text = document.getElementById('commentText').value.trim();

            if (author && text) {
                activeArticle.comments.push({
                    author: author,
                    date: 'Hace un momento',
                    text: text
                });
                document.getElementById('commentAuthor').value = '';
                document.getElementById('commentText').value = '';
                renderComments();
                showToast('Comentario añadido.');
            }
        }

        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toastMessage').textContent = msg;
            toast.classList.remove('translate-y-20', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>
