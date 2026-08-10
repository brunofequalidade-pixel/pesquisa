<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Pesquisa de Satisfação - Recebimento</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    /* Estilo para garantir altura total e centralização no Desktop */
    html, body { height: 100%; margin: 0; padding: 0; overflow-x: hidden; }
    #app-container { min-height: 100%; display: flex; justify-content: center; background-color: #fff; }
    /* No Desktop, dá uma leve sombra e limita largura */
    @media (min-width: 640px) {
      #main-card { max-width: 800px; padding: 3rem; background-color: #fff; border-radius: 1.5rem; box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05); }
      #app-container { background-color: #f3f4f6; padding: 2rem; }
    }
    /* Estilo para dar feedback visual na opção selecionada nos inputs estilo 'botão' */
    input[type="radio"]:checked + span {
      background-color: #2563eb; /* bg-blue-600 */
      color: white;
      border-color: #2563eb;
    }
  </style>
</head>
<body class="font-sans antialiased">

  <div id="app-container">
    <!-- MAIN CARD: Responsivo Total -->
    <div class="w-screen min-h-screen sm:min-h-0 sm:w-full bg-white p-5 sm:p-10 flex flex-col transition-all duration-300" id="main-card">

      <!-- TELA 1: LOGIN/IDENTIFICAÇÃO -->
      <div id="login-screen" class="flex-grow flex flex-col justify-center text-center space-y-8 py-10">
        <div class="space-y-2">
          <h1 class="text-3xl font-extrabold text-gray-900 tracking-tight sm:text-4xl">Pesquisa de Satisfação</h1>
          <p class="text-gray-600 text-lg sm:text-xl">Experiência sem Recebimento de Mercadorias aos Sábados</p>
        </div>
        
        <p class="text-base text-gray-700 max-w-md mx-auto">Por favor, informe seu e-mail corporativo para iniciar a pesquisa:</p>
        
        <form id="login-form" class="space-y-5 max-w-md mx-auto w-full">
          <input type="email" id="user-email" required placeholder="seuemail@empresa.com.br"
                 class="w-full p-4 border border-gray-300 rounded-xl focus:ring-4 focus:ring-blue-100 focus:border-blue-400 focus:outline-none text-center text-lg shadow-inner transition">
          <button type="submit" class="w-full bg-blue-600 hover:bg-blue-700 active:scale-95 text-white font-bold py-4 rounded-xl text-lg transition duration-200 shadow-md">
            Iniciar Pesquisa
          </button>
        </form>
        
        <div class="relative py-4 max-w-md mx-auto w-full">
          <div class="absolute inset-0 flex items-center"><div class="w-full border-t border-gray-300"></div></div>
          <div class="relative flex justify-center text-sm"><span class="px-3 bg-white text-gray-500 font-medium">ou</span></div>
        </div>

        <button id="btn-google" class="w-full max-w-md mx-auto flex items-center justify-center gap-3 border border-gray-300 bg-white hover:bg-gray-50 active:scale-95 text-gray-700 font-semibold py-4 rounded-xl shadow-sm transition">
          <svg class="w-6 h-6" viewBox="0 0 24 24"><path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/><path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/><path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.06H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.94l2.85-2.22.81-.63z"/><path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.06l3.66 2.84c.87-2.6 3.3-4.52 6.16-4.52z"/></svg>
          Entrar com conta Google
        </button>
      </div>

      <!-- TELA 2: FORMULÁRIO DE PESQUISA (RESPONSIVO TOTAL) -->
      <div id="survey-screen" class="hidden space-y-10 py-6">
        <div class="border-b border-gray-200 pb-6 mb-8 text-center sm:text-left">
          <h1 class="text-3xl font-extrabold text-gray-900 tracking-tight sm:text-4xl">Sua Opinião</h1>
          <p class="text-lg text-gray-700 mt-2">Olá, <span id="logged-user" class="font-bold text-blue-700"></span>.</p>
          <p class="text-sm text-gray-500 mt-1">Sua resposta ajudará a melhorar nossa operação.</p>
        </div>

        <form id="survey-form" class="space-y-12">
          <!-- Q1 -->
          <div class="space-y-5">
            <label class="block font-bold text-gray-900 text-lg leading-snug sm:text-xl">1. Na sua opinião, houve impacto negativo nas vendas por não receber mercadorias no sábado?</label>
            <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
              <label class="cursor-pointer relative"><input type="radio" name="q1" value="Sim" required class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition shadow-sm">Sim</span></label>
              <label class="cursor-pointer relative"><input type="radio" name="q1" value="Não" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition shadow-sm">Não</span></label>
              <label class="cursor-pointer relative"><input type="radio" name="q1" value="Não sei informar" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition shadow-sm">Não sei informar</span></label>
            </div>
          </div>

          <!-- Q2 -->
          <div class="space-y-5">
            <label class="block font-bold text-gray-900 text-lg leading-snug sm:text-xl">2. Na sua opinião, não receber mercadorias no sábado facilitou a organização e a regularização das demandas da loja?</label>
            <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
              <label class="cursor-pointer relative"><input type="radio" name="q2" value="Sim" required class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition shadow-sm">Sim</span></label>
              <label class="cursor-pointer relative"><input type="radio" name="q2" value="Não" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition shadow-sm">Não</span></label>
              <label class="cursor-pointer relative"><input type="radio" name="q2" value="Parcialmente" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition shadow-sm">Parcialmente</span></label>
            </div>
          </div>

          <!-- Q3 -->
          <div class="space-y-5">
            <label class="block font-bold text-gray-900 text-lg leading-snug sm:text-xl">3. Como você avalia a experiência de não receber mercadorias no sábado?</label>
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-3">
              <label class="cursor-pointer relative"><input type="radio" name="q3" value="Excelente" required class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition shadow-sm">Excelente</span></label>
              <label class="cursor-pointer relative"><input type="radio" name="q3" value="Boa" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition shadow-sm">Boa</span></label>
              <label class="cursor-pointer relative"><input type="radio" name="q3" value="Normal" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition shadow-sm">Normal</span></label>
              <label class="cursor-pointer relative"><input type="radio" name="q3" value="Ruim" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition shadow-sm">Ruim</span></label>
            </div>
          </div>

          <!-- Q4 -->
          <div class="space-y-5">
            <label class="block font-bold text-gray-900 text-lg leading-snug sm:text-xl">4. Deixe sua opinião ou sugestão sobre a experiência de não receber mercadorias aos sábados. <span class="text-sm font-medium text-gray-500">(Resposta aberta)</span></label>
            <textarea name="q4" rows="6" class="w-full p-4 border border-gray-300 rounded-xl focus:ring-4 focus:ring-blue-100 focus:border-blue-400 focus:outline-none text-lg transition shadow-inner placeholder-gray-400" placeholder="Compartilhe sua visão conosco..."></textarea>
          </div>

          <button type="submit" id="btn-submit" class="w-full bg-blue-600 hover:bg-blue-700 active:scale-95 text-white font-bold py-5 rounded-xl text-xl transition duration-200 shadow-lg disabled:bg-gray-400 disabled:cursor-not-allowed">
            Enviar Minha Resposta
          </button>
        </form>
      </div>

      <!-- TELA 3: CONFIRMAÇÃO DE ENVIO -->
      <div id="success-screen" class="hidden flex-grow flex flex-col justify-center text-center space-y-6 py-12">
        <div class="w-28 h-28 bg-green-100 text-green-600 rounded-full flex items-center justify-center mx-auto shadow-inner">
          <svg class="w-14 h-14" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"></path></svg>
        </div>
        <div class="space-y-2">
          <h2 class="text-4xl font-extrabold text-gray-900 sm:text-5xl">Muito Obrigado!</h2>
          <p class="text-2xl text-gray-700">Sua opinião foi registrada com sucesso.</p>
          <p class="text-base text-gray-500 pt-3">Você já pode fechar esta tela.</p>
        </div>
      </div>

    </div>
  </div>

  <!-- Lógica Firebase JavaScript -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
    import { getFirestore, collection, addDoc } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";
    import { getAuth, GoogleAuthProvider, signInWithPopup } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-auth.js";

    // --- SUA CONFIGURAÇÃO ORIGINAL ---
    const firebaseConfig = {
      apiKey: "AIzaSyAbXWJo0L3fZeK1itLhyFvs03xeTXcn0gg",
      authDomain: "pesquisa-cdcb3.firebaseapp.com",
      projectId: "pesquisa-cdcb3",
      storageBucket: "pesquisa-cdcb3.firebasestorage.app",
      messagingSenderId: "1026729731641",
      appId: "1:1026729731641:web:f2528b1854afaa188d4fe8",
      measurementId: "G-RX6J1XZFHH"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    const auth = getAuth(app);
    const provider = new GoogleAuthProvider();

    let currentUserEmail = "";

    const loginScreen = document.getElementById("login-screen");
    const surveyScreen = document.getElementById("survey-screen");
    const successScreen = document.getElementById("success-screen");
    const loggedUserSpan = document.getElementById("logged-user");

    // Lógica para alternar telas
    function showSurvey() {
      loggedUserSpan.textContent = currentUserEmail;
      loginScreen.classList.add("hidden");
      surveyScreen.classList.remove("hidden");
      window.scrollTo(0, 0);
    }

    // Login digitando o e-mail
    document.getElementById("login-form").addEventListener("submit", (e) => {
      e.preventDefault();
      currentUserEmail = document.getElementById("user-email").value.trim();
      if(currentUserEmail) showSurvey();
    });

    // Login com Google
    document.getElementById("btn-google").addEventListener("click", async () => {
      try {
        const result = await signInWithPopup(auth, provider);
        currentUserEmail = result.user.email;
        showSurvey();
      } catch (error) {
        console.error("Erro login Google:", error);
        alert("Erro no login Google. Verifique se ativou o método de login Google no Firebase.");
      }
    });

    // --- NOVA LÓGICA DE ENVIO COM TEMPO LIMITE (TIMEOUT) ---
    document.getElementById("survey-form").addEventListener("submit", async (e) => {
      e.preventDefault();
      const btn = document.getElementById("btn-submit");
      
      // Feedback imediato: bloqueia botão e muda texto
      btn.disabled = true;
      const originalText = btn.textContent;
      btn.textContent = "Gravando sua resposta... favor aguarde.";

      const formData = new FormData(e.target);
      const now = new Date();
      const dataFormatada = now.toLocaleDateString('pt-BR') + ' ' + now.toLocaleTimeString('pt-BR');

      // Objeto com os dados
      const payload = {
        email: currentUserEmail,
        data_hora: dataFormatada,
        q1_impacto_vendas: formData.get("q1"),
        q2_organizacao: formData.get("q2"),
        q3_avaliacao_geral: formData.get("q3"),
        q4_opiniao_sugestao: formData.get("q4") || ""
      };

      // Cria um TimeOut para não travar a tela
      const timerOutPromise = new Promise((_, reject) =>
        setTimeout(() => reject(new Error('tempo_limite')), 10000) // 10 segundos de limite
      );

      // Tenta gravar no Firebase, mas aceita a desistência pelo timeout
      try {
        await Promise.race([
          addDoc(collection(db, "respostas"), payload),
          timerOutPromise
        ]);

        // SE CHEGOU AQUI, GRAVOU COM SUCESSO
        surveyScreen.classList.add("hidden");
        successScreen.classList.remove("hidden");
        window.scrollTo(0, 0);
      } catch (error) {
        console.error("Erro detectado:", error);
        
        // Reverte botão
        btn.disabled = false;
        btn.textContent = originalText;

        if (error.message === 'tempo_limite') {
          alert("Ops! O servidor Firebase está demorando muito para responder.\n\nPor favor, tente clicar em enviar novamente daqui a alguns segundos.");
        } else if (error.code === 'permission-denied') {
          alert("Erro de Permissão: O envio foi bloqueado pelo Firebase.\n\nIsso geralmente acontece quando as Regras de Segurança (Firestore Rules) do banco de dados não foram configuradas para permitir ESCRITA. Por favor, verifique a configuração no console.");
        } else {
          alert("Ocorreu um erro ao enviar sua resposta. Detalhes:\n" + error.message);
        }
      }
    });
  </script>
</body>
</html>
