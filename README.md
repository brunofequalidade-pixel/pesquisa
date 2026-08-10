<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Pesquisa de Satisfação</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    /* Estilo para dar feedback visual na opção selecionada */
    input[type="radio"]:checked + span {
      background-color: #3b82f6; /* bg-blue-500 */
      color: white;
      border-color: #3b82f6;
    }
  </style>
</head>
<body class="bg-gray-100 min-h-screen py-6 px-4 flex items-center justify-center font-sans antialiased">

  <div class="max-w-xl w-full bg-white p-6 sm:p-10 rounded-2xl shadow-xl transition-all duration-300" id="app">

    <!-- TELA 1: LOGIN -->
    <div id="login-screen" class="text-center space-y-6">
      <div class="space-y-1">
        <h1 class="text-3xl font-extrabold text-gray-900 tracking-tight">Pesquisa de Satisfação</h1>
        <p class="text-gray-600 text-lg">Experiência sem Recebimento de Mercadorias aos Sábados</p>
      </div>
      
      <p class="text-base text-gray-600">Por favor, informe seu e-mail corporativo para iniciar:</p>
      
      <form id="login-form" class="space-y-5 max-w-md mx-auto">
        <input type="email" id="user-email" required placeholder="seuemail@empresa.com.br"
               class="w-full p-4 border border-gray-300 rounded-xl focus:ring-4 focus:ring-blue-100 focus:border-blue-400 focus:outline-none text-center text-lg shadow-sm transition">
        <button type="submit" class="w-full bg-blue-600 hover:bg-blue-700 active:scale-95 text-white font-bold py-4 rounded-xl text-lg transition duration-200 shadow-md">
          Iniciar Pesquisa
        </button>
      </form>
      
      <div class="relative py-4">
        <div class="absolute inset-0 flex items-center"><div class="w-full border-t border-gray-300"></div></div>
        <div class="relative flex justify-center text-sm"><span class="px-3 bg-white text-gray-500 font-medium">ou</span></div>
      </div>

      <button id="btn-google" class="w-full max-w-md mx-auto flex items-center justify-center gap-3 border border-gray-300 bg-white hover:bg-gray-50 active:scale-95 text-gray-700 font-semibold py-4 rounded-xl shadow-sm transition">
        <svg class="w-6 h-6" viewBox="0 0 24 24"><path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/><path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/><path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.06H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.94l2.85-2.22.81-.63z"/><path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.06l3.66 2.84c.87-2.6 3.3-4.52 6.16-4.52z"/></svg>
        Entrar com conta Google
      </button>
    </div>

    <!-- TELA 2: FORMULÁRIO DE PESQUISA (RESPONSIVO) -->
    <div id="survey-screen" class="hidden space-y-8">
      <div class="border-b border-gray-200 pb-6 mb-8 text-center sm:text-left">
        <h1 class="text-3xl font-extrabold text-gray-900 tracking-tight">Pesquisa de Satisfação</h1>
        <p class="text-lg text-gray-700 mt-2">Olá, <span id="logged-user" class="font-bold text-blue-700"></span>.</p>
        <p class="text-sm text-gray-500 mt-1">Sua opinião é fundamental para aprimorarmos nossa operação.</p>
      </div>

      <form id="survey-form" class="space-y-10">
        <!-- Q1 -->
        <div class="space-y-4">
          <label class="block font-bold text-gray-900 text-lg leading-snug">1. Na sua opinião, houve impacto negativo nas vendas por não receber mercadorias no sábado?</label>
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
            <label class="cursor-pointer relative"><input type="radio" name="q1" value="Sim" required class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition">Sim</span></label>
            <label class="cursor-pointer relative"><input type="radio" name="q1" value="Não" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition">Não</span></label>
            <label class="cursor-pointer relative"><input type="radio" name="q1" value="Não sei informar" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition">Não sei informar</span></label>
          </div>
        </div>

        <!-- Q2 -->
        <div class="space-y-4">
          <label class="block font-bold text-gray-900 text-lg leading-snug">2. Na sua opinião, não receber mercadorias no sábado facilitou a organização e a regularização das demandas da loja?</label>
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
            <label class="cursor-pointer relative"><input type="radio" name="q2" value="Sim" required class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition">Sim</span></label>
            <label class="cursor-pointer relative"><input type="radio" name="q2" value="Não" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition">Não</span></label>
            <label class="cursor-pointer relative"><input type="radio" name="q2" value="Parcialmente" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition">Parcialmente</span></label>
          </div>
        </div>

        <!-- Q3 -->
        <div class="space-y-4">
          <label class="block font-bold text-gray-900 text-lg leading-snug">3. Como você avalia a experiência de não receber mercadorias no sábado?</label>
          <div class="grid grid-cols-1 sm:grid-cols-4 gap-3">
            <label class="cursor-pointer relative"><input type="radio" name="q3" value="Excelente" required class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition">Excelente</span></label>
            <label class="cursor-pointer relative"><input type="radio" name="q3" value="Boa" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition">Boa</span></label>
            <label class="cursor-pointer relative"><input type="radio" name="q3" value="Normal" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition">Normal</span></label>
            <label class="cursor-pointer relative"><input type="radio" name="q3" value="Ruim" class="sr-only peer"><span class="flex items-center justify-center text-center p-4 border border-gray-300 rounded-xl font-medium text-gray-800 bg-gray-50 hover:bg-gray-100 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white transition">Ruim</span></label>
          </div>
        </div>

        <!-- Q4 -->
        <div class="space-y-4">
          <label class="block font-bold text-gray-900 text-lg leading-snug">4. Deixe sua opinião ou sugestão sobre a experiência de não receber mercadorias aos sábados. <span class="text-sm font-medium text-gray-500">(Resposta aberta)</span></label>
          <textarea name="q4" rows="5" class="w-full p-4 border border-gray-300 rounded-xl focus:ring-4 focus:ring-blue-100 focus:border-blue-400 focus:outline-none text-lg transition shadow-sm placeholder-gray-400" placeholder="Compartilhe sua visão conosco..."></textarea>
        </div>

        <button type="submit" id="btn-submit" class="w-full bg-blue-600 hover:bg-blue-700 active:scale-95 text-white font-bold py-4 rounded-xl text-lg transition duration-200 shadow-lg disabled:bg-gray-400 disabled:cursor-not-allowed">
          Enviar Resposta
        </button>
      </form>
    </div>

    <!-- TELA 3: CONFIRMAÇÃO DE ENVIO -->
    <div id="success-screen" class="hidden text-center py-12 space-y-6">
      <div class="w-24 h-24 bg-green-100 text-green-600 rounded-full flex items-center justify-center mx-auto shadow-inner">
        <svg class="w-12 h-12" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"></path></svg>
      </div>
      <div class="space-y-2">
        <h2 class="text-3xl font-extrabold text-gray-900">Muito Obrigado!</h2>
        <p class="text-xl text-gray-700">Sua opinião foi registrada com sucesso.</p>
        <p class="text-base text-gray-500">Agradecemos sua colaboração.</p>
      </div>
    </div>

  </div>

  <!-- Lógica Firebase JavaScript - MANTENDO SUA CONFIGURAÇÃO ORIGINAL -->
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
        console.error("Erro no login Google:", error);
        alert("Ocorreu um erro no login com o Google. Verifique se o Google Sign-In está ativado no seu Firebase Console.");
      }
    });

    function showSurvey() {
      loggedUserSpan.textContent = currentUserEmail;
      loginScreen.classList.add("hidden");
      surveyScreen.classList.remove("hidden");
      window.scrollTo(0, 0); // Rola para o topo da tela
    }

    // Gravar no Firestore com Feedback ao Usuário
    document.getElementById("survey-form").addEventListener("submit", async (e) => {
      e.preventDefault();
      const btn = document.getElementById("btn-submit");
      btn.disabled = true;
      btn.textContent = "Gravando sua resposta... por favor aguarde.";

      const formData = new FormData(e.target);
      const now = new Date();
      const dataFormatada = now.toLocaleDateString('pt-BR') + ' ' + now.toLocaleTimeString('pt-BR');

      try {
        // Tenta gravar no banco de dados. O problema de não responder
        // geralmente ocorre aqui, devido às regras de segurança.
        await addDoc(collection(db, "respostas"), {
          email: currentUserEmail,
          data_hora: dataFormatada,
          q1_impacto_vendas: formData.get("q1"),
          q2_organizacao: formData.get("q2"),
          q3_avaliacao_geral: formData.get("q3"),
          q4_opiniao_sugestao: formData.get("q4") || ""
        });

        // Se gravou com sucesso, troca de tela
        surveyScreen.classList.add("hidden");
        successScreen.classList.remove("hidden");
        window.scrollTo(0, 0); // Rola para o topo da tela
      } catch (error) {
        // Se der erro, mostra alerta e console
        console.error("Erro ao gravar resposta no Firebase:", error);
        
        // Mensagem de erro mais amigável, indicando as Regras de Segurança como provável causa
        let msg = "Ops! Ocorreu um erro ao enviar sua resposta. \n\n" +
                  "Detalhes do erro: " + error.message;
        
        if (error.code === 'permission-denied') {
          msg += "\n\nAVISO PARA O DESENVOLVEDOR: O envio falhou porque o banco de dados Cloud Firestore não tem permissão de ESCRITA. Por favor, verifique as REGRAS DE SEGURANÇA no Firebase Console (conforme Passo 2)."
        }
        
        alert(msg);
        btn.disabled = false;
        btn.textContent = "Enviar Resposta";
      }
    });
  </script>
</body>
</html>
