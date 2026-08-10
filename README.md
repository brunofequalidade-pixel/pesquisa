<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pesquisa de Satisfação</title>
  
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts: Inter -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
  <!-- SheetJS para Excel -->
  <script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"></script>

  <style>
    body { font-family: 'Inter', sans-serif; }
    /* Custom Scrollbar */
    ::-webkit-scrollbar { width: 8px; height: 8px; }
    ::-webkit-scrollbar-track { background: #f1f5f9; }
    ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
    ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
  </style>
</head>
<body class="bg-slate-900 text-slate-100 min-h-screen flex flex-col justify-between antialiased selection:bg-blue-500 selection:text-white">

  <!-- BACKGROUND DECORATIVO INTERATIVO -->
  <div class="fixed inset-0 pointer-events-none z-0 overflow-hidden">
    <div class="absolute -top-40 -left-40 w-96 h-96 bg-blue-600/20 rounded-full blur-3xl"></div>
    <div class="absolute top-1/2 -right-40 w-96 h-96 bg-indigo-600/20 rounded-full blur-3xl"></div>
    <div class="absolute -bottom-40 left-1/3 w-96 h-96 bg-cyan-600/15 rounded-full blur-3xl"></div>
  </div>

  <!-- CABEÇALHO FIXO PREMIUM -->
  <header class="sticky top-0 z-40 w-full bg-slate-900/80 backdrop-blur-md border-b border-slate-800/80 px-4 sm:px-8 py-4 transition-all">
    <div class="max-w-7xl mx-auto flex justify-between items-center">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-blue-600 to-indigo-500 flex items-center justify-center shadow-lg shadow-blue-500/20">
          <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"/>
          </svg>
        </div>
        <div>
          <h1 class="text-lg sm:text-xl font-bold bg-gradient-to-r from-white via-slate-200 to-slate-400 bg-clip-text text-transparent">
            Pesquisa de Satisfação
          </h1>
          <p class="text-xs text-slate-400 hidden sm:block">Portal de Avaliação Corporativa</p>
        </div>
      </div>

      <button id="btn-open-admin-modal" title="Acesso Administrativo" 
        class="p-2.5 rounded-xl bg-slate-800/80 border border-slate-700/60 hover:bg-slate-700/80 text-slate-300 hover:text-white transition-all duration-200 shadow-sm active:scale-95 flex items-center gap-2">
        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"></path>
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
        </svg>
        <span class="text-xs font-semibold hidden md:inline">Painel Admin</span>
      </button>
    </div>
  </header>

  <!-- CONTEÚDO PRINCIPAL (TELA CHEIA RESPONSIVA) -->
  <main class="relative z-10 flex-1 w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 sm:py-10 flex flex-col justify-center">

    <!-- ÁREA DO PARTICIPANTE -->
    <div id="participant-container" class="w-full max-w-3xl mx-auto">
      
      <!-- ETAPA 1: SOLICITAR E-MAIL DO PARTICIPANTE -->
      <div id="email-step" class="bg-slate-800/60 backdrop-blur-xl border border-slate-700/60 p-6 sm:p-12 rounded-3xl shadow-2xl space-y-8 transition-all">
        <div class="text-center space-y-3">
          <span class="px-3 py-1 bg-blue-500/10 border border-blue-500/20 text-blue-400 text-xs font-semibold rounded-full uppercase tracking-wider">
            Identificação
          </span>
          <h2 class="text-2xl sm:text-4xl font-extrabold text-white tracking-tight">Seja bem-vindo(a)</h2>
          <p class="text-slate-400 text-sm sm:text-base max-w-md mx-auto">
            Para iniciar o preenchimento, informe seu endereço de e-mail corporativo abaixo:
          </p>
        </div>

        <form id="participant-email-form" class="space-y-5 max-w-md mx-auto">
          <div class="relative">
            <div class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none text-slate-500">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 12a4 4 0 10-8 0 4 4 0 008 0zm0 0v1.5a2.5 2.5 0 005 0V12a9 9 0 10-9 9m4.5-1.206a8.959 8.959 0 01-4.5 1.207"/>
              </svg>
            </div>
            <input type="email" id="participant-email" required placeholder="seuemail@empresa.com.br"
                   class="w-full pl-12 pr-4 py-4 bg-slate-900/80 border border-slate-700 focus:border-blue-500 rounded-2xl focus:ring-4 focus:ring-blue-500/20 focus:outline-none text-slate-100 placeholder-slate-500 text-base sm:text-lg transition-all">
          </div>
          <button type="submit" id="btn-start-survey" 
                  class="w-full bg-gradient-to-r from-blue-600 to-indigo-600 hover:from-blue-500 hover:to-indigo-500 text-white font-bold py-4 rounded-2xl text-base sm:text-lg transition-all duration-200 shadow-lg shadow-blue-600/30 active:scale-[0.98] flex items-center justify-center gap-2">
            <span>Iniciar Pesquisa</span>
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"/>
            </svg>
          </button>
        </form>
      </div>

      <!-- ETAPA 2: FORMULÁRIO DE PERGUNTAS -->
      <div id="survey-step" class="hidden bg-slate-800/60 backdrop-blur-xl border border-slate-700/60 p-6 sm:p-10 rounded-3xl shadow-2xl space-y-8">
        
        <div class="border-b border-slate-700/80 pb-6 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-2">
          <div>
            <span class="text-xs font-semibold text-blue-400 uppercase tracking-wider">Pesquisa Ativa</span>
            <h2 id="survey-title-display" class="text-2xl sm:text-3xl font-bold text-white mt-1"></h2>
          </div>
          <div class="px-3 py-1.5 bg-slate-900/80 border border-slate-700 rounded-xl text-xs text-slate-400">
            Usuário: <span id="user-email-display" class="font-semibold text-blue-400"></span>
          </div>
        </div>

        <form id="survey-questions-form" class="space-y-8">
          
          <!-- Pergunta 1 -->
          <div class="bg-slate-900/50 p-5 sm:p-6 rounded-2xl border border-slate-700/50 space-y-4">
            <label class="block font-semibold text-slate-100 text-base sm:text-lg">
              1. Na sua opinião, houve impacto negativo nas vendas por não receber mercadorias no sábado?
            </label>
            <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
              <label class="flex items-center gap-3 p-4 bg-slate-800/80 border border-slate-700 rounded-xl hover:border-blue-500/50 hover:bg-slate-800 cursor-pointer transition-all">
                <input type="radio" name="q1" value="Sim" required class="w-5 h-5 text-blue-600 focus:ring-blue-500 bg-slate-900 border-slate-700">
                <span class="font-medium text-slate-200">Sim</span>
              </label>
              <label class="flex items-center gap-3 p-4 bg-slate-800/80 border border-slate-700 rounded-xl hover:border-blue-500/50 hover:bg-slate-800 cursor-pointer transition-all">
                <input type="radio" name="q1" value="Não" class="w-5 h-5 text-blue-600 focus:ring-blue-500 bg-slate-900 border-slate-700">
                <span class="font-medium text-slate-200">Não</span>
              </label>
              <label class="flex items-center gap-3 p-4 bg-slate-800/80 border border-slate-700 rounded-xl hover:border-blue-500/50 hover:bg-slate-800 cursor-pointer transition-all">
                <input type="radio" name="q1" value="Não sei informar" class="w-5 h-5 text-blue-600 focus:ring-blue-500 bg-slate-900 border-slate-700">
                <span class="font-medium text-slate-200">Não sei informar</span>
              </label>
            </div>
          </div>

          <!-- Pergunta 2 -->
          <div class="bg-slate-900/50 p-5 sm:p-6 rounded-2xl border border-slate-700/50 space-y-4">
            <label class="block font-semibold text-slate-100 text-base sm:text-lg">
              2. Na sua opinião, não receber mercadorias no sábado facilitou a organização e a regularização das demandas da loja?
            </label>
            <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
              <label class="flex items-center gap-3 p-4 bg-slate-800/80 border border-slate-700 rounded-xl hover:border-blue-500/50 hover:bg-slate-800 cursor-pointer transition-all">
                <input type="radio" name="q2" value="Sim" required class="w-5 h-5 text-blue-600 focus:ring-blue-500 bg-slate-900 border-slate-700">
                <span class="font-medium text-slate-200">Sim</span>
              </label>
              <label class="flex items-center gap-3 p-4 bg-slate-800/80 border border-slate-700 rounded-xl hover:border-blue-500/50 hover:bg-slate-800 cursor-pointer transition-all">
                <input type="radio" name="q2" value="Não" class="w-5 h-5 text-blue-600 focus:ring-blue-500 bg-slate-900 border-slate-700">
                <span class="font-medium text-slate-200">Não</span>
              </label>
              <label class="flex items-center gap-3 p-4 bg-slate-800/80 border border-slate-700 rounded-xl hover:border-blue-500/50 hover:bg-slate-800 cursor-pointer transition-all">
                <input type="radio" name="q2" value="Parcialmente" class="w-5 h-5 text-blue-600 focus:ring-blue-500 bg-slate-900 border-slate-700">
                <span class="font-medium text-slate-200">Parcialmente</span>
              </label>
            </div>
          </div>

          <!-- Pergunta 3 -->
          <div class="bg-slate-900/50 p-5 sm:p-6 rounded-2xl border border-slate-700/50 space-y-4">
            <label class="block font-semibold text-slate-100 text-base sm:text-lg">
              3. Como você avalia a experiência de não receber mercadorias no sábado?
            </label>
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-3">
              <label class="flex items-center gap-3 p-4 bg-slate-800/80 border border-slate-700 rounded-xl hover:border-blue-500/50 hover:bg-slate-800 cursor-pointer transition-all">
                <input type="radio" name="q3" value="Excelente" required class="w-5 h-5 text-blue-600 focus:ring-blue-500 bg-slate-900 border-slate-700">
                <span class="font-medium text-slate-200">Excelente</span>
              </label>
              <label class="flex items-center gap-3 p-4 bg-slate-800/80 border border-slate-700 rounded-xl hover:border-blue-500/50 hover:bg-slate-800 cursor-pointer transition-all">
                <input type="radio" name="q3" value="Boa" class="w-5 h-5 text-blue-600 focus:ring-blue-500 bg-slate-900 border-slate-700">
                <span class="font-medium text-slate-200">Boa</span>
              </label>
              <label class="flex items-center gap-3 p-4 bg-slate-800/80 border border-slate-700 rounded-xl hover:border-blue-500/50 hover:bg-slate-800 cursor-pointer transition-all">
                <input type="radio" name="q3" value="Normal" class="w-5 h-5 text-blue-600 focus:ring-blue-500 bg-slate-900 border-slate-700">
                <span class="font-medium text-slate-200">Normal</span>
              </label>
              <label class="flex items-center gap-3 p-4 bg-slate-800/80 border border-slate-700 rounded-xl hover:border-blue-500/50 hover:bg-slate-800 cursor-pointer transition-all">
                <input type="radio" name="q3" value="Ruim" class="w-5 h-5 text-blue-600 focus:ring-blue-500 bg-slate-900 border-slate-700">
                <span class="font-medium text-slate-200">Ruim</span>
              </label>
            </div>
          </div>

          <!-- Pergunta 4 -->
          <div class="bg-slate-900/50 p-5 sm:p-6 rounded-2xl border border-slate-700/50 space-y-4">
            <label class="block font-semibold text-slate-100 text-base sm:text-lg">
              4. Deixe sua opinião ou sugestão sobre a experiência de não receber mercadorias aos sábados.
            </label>
            <textarea name="q4" rows="4" 
                      class="w-full p-4 bg-slate-800/80 border border-slate-700 rounded-xl focus:border-blue-500 focus:ring-2 focus:ring-blue-500/20 focus:outline-none text-slate-100 placeholder-slate-500 transition-all" 
                      placeholder="Escreva seus comentários aqui..."></textarea>
          </div>

          <button type="submit" id="btn-submit-survey" 
                  class="w-full bg-gradient-to-r from-emerald-600 to-teal-600 hover:from-emerald-500 hover:to-teal-500 text-white font-bold py-4 rounded-2xl text-lg transition-all duration-200 shadow-lg shadow-emerald-600/30 active:scale-[0.98]">
            Enviar Resposta
          </button>
        </form>
      </div>

      <!-- ETAPA 3: MENSAGENS DE FEEDBACK -->
      <div id="feedback-step" class="hidden bg-slate-800/60 backdrop-blur-xl border border-slate-700/60 p-8 sm:p-12 rounded-3xl shadow-2xl text-center space-y-4"></div>

    </div>

    <!-- PAINEL ADMINISTRATIVO (COMPLETO E AMPLO PARA NOTEBOOK/TELA CHEIA) -->
    <div id="admin-panel" class="hidden w-full space-y-8 bg-slate-800/60 backdrop-blur-xl border border-slate-700/60 p-6 sm:p-10 rounded-3xl shadow-2xl">
      
      <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 border-b border-slate-700/80 pb-6">
        <div>
          <span class="px-3 py-1 bg-indigo-500/10 border border-indigo-500/20 text-indigo-400 text-xs font-semibold rounded-full uppercase tracking-wider">
            Área Restrita
          </span>
          <h2 class="text-2xl sm:text-3xl font-bold text-white mt-2">Painel Administrativo</h2>
          <p class="text-slate-400 text-sm">Gestão de Pesquisas e Métricas de Respostas</p>
        </div>
        <button id="btn-exit-admin" 
                class="bg-slate-700 hover:bg-slate-600 text-slate-200 font-semibold px-5 py-2.5 rounded-xl text-sm transition-all duration-200 border border-slate-600">
          Sair do Admin
        </button>
      </div>

      <!-- CRIAR NOVA PESQUISA -->
      <div class="bg-slate-900/70 p-6 rounded-2xl border border-slate-700/60 space-y-4">
        <h3 class="text-lg font-bold text-slate-100 flex items-center gap-2">
          <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/>
          </svg>
          Criar Nova Pesquisa
        </h3>
        <form id="create-survey-form" class="flex flex-col sm:flex-row gap-3">
          <input type="text" id="survey-title-input" required placeholder="Ex: Pesquisa de Recebimento - Sábados" 
                 class="flex-grow p-3.5 bg-slate-800 border border-slate-700 rounded-xl focus:border-blue-500 focus:outline-none text-slate-100 placeholder-slate-500 text-sm">
          <button type="submit" id="btn-create-survey" 
                  class="bg-blue-600 hover:bg-blue-500 text-white font-bold px-6 py-3.5 rounded-xl transition-all duration-200 shadow-md shadow-blue-600/20 whitespace-nowrap text-sm">
            Criar Pesquisa
          </button>
        </form>
      </div>

      <!-- LISTA DE PESQUISAS -->
      <div class="space-y-6">
        <h3 class="text-xl font-bold text-white">Pesquisas Cadastradas</h3>
        <div id="admin-surveys-list" class="space-y-6"></div>
      </div>
    </div>

  </main>

  <!-- FOOTER SUTIL -->
  <footer class="relative z-10 w-full text-center py-4 border-t border-slate-800/60 text-xs text-slate-500">
    © 2026 Sistema de Pesquisas de Satisfação • CD Bahia DPSP
  </footer>

  <!-- MODAL DE LOGIN ADMIN -->
  <div id="admin-login-modal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-md hidden flex items-center justify-center p-4 z-50">
    <div class="bg-slate-900 border border-slate-800 rounded-3xl max-w-sm w-full p-6 sm:p-8 shadow-2xl space-y-6 relative animate-in fade-in zoom-in duration-200">
      
      <button id="btn-close-modal" class="absolute top-4 right-4 text-slate-500 hover:text-slate-300 transition text-2xl font-bold">&times;</button>
      
      <div class="text-center space-y-2">
        <div class="w-12 h-12 bg-slate-800 rounded-2xl flex items-center justify-center mx-auto text-blue-400 border border-slate-700">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"/>
          </svg>
        </div>
        <h3 class="text-xl font-bold text-white">Acesso Restrito</h3>
        <p class="text-xs text-slate-400">Informe suas credenciais de Administrador</p>
      </div>

      <form id="admin-login-form" class="space-y-4">
        <div>
          <label class="block text-xs font-semibold text-slate-400 uppercase tracking-wider mb-1">Usuário</label>
          <input type="text" id="admin-user" required class="w-full p-3 bg-slate-800 border border-slate-700 rounded-xl focus:border-blue-500 focus:outline-none text-slate-100 text-sm">
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-400 uppercase tracking-wider mb-1">Senha</label>
          <input type="password" id="admin-pass" required class="w-full p-3 bg-slate-800 border border-slate-700 rounded-xl focus:border-blue-500 focus:outline-none text-slate-100 text-sm">
        </div>
        <button type="submit" class="w-full bg-gradient-to-r from-blue-600 to-indigo-600 hover:from-blue-500 hover:to-indigo-500 text-white font-bold py-3 rounded-xl transition duration-200 shadow-lg shadow-blue-600/30 text-sm">
          Entrar no Admin
        </button>
      </form>
    </div>
  </div>

  <!-- SCRIPT FIREBASE -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
    import { getFirestore, collection, addDoc, getDocs, doc, deleteDoc, updateDoc, query, where } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "AIzaSyAbXWJo0L3fZeK1itLhyFvs03xeTXcn0gg",
      authDomain: "pesquisa-cdcb3.firebaseapp.com",
      databaseURL: "https://pesquisa-cdcb3-default-rtdb.firebaseio.com",
      projectId: "pesquisa-cdcb3",
      storageBucket: "pesquisa-cdcb3.firebasestorage.app",
      messagingSenderId: "1026729731641",
      appId: "1:1026729731641:web:6dc2af32a152c2808d4fe8",
      measurementId: "G-ZX3Y1VBSXN"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    let currentParticipantEmail = "";
    let activeSurvey = null;

    const participantContainer = document.getElementById("participant-container");
    const emailStep = document.getElementById("email-step");
    const surveyStep = document.getElementById("survey-step");
    const feedbackStep = document.getElementById("feedback-step");
    const adminPanel = document.getElementById("admin-panel");
    const adminLoginModal = document.getElementById("admin-login-modal");

    document.getElementById("btn-open-admin-modal").addEventListener("click", () => {
      adminLoginModal.classList.remove("hidden");
    });

    document.getElementById("btn-close-modal").addEventListener("click", () => {
      adminLoginModal.classList.add("hidden");
    });

    document.getElementById("admin-login-form").addEventListener("submit", (e) => {
      e.preventDefault();
      const user = document.getElementById("admin-user").value.trim().toUpperCase();
      const pass = document.getElementById("admin-pass").value.trim();

      if (user === "PESQUISA" && pass === "DPSP2026") {
        adminLoginModal.classList.add("hidden");
        participantContainer.classList.add("hidden");
        adminPanel.classList.remove("hidden");
        document.getElementById("admin-user").value = "";
        document.getElementById("admin-pass").value = "";
        loadAdminData();
      } else {
        alert("Usuário ou Senha incorretos!");
      }
    });

    document.getElementById("btn-exit-admin").addEventListener("click", () => {
      adminPanel.classList.add("hidden");
      participantContainer.classList.remove("hidden");
    });

    document.getElementById("participant-email-form").addEventListener("submit", async (e) => {
      e.preventDefault();
      const btn = document.getElementById("btn-start-survey");
      btn.disabled = true;
      btn.innerHTML = `<span class="animate-pulse">Verificando...</span>`;

      currentParticipantEmail = document.getElementById("participant-email").value.trim().toLowerCase();

      try {
        const q = query(collection(db, "pesquisas"), where("status", "==", "ativa"));
        const snap = await getDocs(q);

        emailStep.classList.add("hidden");

        if (snap.empty) {
          showFeedback("Nenhuma Pesquisa Ativa", "Não há nenhuma pesquisa aberta no momento.");
          return;
        }

        activeSurvey = { id: snap.docs[0].id, ...snap.docs[0].data() };

        const respQ = query(
          collection(db, "respostas"),
          where("pesquisa_id", "==", activeSurvey.id),
          where("email", "==", currentParticipantEmail)
        );
        const respSnap = await getDocs(respQ);

        if (!respSnap.empty) {
          showFeedback("Resposta já Registrada!", `O e-mail <b class="text-blue-400">${currentParticipantEmail}</b> já respondeu a esta pesquisa. É permitida apenas uma resposta por e-mail.`);
          return;
        }

        document.getElementById("survey-title-display").textContent = activeSurvey.titulo;
        document.getElementById("user-email-display").textContent = currentParticipantEmail;
        surveyStep.classList.remove("hidden");
      } catch (err) {
        alert("Erro ao conectar no banco de dados: " + err.message);
        emailStep.classList.remove("hidden");
      } finally {
        btn.disabled = false;
        btn.innerHTML = `<span>Iniciar Pesquisa</span> <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"/></svg>`;
      }
    });

    document.getElementById("survey-questions-form").addEventListener("submit", async (e) => {
      e.preventDefault();
      const btn = document.getElementById("btn-submit-survey");
      btn.disabled = true;
      btn.textContent = "Gravando...";

      const formData = new FormData(e.target);
      const now = new Date();
      const dataFormatada = now.toLocaleDateString('pt-BR') + ' ' + now.toLocaleTimeString('pt-BR');

      try {
        await addDoc(collection(db, "respostas"), {
          pesquisa_id: activeSurvey.id,
          email: currentParticipantEmail,
          data_hora: dataFormatada,
          q1: formData.get("q1"),
          q2: formData.get("q2"),
          q3: formData.get("q3"),
          q4: formData.get("q4") || ""
        });

        surveyStep.classList.add("hidden");
        showFeedback("Muito Obrigado!", "Sua resposta foi salva com sucesso.");
      } catch (err) {
        alert("Erro ao gravar resposta: " + err.message);
        btn.disabled = false;
        btn.textContent = "Enviar Resposta";
      }
    });

    function showFeedback(title, message) {
      feedbackStep.innerHTML = `
        <div class="w-16 h-16 bg-blue-500/10 border border-blue-500/20 text-blue-400 rounded-full flex items-center justify-center mx-auto mb-2">
          <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/></svg>
        </div>
        <h3 class="text-2xl sm:text-3xl font-bold text-white">${title}</h3>
        <p class="text-slate-300 max-w-md mx-auto text-sm sm:text-base">${message}</p>
      `;
      feedbackStep.classList.remove("hidden");
    }

    // --- AÇÕES ADMINISTRATIVAS ---
    document.getElementById("create-survey-form").addEventListener("submit", async (e) => {
      e.preventDefault();
      const input = document.getElementById("survey-title-input");
      const title = input.value.trim();
      const btn = document.getElementById("btn-create-survey");

      if (!title) return;

      btn.disabled = true;
      btn.textContent = "Criando...";

      try {
        const now = new Date();
        const dataFormatada = now.toLocaleDateString('pt-BR') + ' ' + now.toLocaleTimeString('pt-BR');

        await addDoc(collection(db, "pesquisas"), {
          titulo: title,
          data_criacao: dataFormatada,
          status: "ativa"
        });

        input.value = "";
        alert("Pesquisa criada com sucesso!");
        await loadAdminData();
      } catch (err) {
        console.error(err);
        alert("Erro ao criar pesquisa: " + err.message);
      } finally {
        btn.disabled = false;
        btn.textContent = "Criar Pesquisa";
      }
    });

    async function loadAdminData() {
      const container = document.getElementById("admin-surveys-list");
      container.innerHTML = "<p class='text-slate-400 text-sm animate-pulse'>Carregando dados...</p>";

      try {
        const pSnap = await getDocs(collection(db, "pesquisas"));
        const rSnap = await getDocs(collection(db, "respostas"));

        const respostas = rSnap.docs.map(d => ({ id: d.id, ...d.data() }));

        if (pSnap.empty) {
          container.innerHTML = "<p class='text-slate-400 text-sm'>Nenhuma pesquisa cadastrada até o momento.</p>";
          return;
        }

        container.innerHTML = "";

        pSnap.docs.forEach(docSnap => {
          const p = { id: docSnap.id, ...docSnap.data() };
          const pRespostas = respostas.filter(r => r.pesquisa_id === p.id);

          const card = document.createElement("div");
          card.className = "border border-slate-700/80 rounded-2xl p-5 sm:p-6 bg-slate-900/80 space-y-4 shadow-xl";
          card.innerHTML = `
            <div class="flex flex-col lg:flex-row justify-between lg:items-center gap-4 border-b border-slate-800 pb-4">
              <div>
                <h4 class="font-bold text-lg text-white">${p.titulo}</h4>
                <p class="text-xs text-slate-400 mt-1">
                  Criada em: ${p.data_criacao} | 
                  Status: <span class="font-bold uppercase ${p.status === 'ativa' ? 'text-emerald-400' : 'text-rose-400'}">${p.status}</span>
                </p>
              </div>
              <div class="flex flex-wrap gap-2">
                <button onclick="downloadExcel('${p.id}', '${p.titulo}')" class="bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-semibold px-3.5 py-2 rounded-lg transition-all flex items-center gap-1.5">
                  📥 Baixar Excel (${pRespostas.length})
                </button>
                ${p.status === 'ativa' ? `
                  <button onclick="closeSurvey('${p.id}')" class="bg-amber-600 hover:bg-amber-500 text-white text-xs font-semibold px-3.5 py-2 rounded-lg transition-all">
                    Encerrar
                  </button>
                ` : ''}
                <button onclick="deleteSurvey('${p.id}')" class="bg-rose-600 hover:bg-rose-500 text-white text-xs font-semibold px-3.5 py-2 rounded-lg transition-all">
                  Excluir
                </button>
              </div>
            </div>

            <div class="overflow-x-auto rounded-xl border border-slate-800">
              <table class="w-full text-xs text-left text-slate-300">
                <thead class="bg-slate-800/90 text-slate-400 uppercase tracking-wider font-semibold">
                  <tr>
                    <th class="p-3">Data/Hora</th>
                    <th class="p-3">E-mail</th>
                    <th class="p-3">Q1</th>
                    <th class="p-3">Q2</th>
                    <th class="p-3">Q3</th>
                    <th class="p-3">Q4 (Opinião)</th>
                    <th class="p-3 text-center">Ações</th>
                  </tr>
                </thead>
                <tbody class="divide-y divide-slate-800/60">
                  ${pRespostas.length > 0 ? pRespostas.map(r => `
                    <tr class="hover:bg-slate-800/40 transition-colors">
                      <td class="p-3 whitespace-nowrap text-slate-400">${r.data_hora}</td>
                      <td class="p-3 font-medium text-slate-200">${r.email}</td>
                      <td class="p-3">${r.q1}</td>
                      <td class="p-3">${r.q2}</td>
                      <td class="p-3">${r.q3}</td>
                      <td class="p-3 max-w-xs truncate" title="${r.q4}">${r.q4 || '-'}</td>
                      <td class="p-3 text-center">
                        <button onclick="deleteResponse('${r.id}')" title="Excluir Resposta" class="text-rose-400 hover:text-rose-300 font-bold p-1 transition">
                          🗑️
                        </button>
                      </td>
                    </tr>
                  `).join('') : `
                    <tr><td colspan="7" class="p-4 text-center text-slate-500">Nenhuma resposta registrada.</td></tr>
                  `}
                </tbody>
              </table>
            </div>
          `;
          container.appendChild(card);
        });
      } catch (err) {
        container.innerHTML = `<p class='text-rose-400 text-sm'>Erro ao carregar dados: ${err.message}</p>`;
      }
    }

    window.closeSurvey = async (id) => {
      if(confirm("Deseja encerrar esta pesquisa? Ninguém mais poderá responder.")) {
        await updateDoc(doc(db, "pesquisas", id), { status: "encerrada" });
        loadAdminData();
      }
    };

    window.deleteSurvey = async (id) => {
      if(confirm("Tem certeza que deseja excluir a pesquisa completa? Todas as respostas serão apagadas.")) {
        await deleteDoc(doc(db, "pesquisas", id));
        loadAdminData();
      }
    };

    window.deleteResponse = async (id) => {
      if(confirm("Deseja excluir esta resposta individual?")) {
        await deleteDoc(doc(db, "respostas", id));
        loadAdminData();
      }
    };

    window.downloadExcel = async (pesquisaId, titulo) => {
      const q = query(collection(db, "respostas"), where("pesquisa_id", "==", pesquisaId));
      const snap = await getDocs(q);

      const dados = snap.docs.map(docSnap => {
        const r = docSnap.data();
        return {
          "Data/Hora": r.data_hora,
          "E-mail": r.email,
          "Impacto Vendas (Q1)": r.q1,
          "Facilitou Organização (Q2)": r.q2,
          "Avaliação Geral (Q3)": r.q3,
          "Opinião / Sugestão (Q4)": r.q4
        };
      });

      if(dados.length === 0) {
        alert("Não há respostas registradas nesta pesquisa para exportar.");
        return;
      }

      const worksheet = XLSX.utils.json_to_sheet(dados);
      const workbook = XLSX.utils.book_new();
      XLSX.utils.book_append_sheet(workbook, worksheet, "Respostas");
      XLSX.writeFile(workbook, `Pesquisa_${titulo.replaceAll(' ', '_')}.xlsx`);
    };
  </script>
</body>
</html>
