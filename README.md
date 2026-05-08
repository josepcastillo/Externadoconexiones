# Externadoconexiones
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Externado Conexiones | FAE</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        :root { --externado-green: #00A99D; --externado-blue: #2E3192; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: #000; color: #fff; overflow-x: hidden; }
        .gradient-text { background: linear-gradient(135deg, #00FFCC 0%, #00A99D 50%, #2E3192 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .login-card { background: rgba(10, 10, 10, 0.8); border: 1px solid rgba(0, 169, 157, 0.2); box-shadow: 0 0 40px rgba(0, 169, 157, 0.05); }
        .role-card { background: rgba(20, 20, 20, 0.6); border: 1px solid rgba(255, 255, 255, 0.1); transition: all 0.3s ease; cursor: pointer; }
        .role-card.selected { border-color: var(--externado-green); background: rgba(0, 169, 157, 0.1); transform: scale(1.02); }
        .btn-externado { background: linear-gradient(90deg, #00A99D, #2E3192); transition: all 0.3s ease; }
        .btn-externado:hover { opacity: 0.9; transform: translateY(-2px); }
        .hidden-step { display: none; }
        .visible-step { display: block; animation: fadeIn 0.5s forwards; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        
        .profile-dropdown { display: none; position: absolute; top: 100%; right: 0; width: 340px; background: rgba(10, 10, 10, 0.98); border: 1px solid rgba(0, 169, 157, 0.4); border-radius: 1.5rem; backdrop-filter: blur(25px); z-index: 100; margin-top: 0.75rem; }
        .profile-dropdown.active { display: block; }
        
        .calc-input { background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1); border-radius: 12px; padding: 10px; color: white; width: 100%; text-align: center; font-weight: 800; }
        .semester-btn { background: rgba(30,30,30,0.6); border: 1px solid rgba(255,255,255,0.1); transition: 0.2s; white-space: nowrap; }
        .semester-btn.active { background: #00A99D; color: white; border-color: #00FFCC; }
        
        /* Óvalos de Estado */
        .status-oval { border-radius: 9999px; padding: 4px 12px; font-size: 9px; font-weight: 900; text-transform: uppercase; border: 1px solid currentColor; display: flex; align-items: center; justify-content: center; min-width: 85px; }
        .bg-malo { color: #ef4444; background-color: rgba(239, 68, 68, 0.15); }
        .bg-medio { color: #f59e0b; background-color: rgba(245, 158, 11, 0.15); }
        .bg-bueno { color: #10b981; background-color: rgba(16, 185, 129, 0.15); }
        
        .chat-bubble-me { background: linear-gradient(135deg, #00A99D, #2E3192); border-radius: 1.2rem 1.2rem 0.2rem 1.2rem; align-self: flex-end; }
        .chat-bubble-them { background: rgba(255,255,255,0.1); border-radius: 1.2rem 1.2rem 1.2rem 0.2rem; align-self: flex-start; }
        .typing-indicator { font-size: 8px; color: #00A99D; font-weight: 800; text-transform: uppercase; letter-spacing: 2px; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.4; } }
        .custom-scrollbar::-webkit-scrollbar { width: 4px; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #00A99D; border-radius: 10px; }
    </style>
</head>
<body class="min-h-screen flex flex-col items-center p-4 md:p-6">

    <header id="header-section" class="w-full max-w-5xl text-center space-y-0 pt-8 mb-12">
        <h1 class="flex flex-col leading-none font-extrabold tracking-tighter italic">
            <span class="text-6xl md:text-8xl text-white uppercase">Externado</span>
            <span class="text-6xl md:text-8xl gradient-text -mt-2 md:-mt-4 uppercase">Conexiones</span>
        </h1>
        <p class="text-zinc-500 text-[11px] md:text-sm font-medium tracking-[0.5em] uppercase mt-6">Gestión Inteligente FAE - Versión 2026</p>
    </header>

    <main class="w-full max-w-4xl">
        <div class="login-card p-6 md:p-10 rounded-[3rem] backdrop-blur-xl relative overflow-hidden">
            
            <div id="step1" class="visible-step">
                <h2 class="text-xl font-semibold mb-8 border-l-4 border-[#00A99D] pl-4 uppercase italic">Identifícate</h2>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-8">
                    <div onclick="selectRole('aprendiz')" id="role-aprendiz" class="role-card p-8 rounded-3xl flex flex-col items-center gap-4">
                        <div class="w-12 h-12 bg-white/5 rounded-full flex items-center justify-center">
                            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="text-white"><path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/><path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/></svg>
                        </div>
                        <span class="font-black text-xs uppercase tracking-widest text-zinc-400">Soy Aprendiz</span>
                    </div>
                    <div onclick="selectRole('monitor')" id="role-monitor" class="role-card p-8 rounded-3xl flex flex-col items-center gap-4">
                        <div class="w-12 h-12 bg-white/5 rounded-full flex items-center justify-center">
                            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="text-white"><path d="M12 2v8"/><path d="m4.93 10.93 1.41 1.41"/><path d="M2 18h2"/><path d="M20 18h2"/><path d="m19.07 10.93-1.41 1.41"/><path d="M22 22H2"/><path d="m8 22 4-10 4 10"/></svg>
                        </div>
                        <span class="font-black text-xs uppercase tracking-widest text-zinc-400">Soy Monitor</span>
                    </div>
                </div>
                <button onclick="goToStep2()" id="nextBtn" disabled class="w-full bg-zinc-800 text-zinc-600 font-black py-5 rounded-2xl cursor-not-allowed uppercase text-[10px] tracking-[0.3em]">Continuar</button>
            </div>

            <div id="step2" class="hidden-step">
                <div class="mb-8">
                    <button onclick="transitionSteps('step2', 'step1')" class="text-[10px] font-black text-zinc-500 uppercase flex items-center gap-2 hover:text-white transition-colors">
                        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><polyline points="15 18 9 12 15 6"></polyline></svg>
                        Atrás
                    </button>
                    <h2 id="login-title" class="text-3xl font-black text-white italic uppercase mt-4">Acceso Usuarios</h2>
                </div>
                <form id="loginForm" class="space-y-4">
                    <div class="space-y-1">
                        <label class="text-[9px] font-black text-zinc-500 uppercase ml-2">Usuario</label>
                        <input type="text" id="userIdInput" required placeholder="Tu nombre" class="w-full bg-zinc-900 border border-zinc-800 rounded-2xl px-5 py-4 text-white focus:outline-none focus:border-[#00A99D]">
                    </div>
                    <div class="space-y-1">
                        <label class="text-[9px] font-black text-zinc-500 uppercase ml-2">Contraseña</label>
                        <input type="password" id="userPassInput" required placeholder="••••••••" class="w-full bg-zinc-900 border border-zinc-800 rounded-2xl px-5 py-4 text-white focus:outline-none focus:border-[#00A99D]">
                    </div>
                    <button type="submit" class="w-full btn-externado text-white font-black py-5 rounded-2xl uppercase text-[10px] tracking-widest shadow-xl shadow-teal-900/20">Iniciar Sesión</button>
                </form>
            </div>

            <div id="step3-panel" class="hidden-step space-y-8">
                <div class="flex flex-col md:flex-row justify-between items-center bg-zinc-900/40 p-6 rounded-[2.5rem] border border-zinc-800 gap-6">
                    <div>
                        <p id="panel-role-label" class="text-[9px] uppercase tracking-widest text-[#00A99D] font-black">ESTADO: ACTIVO</p>
                        <h2 class="text-2xl font-black text-white italic uppercase mt-1">HOLA, <span id="displayUserName" class="gradient-text uppercase">USUARIO</span></h2>
                    </div>
                    <div class="flex items-center gap-4">
                        <button onclick="toggleRequestsModal()" class="p-4 bg-zinc-800 rounded-2xl relative group hover:bg-[#00A99D] transition-all">
                            <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="text-white"><path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"></path><path d="M13.73 21a2 2 0 0 1-3.46 0"></path></svg>
                            <div id="req-count-badge" class="absolute -top-2 -right-2 bg-red-500 text-[10px] font-black w-6 h-6 flex items-center justify-center rounded-full border-2 border-black">0</div>
                        </button>
                        <div class="relative">
                            <button onclick="toggleProfileMenu()" id="profile-trigger" class="w-14 h-14 rounded-full bg-gradient-to-br from-[#00A99D] to-[#2E3192] flex items-center justify-center p-[3px]">
                                <div class="w-full h-full bg-black rounded-full flex items-center justify-center">
                                    <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
                                </div>
                            </button>
                            <!-- DROPDOWN DE PERFIL -->
                            <div id="profile-menu" class="profile-dropdown shadow-2xl overflow-hidden">
                                <div class="p-6 border-b border-zinc-800 bg-zinc-900/50">
                                    <p class="text-[10px] font-black text-[#00A99D] uppercase">Tu Perfil FAE</p>
                                    <h4 id="menu-user-name" class="text-sm font-bold text-white uppercase mt-1">Usuario</h4>
                                </div>
                                <div id="profile-indicators-container" class="p-6 space-y-6 max-h-[500px] overflow-y-auto custom-scrollbar">
                                    
                                    <!-- CALCULADORA DE NOTAS (4 CORTES) -->
                                    <div class="space-y-4">
                                        <p class="text-[9px] font-black text-zinc-500 uppercase tracking-widest">Calculadora de Notas (Cortes al 25%)</p>
                                        <div class="grid grid-cols-2 gap-2">
                                            <input type="number" id="c1" step="0.1" min="0" max="5" placeholder="C1 (25%)" oninput="updateRequiredGrade()" class="calc-input text-xs">
                                            <input type="number" id="c2" step="0.1" min="0" max="5" placeholder="C2 (25%)" oninput="updateRequiredGrade()" class="calc-input text-xs">
                                            <input type="number" id="c3" step="0.1" min="0" max="5" placeholder="C3 (25%)" oninput="updateRequiredGrade()" class="calc-input text-xs">
                                            <input type="number" id="c4" step="0.1" min="0" max="5" placeholder="C4 (25%)" oninput="updateRequiredGrade()" class="calc-input text-xs">
                                        </div>
                                        <div class="bg-zinc-800/50 rounded-xl p-3 flex flex-col justify-center items-center border border-[#00A99D]/30">
                                            <span id="calc-label" class="text-[7px] text-[#00A99D] font-black uppercase">Para pasar con 3.0 necesitas</span>
                                            <span id="grade-needed" class="text-lg font-black text-white italic">3.0</span>
                                        </div>
                                    </div>

                                    <!-- INDICADORES DE RENDIMIENTO (OVALOS) -->
                                    <div class="space-y-4 pt-4 border-t border-zinc-800">
                                        <p id="stats-label" class="text-[9px] font-black text-zinc-500 uppercase tracking-widest">Resumen de Monitorías</p>
                                        <div id="stats-list" class="space-y-3">
                                            <!-- Stats dinámicos con óvalos -->
                                        </div>
                                    </div>
                                </div>
                                <div class="p-4 border-t border-zinc-800">
                                    <button onclick="location.reload()" class="w-full text-left p-4 text-red-500 text-[10px] font-black uppercase hover:bg-red-500/5 rounded-2xl transition-all text-center">Cerrar Sesión</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div id="feed-container" class="space-y-6">
                    <h3 class="text-[10px] font-black text-zinc-500 uppercase tracking-[0.3em] flex items-center gap-3">
                        <span class="w-8 h-[1px] bg-zinc-800"></span> Historias de Éxito FAE
                    </h3>
                    <div id="social-feed" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4"></div>
                </div>

                <!-- SECCIÓN ACADÉMICA -->
                <div id="academic-section" class="hidden space-y-6">
                    <h3 id="academic-title" class="text-[10px] font-black text-zinc-500 uppercase tracking-[0.3em] flex items-center gap-3">
                        <span class="w-8 h-[1px] bg-zinc-800"></span> Plan de Estudios por Semestre
                    </h3>
                    <div id="semester-tabs" class="flex gap-2 overflow-x-auto pb-4 scrollbar-hide"></div>
                    <div id="subjects-grid" class="grid grid-cols-1 sm:grid-cols-2 gap-4"></div>
                    
                    <div id="casting-view" class="hidden space-y-6">
                        <div class="flex items-center justify-between">
                            <button onclick="backToSubjects()" class="text-[9px] font-black text-[#00A99D] uppercase flex items-center gap-2">
                                <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><polyline points="15 18 9 12 15 6"></polyline></svg>
                                Volver a Materias
                            </button>
                            <h4 id="casting-title" class="text-lg font-black text-white italic uppercase">LISTADO</h4>
                        </div>
                        <div id="casting-list" class="space-y-4"></div>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <div id="chat-modal" class="fixed inset-0 bg-black/95 z-[600] hidden flex items-center justify-center p-4">
        <div class="bg-zinc-900 w-full max-w-md h-[85vh] rounded-[3rem] border border-zinc-800 flex flex-col overflow-hidden">
            <div class="p-6 bg-zinc-800/50 border-b border-zinc-700 flex items-center justify-between">
                <div class="flex items-center gap-3">
                    <div id="chat-avatar" class="w-10 h-10 bg-gradient-to-br from-[#00A99D] to-[#2E3192] rounded-full flex items-center justify-center font-black text-sm">?</div>
                    <div>
                        <h4 id="chat-with-name" class="text-sm font-black text-white uppercase">Chat</h4>
                        <p id="chat-subject" class="text-[8px] text-[#00A99D] font-black uppercase">Consulta Académica</p>
                    </div>
                </div>
                <button onclick="closeChat()" class="text-zinc-500 hover:text-white">
                    <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
                </button>
            </div>
            <div id="chat-messages-container" class="flex-1 p-6 overflow-y-auto custom-scrollbar space-y-4 flex flex-col"></div>
            <div id="typing-status" class="px-6 py-2 hidden">
                <span class="typing-indicator italic">Escribiendo respuesta coherente...</span>
            </div>
            <div class="p-6 border-t border-zinc-800 bg-black/20">
                <form id="chatForm" class="flex gap-2">
                    <input type="text" id="chatInput" placeholder="Escribe un mensaje..." class="flex-1 bg-zinc-900 border border-zinc-800 rounded-2xl px-5 py-3 text-sm focus:outline-none focus:border-[#00A99D]">
                    <button type="submit" class="w-12 h-12 btn-externado rounded-2xl flex items-center justify-center">
                        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="3"><line x1="22" y1="2" x2="11" y2="13"></line><polygon points="22 2 15 22 11 13 2 9 22 2"></polygon></svg>
                    </button>
                </form>
            </div>
        </div>
    </div>

    <div id="requests-modal" class="fixed inset-0 bg-black/90 backdrop-blur-md z-[500] hidden flex items-center justify-center p-4">
        <div class="bg-zinc-900 border border-zinc-800 w-full max-w-lg rounded-[3rem] p-8 space-y-6 relative max-h-[90vh] flex flex-col">
            <button onclick="toggleRequestsModal()" class="absolute top-8 right-8 text-zinc-500 hover:text-white">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
            </button>
            <h3 class="text-2xl font-black text-white italic uppercase">Bandeja de Mensajes</h3>
            <div id="requests-list" class="flex-1 overflow-y-auto custom-scrollbar space-y-4"></div>
        </div>
    </div>

    <script>
        const subjectsData = {
            1: ["Pensamiento Estratégico", "Liderazgo Personal", "Fundamentos de Adm. y Org.", "Tecnología y Sociedad", "Fundamentos de Matemáticas", "Introducción a la Economía", "Ética y Comp. Ciudadanas", "Pensamiento Crítico I", "Idioma 1"],
            2: ["Fund. Estrategia y Prospectiva", "Análisis Organizacional", "Contabilidad Gerencial", "Métodos Cuantitativos 1", "Microeconomía", "Instituciones Políticas", "Electiva I", "DECAPE", "Idioma 2"],
            3: ["Propuestas Gerenciales", "Fundamentos de Marketing", "Comportamiento Org.", "Desarrollo Sostenible", "Planeación Financiera y Costos", "Sistemas de Información", "Métodos Cuantitativos 2", "Política y Entorno Macro.", "Idioma 3"],
            4: ["Prospectiva", "Liderazgo de Equipos", "Investigación de Mercados", "Producción de Bienes y Serv.", "Decisiones de Inv. y Finan.", "Estadística y Programación", "Pensamiento Crítico II", "Seminario Legis. Comercial", "Idioma 4"],
            5: ["Comunicaciones Integradas", "Gestión Humana", "Logística", "Creatividad", "Mercados Financieros", "Modelos de Optimización I", "Diagnóstico Sectorial y Reg.", "Electiva II", "Seminario Legis. Laboral", "Idioma 5"],
            6: ["Dirección Estratégica", "Gerencia de Mercadeo", "Gestión del Cambio", "Innovación y Mod. Negocio", "Gerencia Financiera", "Formulac. y Des. Proyectos", "Modelos de Optimización II", "Seminario Legis. Tributaria", "Idioma 6"],
            7: ["Casos Empresariales", "Liderazgo Directivo", "Habilidades Profesionales", "Simuladores Gerenciales", "Taller Primeros Pasos RSE", "Taller de Emprendimiento", "Negocios Internacionales", "Plan Padrinos"],
            8: ["Énfasis 1", "Énfasis 2", "Electiva III"],
            9: ["Opción de Grado"]
        };

        const monitorProfiles = [
            { id: 'm1', name: 'Laura Gómez', init: 'L', stars: 5, bio: 'Especialista en Finanzas.', grade: '4.9' },
            { id: 'm2', name: 'Andrés Felipe', init: 'A', stars: 4, bio: 'Experto en Microeconomía.', grade: '4.7' },
            { id: 'm3', name: 'Valentina Soto', init: 'V', stars: 5, bio: 'Marketing y RSE.', grade: '4.8' },
            { id: 'm4', name: 'Mateo Rojas', init: 'M', stars: 4, bio: 'Cuantitativos y Cálculo.', grade: '4.5' },
            { id: 'm5', name: 'Camila Pardo', init: 'C', stars: 5, bio: 'Liderazgo y Equipos.', grade: '4.9' }
        ];

        const learnerProfiles = [
            { id: 'l1', name: 'Santiago Bernal', init: 'S', need: 'Dificultad con modelos de optimización.', avg: '2.8' },
            { id: 'l2', name: 'Mariana Duarte', init: 'M', need: 'Dudas sobre utilidad marginal.', avg: '3.1' },
            { id: 'l3', name: 'Kevin Espitia', init: 'K', need: 'Análisis de estados financieros.', avg: '2.5' },
            { id: 'l4', name: 'Isabella Ruiz', init: 'I', need: 'Repaso examen final.', avg: '3.4' },
            { id: 'l5', name: 'Nicolás Silva', init: 'N', need: 'Tablas dinámicas.', avg: '2.9' },
            { id: 'l6', name: 'Paula Méndez', init: 'P', need: 'Estrategia Prospectiva.', avg: '3.8' },
            { id: 'l7', name: 'Diego Torres', init: 'D', need: 'Estadística avanzada.', avg: '2.4' },
            { id: 'l8', name: 'Gabriela Vega', init: 'G', need: 'Legislación comercial.', avg: '4.0' },
            { id: 'l9', name: 'Javier Castro', init: 'J', need: 'Liderazgo Situacional.', avg: '3.2' },
            { id: 'l10', name: 'Sofía Rincón', init: 'S', need: 'Formulación de proyectos.', avg: '3.0' }
        ];

        let currentRole = '';
        let currentUser = '';
        let activeChatId = null;
        let systemRequests = JSON.parse(localStorage.getItem('fae_chats_v6')) || [];

        window.selectRole = (role) => {
            currentRole = role;
            document.querySelectorAll('.role-card').forEach(c => c.classList.toggle('selected', c.id === `role-${role}`));
            const btn = document.getElementById('nextBtn');
            btn.disabled = false;
            btn.className = "w-full btn-externado text-white font-black py-5 rounded-2xl cursor-pointer uppercase text-[10px] tracking-[0.3em]";
        };

        window.goToStep2 = () => transitionSteps('step1', 'step2');

        window.transitionSteps = (outId, inId) => {
            document.getElementById(outId).classList.replace('visible-step', 'hidden-step');
            document.getElementById(inId).classList.replace('hidden-step', 'visible-step');
        };

        window.toggleProfileMenu = () => document.getElementById('profile-menu').classList.toggle('active');

        window.updateRequiredGrade = () => {
            const c1 = parseFloat(document.getElementById('c1').value) || 0;
            const c2 = parseFloat(document.getElementById('c2').value) || 0;
            const c3 = parseFloat(document.getElementById('c3').value) || 0;
            const c4Input = document.getElementById('c4');
            const c4 = parseFloat(c4Input.value);
            
            const display = document.getElementById('grade-needed');
            const label = document.getElementById('calc-label');

            if (!isNaN(c4)) {
                // Cálculo de promedio final si están las 4 notas
                const final = (c1 + c2 + c3 + c4) / 4;
                label.innerText = "Promedio Final (Aproximado)";
                display.innerText = final.toFixed(2);
                display.className = final >= 3 ? "text-lg font-black text-emerald-400 italic" : "text-lg font-black text-red-500 italic";
            } else {
                // Cálculo de cuánto falta para el 3.0
                const needed = 12 - (c1 + c2 + c3);
                label.innerText = "Para pasar con 3.0 necesitas en C4";
                
                if (needed <= 0) {
                    display.innerText = "¡YA PASASTE!";
                    display.className = "text-lg font-black text-emerald-400 italic";
                } else if (needed > 5) {
                    display.innerText = needed.toFixed(1) + " (Imposible)";
                    display.className = "text-lg font-black text-red-500 italic";
                } else {
                    display.innerText = needed.toFixed(1);
                    display.className = "text-lg font-black text-white italic";
                }
            }
        };

        window.renderIndicators = () => {
            const list = document.getElementById('stats-list');
            const label = document.getElementById('stats-label');
            
            if (currentRole === 'monitor') {
                label.innerText = 'Rendimiento de Monitorías';
                const stats = [
                    { name: "Microeconomía", rate: "30%", status: "Mala", class: "bg-malo" },
                    { name: "Pensamiento Estratégico", rate: "80%", status: "Excelente", class: "bg-bueno" },
                    { name: "Métodos Cuantitativos", rate: "50%", status: "Regular", class: "bg-medio" }
                ];

                list.innerHTML = stats.map(s => `
                    <div class="bg-black/40 p-3 rounded-xl border border-white/5 flex items-center justify-between">
                        <div>
                            <h5 class="text-[10px] font-bold text-white uppercase">${s.name}</h5>
                            <p class="text-[8px] text-zinc-500 uppercase font-black">Porcentaje: ${s.rate}</p>
                        </div>
                        <div class="status-oval ${s.class}">${s.status}</div>
                    </div>
                `).join('');
            } else {
                label.innerText = 'Estado de tus Materias';
                const stats = [
                    { name: "Introducción Econ.", status: "Aprobada", class: "bg-bueno" },
                    { name: "Matemáticas F.", status: "En Proceso", class: "bg-medio" },
                    { name: "Idioma 1", status: "No Aprobada", class: "bg-malo" }
                ];

                list.innerHTML = stats.map(s => `
                    <div class="bg-black/40 p-3 rounded-xl border border-white/5 flex items-center justify-between">
                        <h5 class="text-[10px] font-bold text-white uppercase">${s.name}</h5>
                        <div class="status-oval ${s.class}">${s.status}</div>
                    </div>
                `).join('');
            }
        };

        window.setSemester = (num) => {
            const tabs = document.getElementById('semester-tabs');
            tabs.innerHTML = Object.keys(subjectsData).map(s => `
                <button onclick="setSemester(${s})" class="semester-btn px-6 py-3 rounded-xl text-[10px] font-black uppercase ${s == num ? 'active' : ''}">Semestre ${s}</button>
            `).join('');
            
            const grid = document.getElementById('subjects-grid');
            grid.innerHTML = subjectsData[num].map(sub => `
                <div onclick="openCasting('${sub}')" class="bg-zinc-900/40 p-5 rounded-2xl border border-white/5 hover:border-[#00A99D] cursor-pointer transition-all">
                    <h4 class="text-sm font-bold text-white">${sub}</h4>
                    <p class="text-[8px] text-zinc-500 mt-1 uppercase font-black">${currentRole === 'monitor' ? 'Ver Estudiantes' : 'Ver Monitores'}</p>
                </div>
            `).join('');
        };

        window.openCasting = (subject) => {
            document.getElementById('subjects-grid').classList.add('hidden');
            document.getElementById('semester-tabs').classList.add('hidden');
            document.getElementById('casting-view').classList.remove('hidden');
            document.getElementById('casting-title').innerText = subject;
            
            const list = document.getElementById('casting-list');
            if (currentRole === 'aprendiz') {
                list.innerHTML = monitorProfiles.map(m => `
                    <div class="bg-zinc-900/60 p-6 rounded-[2rem] border border-white/5 flex flex-col md:flex-row gap-6 items-center">
                        <div class="w-16 h-16 rounded-full bg-gradient-to-br from-[#00A99D] to-[#2E3192] flex items-center justify-center text-xl font-black">${m.init}</div>
                        <div class="flex-1 text-center md:text-left">
                            <h5 class="text-lg font-black uppercase">${m.name}</h5>
                            <p class="text-xs text-zinc-400 italic">"${m.bio}"</p>
                            <span class="text-[9px] text-[#00A99D] font-bold">HISTÓRICO: ${m.grade} | ${'★'.repeat(m.stars)}</span>
                        </div>
                        <button onclick="startChat('${m.name}', '${subject}')" class="btn-externado px-8 py-4 rounded-2xl text-[10px] font-black uppercase">Chatear</button>
                    </div>
                `).join('');
            } else {
                list.innerHTML = learnerProfiles.map(l => `
                    <div class="bg-zinc-900/60 p-6 rounded-[2rem] border border-white/5 flex flex-col md:flex-row gap-6 items-center">
                        <div class="w-14 h-14 rounded-full bg-zinc-800 flex items-center justify-center text-lg font-black text-[#00A99D]">${l.init}</div>
                        <div class="flex-1 text-center md:text-left">
                            <h5 class="text-lg font-black uppercase">${l.name}</h5>
                            <p class="text-xs text-zinc-400 italic">"${l.need}"</p>
                            <span class="text-[9px] text-red-500 font-bold uppercase">PROMEDIO: ${l.avg}</span>
                        </div>
                        <button onclick="startChat('${l.name}', '${subject}')" class="btn-externado px-8 py-4 rounded-2xl text-[10px] font-black uppercase">Ayudar</button>
                    </div>
                `).join('');
            }
        };

        window.backToSubjects = () => {
            document.getElementById('casting-view').classList.add('hidden');
            document.getElementById('subjects-grid').classList.remove('hidden');
            document.getElementById('semester-tabs').classList.remove('hidden');
        };

        window.startChat = (targetName, subject) => {
            const existing = systemRequests.find(r => (r.u1 === currentUser || r.u2 === currentUser) && (r.u1 === targetName || r.u2 === targetName) && r.subject === subject);
            if (existing) {
                openChat(existing.id);
            } else {
                const newId = Date.now();
                systemRequests.push({
                    id: newId, u1: currentUser, u2: targetName, subject: subject,
                    messages: [{ sender: 'System', text: `Hola. Estoy listo para coordinar la monitoría de ${subject}.` }]
                });
                localStorage.setItem('fae_chats_v6', JSON.stringify(systemRequests));
                openChat(newId);
            }
        };

        window.openChat = (chatId) => {
            activeChatId = chatId;
            const req = systemRequests.find(r => r.id === chatId);
            document.getElementById('chat-modal').classList.remove('hidden');
            document.getElementById('chat-with-name').innerText = req.u1 === currentUser ? req.u2 : req.u1;
            document.getElementById('chat-subject').innerText = req.subject;
            renderMessages();
        };

        window.closeChat = () => { document.getElementById('chat-modal').classList.add('hidden'); activeChatId = null; };

        window.renderMessages = () => {
            const req = systemRequests.find(r => r.id === activeChatId);
            const cont = document.getElementById('chat-messages-container');
            cont.innerHTML = req.messages.map(m => `
                <div class="${m.sender === currentUser ? 'chat-bubble-me' : 'chat-bubble-them'} p-4 max-w-[80%] text-sm shadow-lg">
                    <p class="text-[9px] opacity-60 font-black uppercase mb-1">${m.sender}</p>
                    <p>${m.text}</p>
                </div>
            `).join('');
            cont.scrollTop = cont.scrollHeight;
        };

        // IA Coherente (Gemini Simulation)
        async function getAIResponse(chatHistory, role) {
            return new Promise(resolve => {
                setTimeout(() => {
                    const pool = role === 'monitor' ? 
                        ["Me parece bien. ¿Dónde nos encontramos?", "Sí, esa parte de los 4 cortes me tiene confundido.", "Gracias monitor, nos vemos mañana.", "¡Entendido! Llevaré mis apuntes."] :
                        ["Hola, claro que puedo ayudarte.", "Revisemos los temas del segundo corte.", "Nos vemos en el salón H-102.", "Recuerda que para pasar necesitas un 3.0."];
                    resolve(pool[Math.floor(Math.random() * pool.length)]);
                }, 1500);
            });
        }

        window.toggleRequestsModal = () => {
            const modal = document.getElementById('requests-modal');
            modal.classList.toggle('hidden');
            if (!modal.classList.contains('hidden')) {
                const list = document.getElementById('requests-list');
                const myChats = systemRequests.filter(r => r.u1 === currentUser || r.u2 === currentUser);
                list.innerHTML = myChats.map(r => `
                    <div onclick="toggleRequestsModal(); openChat(${r.id})" class="p-6 bg-zinc-800/50 rounded-2xl cursor-pointer hover:bg-[#00A99D]/20 border border-white/5 mb-4">
                        <div class="flex justify-between items-center">
                            <h5 class="font-black text-white uppercase text-sm">${r.u1 === currentUser ? r.u2 : r.u1}</h5>
                            <span class="text-[9px] font-black text-[#00A99D] uppercase">${r.subject}</span>
                        </div>
                    </div>
                `).join(myChats.length ? '' : '<p class="text-center text-zinc-600 font-black uppercase text-xs py-10">Sin chats activos</p>');
            }
        };

        document.addEventListener('DOMContentLoaded', () => {
            document.getElementById('loginForm').addEventListener('submit', (e) => {
                e.preventDefault();
                currentUser = document.getElementById('userIdInput').value.trim();
                document.getElementById('displayUserName').innerText = currentUser;
                document.getElementById('menu-user-name').innerText = currentUser;
                
                transitionSteps('step2', 'step3-panel');
                document.getElementById('header-section').classList.add('hidden');
                document.getElementById('academic-section').classList.remove('hidden');
                
                setSemester(1);
                renderIndicators();
                
                const myChatsCount = systemRequests.filter(r => r.u1 === currentUser || r.u2 === currentUser).length;
                document.getElementById('req-count-badge').innerText = myChatsCount;

                // Feed Social
                document.getElementById('social-feed').innerHTML = Array(12).fill().map((_,i) => `
                    <div class="bg-zinc-900/50 p-6 rounded-3xl border border-white/5">
                        <p class="text-[11px] text-zinc-400 italic">"Logré subir mi promedio de ${ (2 + Math.random()*2).toFixed(1) } a ${ (4 + Math.random()).toFixed(1) } gracias a las monitorías."</p>
                    </div>
                `).join('');
            });

            document.getElementById('chatForm').addEventListener('submit', async (e) => {
                e.preventDefault();
                const inp = document.getElementById('chatInput');
                if (!inp.value.trim()) return;

                const req = systemRequests.find(r => r.id === activeChatId);
                req.messages.push({ sender: currentUser, text: inp.value });
                inp.value = '';
                renderMessages();

                document.getElementById('typing-status').classList.remove('hidden');
                const aiResp = await getAIResponse(req.messages, currentRole);
                
                setTimeout(() => {
                    req.messages.push({ sender: req.u1 === currentUser ? req.u2 : req.u1, text: aiResp });
                    document.getElementById('typing-status').classList.add('hidden');
                    renderMessages();
                    localStorage.setItem('fae_chats_v6', JSON.stringify(systemRequests));
                }, 1200);
            });
        });
    </script>
</body>
</html>
