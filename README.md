<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pesquisa de Satisfação - Recebimento aos Sábados</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 min-h-screen py-10 px-4 flex items-center justify-center">

  <div class="max-w-2xl w-full bg-white p-8 rounded-xl shadow-md" id="app">

    <!-- TELA 1: LOGIN -->
    <div id="login-screen" class="text-center">
      <h1 class="text-2xl font-bold text-gray-800 mb-2">Pesquisa de Satisfação</h1>
      <p class="text-gray-600 mb-6">Experiência sem Recebimento de Mercadorias aos Sábados</p>
      
      <p class="text-sm text-gray-500 mb-4">Informe seu e-mail para iniciar a pesquisa:</p>
      
      <form id="login-form" class="space-y-4 max-w-md mx-auto">
        <input type="email" id="user-email" required placeholder="seuemail@empresa.com.br"
               class="w-full px-4 py-2 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none text-center">
        <button type="submit" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-3 rounded-lg transition duration-200">
          Iniciar Pesquisa
        </button>
      </form>
      
      <div class="relative my-6">
        <div class="absolute inset-0 flex items-center"><div class="w-full border-t border-gray-300"></div></div>
        <div class="relative flex justify-center text-sm"><span class="px-2 bg-white text-gray-500">ou</span></div>
      </div>

      <button id="btn-google" class="w-full max-w-md mx-auto flex items-center justify-center gap-2 border border-gray-300 bg-white hover:bg-gray-50 text-gray-700 font-medium py-2.5 rounded-lg transition">
        <svg class="w-5 h-5" viewBox="0 0 24 24"><path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/><path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/><path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.06H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.94l2.85-2.22.81-.63z"/><path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.06l3.66 2.84c.87-2.6 3.3-4.52 6.16-4.52z"/></svg>
        Entrar com conta Google
      </button>
    </div>

    <!-- TELA 2: FORMULÁRIO DE PESQUISA -->
    <div id="survey-screen" class="hidden">
      <div class="border-b pb-4 mb-6">
        <h1 class="text-2xl font-bold text-gray-800">Pesquisa de Satisfação</h1>
        <p class="text-sm text-gray-500">Respondendo como: <span id="logged-user" class="font-semibold text-blue-600"></span></p>
      </div>

      <form id="survey-form" class="space-y-6">
        <!-- Q1 -->
        <div>
          <label class="block font-medium text-gray-800 mb-2">1. Na sua opinião, houve impacto negativo nas vendas por não receber mercadorias no sábado?</label>
          <div class="space-y-2">
            <label class="flex items-center space-x-2 cursor-pointer"><input type="radio" name="q1" value="Sim" required class="w-4 h-4 text-blue-600"> <span>Sim</span></label>
            <label class="flex items-center space-x-2 cursor-pointer"><input type="radio" name="q1" value="Não" class="w-4 h-4 text-blue-600"> <span>Não</span></label>
            <label class="flex items-center space-x-2 cursor-pointer"><input type="radio" name="q1" value="Não sei informar" class="w-4 h-4 text-blue-600"> <span>Não sei informar</span></label>
          </div>
        </div>

        <!-- Q2 -->
        <div>
          <label class="block font-medium text-gray-800 mb-2">2. Na sua opinião, não receber mercadorias no sábado facilitou a organização e a regularização das demandas da loja?</label>
          <div class="space-y-2">
            <label class="flex items-center space-x-2 cursor-pointer"><input type="radio" name="q2" value="Sim" required class="w-4 h-4 text-blue-600"> <span>Sim</span></label>
            <label class="flex items-center space-x-2 cursor-pointer"><input type="radio" name="q2" value="Não" class="w-4 h-4 text-blue-600"> <span>Não</span></label>
            <label class="flex items-center space-x-2 cursor-pointer"><input type="radio" name="q2" value="Parcialmente" class="w-4 h-4 text-blue-600"> <span>Parcialmente</span></label>
          </div>
        </div>

        <!-- Q3 -->
        <div>
          <label class="block font-medium text-gray-800 mb-2">3. Como você avalia a experiência de não receber mercadorias no sábado?</label>
          <div class="space-y-2">
            <label class="flex items-center space-x-2 cursor-pointer"><input type="radio" name="q3" value="Excelente" required class="w-4 h-4 text-blue-600"> <span>Excelente</span></label>
            <label class="flex items-center space-x-2 cursor-pointer"><input type="radio" name="q3" value="Boa" class="w-4 h-4 text-blue-600"> <span>Boa</span></label>
            <label class="flex items-center space-x-2 cursor-pointer"><input type="radio" name="q3" value="Normal" class="w-4 h-4 text-blue-600"> <span>Normal</span></label>
            <label class="flex items-center space-x-2 cursor-pointer"><input type="radio" name="q3" value="Ruim" class="w-4 h-4 text-blue-600"> <span>Ruim</span></label>
          </div>
        </div>

        <!-- Q4 -->
        <div>
          <label class="block font-medium text-gray-800 mb-2">4. Deixe sua opinião ou sugestão sobre a experiência de não receber mercadorias aos sábados.</label>
          <textarea name="q4" rows="4" class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none" placeholder="Sua resposta aberta..."></textarea>
        </div>

        <button type="submit" id="btn-submit" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-3 rounded-lg transition duration-200">
          Enviar Resposta
        </button>
      </form>
    </div>

    <!-- TELA 3: CONFIRMAÇÃO DE ENVIO -->
    <div id="success-screen" class="hidden text-center py-8">
      <div class="w-16 h-16 bg-green-100 text-green-600 rounded-full flex items-center justify-center mx-auto mb-4">
        <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>
      </div>
      <h2 class="text-2xl font-bold text-gray-800 mb-2">Obrigado!</h2>
      <p class="text-gray-600">Sua opinião foi registrada com sucesso.</p>
    </div>

  </div>

  <!-- Lógica Firebase JavaScript -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
    import { getFirestore, collection, addDoc } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";
    import { getAuth, GoogleAuthProvider, signInWithPopup } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-auth.js";

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
        alert("Erro no login Google: " + error.message);
      }
    });

    function showSurvey() {
      loggedUserSpan.textContent = currentUserEmail;
      loginScreen.classList.add("hidden");
      surveyScreen.classList.remove("hidden");
    }

    // Gravar no Firestore
    document.getElementById("survey-form").addEventListener("submit", async (e) => {
      e.preventDefault();
      const btn = document.getElementById("btn-submit");
      btn.disabled = true;
      btn.textContent = "Enviando...";

      const formData = new FormData(e.target);
      const now = new Date();
      const dataFormatada = now.toLocaleDateString('pt-BR') + ' ' + now.toLocaleTimeString('pt-BR');

      try {
        await addDoc(collection(db, "respostas"), {
          email: currentUserEmail,
          data_hora: dataFormatada,
          q1_impacto_vendas: formData.get("q1"),
          q2_organizacao: formData.get("q2"),
          q3_avaliacao_geral: formData.get("q3"),
          q4_opiniao_sugestao: formData.get("q4") || ""
        });

        surveyScreen.classList.add("hidden");
        successScreen.classList.remove("hidden");
      } catch (error) {
        alert("Erro ao gravar resposta: " + error.message);
        btn.disabled = false;
        btn.textContent = "Enviar Resposta";
      }
    });
  </script>
</body>
</html>
