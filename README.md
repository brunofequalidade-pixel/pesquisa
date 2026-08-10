<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sistema de Pesquisa de Satisfação</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Biblioteca para gerar arquivo Excel diretamente no navegador -->
  <script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"></script>
</head>
<body class="bg-gray-100 min-h-screen py-6 px-4 font-sans text-gray-800">

  <div class="max-w-4xl mx-auto bg-white p-6 sm:p-10 rounded-2xl shadow-xl" id="app">

    <!-- CABEÇALHO COM NAVEGAÇÃO -->
    <div class="flex justify-between items-center border-b pb-4 mb-6">
      <div>
        <h1 class="text-2xl font-bold text-gray-900">Pesquisa de Satisfação</h1>
        <p id="user-status" class="text-sm text-gray-500">Não autenticado</p>
      </div>
      <button id="btn-toggle-admin" class="hidden bg-gray-800 hover:bg-gray-900 text-white text-sm font-semibold px-4 py-2 rounded-lg transition">
        Painel Admin
      </button>
    </div>

    <!-- TELA 1: LOGIN -->
    <div id="login-screen" class="max-w-md mx-auto text-center space-y-6 py-8">
      <p class="text-gray-600">Identifique-se para acessar o formulário:</p>
      <form id="login-form" class="space-y-4">
        <input type="email" id="user-email" required placeholder="seuemail@empresa.com.br"
               class="w-full p-3 border rounded-xl text-center focus:ring-2 focus:ring-blue-500 focus:outline-none">
        <button type="submit" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 rounded-xl transition">
          Acessar com E-mail
        </button>
      </form>
      <div class="text-gray-400 text-sm">ou</div>
      <button id="btn-google" class="w-full flex items-center justify-center gap-3 border bg-white hover:bg-gray-50 text-gray-700 font-semibold py-3 rounded-xl shadow-sm transition">
        <svg class="w-5 h-5" viewBox="0 0 24 24"><path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/><path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/><path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.06H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.94l2.85-2.22.81-.63z"/><path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.06l3.66 2.84c.87-2.6 3.3-4.52 6.16-4.52z"/></svg>
        Entrar com conta Google
      </button>
    </div>

    <!-- TELA 2: FORMULÁRIO DO USUÁRIO -->
    <div id="survey-screen" class="hidden space-y-8">
      <div id="survey-content">
        <!-- Renderizado dinamicamente -->
      </div>
    </div>

    <!-- TELA 3: PAINEL ADMINISTRATIVO -->
    <div id="admin-screen" class="hidden space-y-8">
      <div class="bg-gray-50 p-6 rounded-xl border border-gray-200">
        <h2 class="text-xl font-bold mb-4">Criar Nova Pesquisa</h2>
        <form id="create-survey-form" class="flex flex-col sm:flex-row gap-4">
          <input type="text" id="survey-title" required placeholder="Título da Pesquisa" class="flex-grow p-3 border rounded-lg focus:outline-none">
          <button type="submit" class="bg-green-600 hover:bg-green-700 text-white font-bold px-6 py-3 rounded-lg transition">
            Criar Pesquisa
          </button>
        </form>
      </div>

      <div>
        <h2 class="text-xl font-bold mb-4">Gerenciar Pesquisas e Respostas</h2>
        <div id="admin-surveys-list" class="space-y-6">
          <!-- Lista de pesquisas cadastradas -->
        </div>
      </div>
    </div>

  </div>

  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
    import { getFirestore, collection, addDoc, getDocs, doc, deleteDoc, updateDoc, query, where } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";
    import { getAuth, GoogleAuthProvider, signInWithPopup, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-auth.js";

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

    let currentUser = null;
    let activeSurvey = null;

    // Elementos da interface
    const loginScreen = document.getElementById("login-screen");
    const surveyScreen = document.getElementById("survey-screen");
    const adminScreen = document.getElementById("admin-screen");
    const userStatus = document.getElementById("user-status");
    const btnToggleAdmin = document.getElementById("btn-toggle-admin");

    // Login via e-mail manual
    document.getElementById("login-form").addEventListener("submit", (e) => {
      e.preventDefault();
      const email = document.getElementById("user-email").value.trim();
      if(email) {
        currentUser = { email };
        initAppView();
      }
    });

    // Login com Google
    document.getElementById("btn-google").addEventListener("click", async () => {
      try {
        const res = await signInWithPopup(auth, provider);
        currentUser = res.user;
        initAppView();
      } catch (err) {
        alert("Erro no login Google: " + err.message);
      }
    });

    // Alternar visualização entre Formulário e Admin
    btnToggleAdmin.addEventListener("click", () => {
      if(adminScreen.classList.contains("hidden")) {
        surveyScreen.classList.add("hidden");
        adminScreen.classList.remove("hidden");
        loadAdminData();
      } else {
        adminScreen.classList.add("hidden");
        surveyScreen.classList.remove("hidden");
      }
    });

    async function initAppView() {
      userStatus.textContent = `Logado como: ${currentUser.email}`;
      loginScreen.classList.add("hidden");
      btnToggleAdmin.classList.remove("hidden");
      surveyScreen.classList.remove("hidden");
      await loadActiveSurvey();
    }

    // Carrega a pesquisa ativa e verifica se usuário já respondeu
    async function loadActiveSurvey() {
      const q = query(collection(db, "pesquisas"), where("status", "==", "ativa"));
      const snap = await getDocs(q);

      const surveyContent = document.getElementById("survey-content");

      if(snap.empty) {
        surveyContent.innerHTML = `<div class="text-center py-10 text-gray-500 font-medium">Nenhuma pesquisa ativa no momento.</div>`;
        return;
      }

      activeSurvey = { id: snap.docs[0].id, ...snap.docs[0].data() };

      // Trava de 1 resposta por e-mail
      const respQ = query(
        collection(db, "respostas"),
        where("pesquisa_id", "==", activeSurvey.id),
        where("email", "==", currentUser.email)
      );
      const respSnap = await getDocs(respQ);

      if(!respSnap.empty) {
        surveyContent.innerHTML = `
          <div class="text-center py-10 space-y-3">
            <div class="text-2xl font-bold text-green-600">Resposta já Registrada!</div>
            <p class="text-gray-600">Você já respondeu à pesquisa "${activeSurvey.titulo}". É permitida apenas uma resposta por e-mail.</p>
          </div>`;
        return;
      }

      renderSurveyForm(activeSurvey);
    }

    // Renderiza as perguntas da pesquisa
    function renderSurveyForm(survey) {
      document.getElementById("survey-content").innerHTML = `
        <h2 class="text-2xl font-bold text-gray-900">${survey.titulo}</h2>
        <p class="text-sm text-gray-500 mb-6">Criada em: ${survey.data_criacao}</p>

        <form id="user-survey-form" class="space-y-6">
          <div>
            <label class="block font-bold text-gray-800 mb-2">1. Na sua opinião, houve impacto negativo nas vendas por não receber mercadorias no sábado?</label>
            <div class="space-y-2">
              <label class="flex items-center gap-2"><input type="radio" name="q1" value="Sim" required> Sim</label>
              <label class="flex items-center gap-2"><input type="radio" name="q1" value="Não"> Não</label>
              <label class="flex items-center gap-2"><input type="radio" name="q1" value="Não sei informar"> Não sei informar</label>
            </div>
          </div>

          <div>
            <label class="block font-bold text-gray-800 mb-2">2. Na sua opinião, não receber mercadorias no sábado facilitou a organização e a regularização das demandas da loja?</label>
            <div class="space-y-2">
              <label class="flex items-center gap-2"><input type="radio" name="q2" value="Sim" required> Sim</label>
              <label class="flex items-center gap-2"><input type="radio" name="q2" value="Não"> Não</label>
              <label class="flex items-center gap-2"><input type="radio" name="q2" value="Parcialmente"> Parcialmente</label>
            </div>
          </div>

          <div>
            <label class="block font-bold text-gray-800 mb-2">3. Como você avalia a experiência de não receber mercadorias no sábado?</label>
            <div class="space-y-2">
              <label class="flex items-center gap-2"><input type="radio" name="q3" value="Excelente" required> Excelente</label>
              <label class="flex items-center gap-2"><input type="radio" name="q3" value="Boa"> Boa</label>
              <label class="flex items-center gap-2"><input type="radio" name="q3" value="Normal"> Normal</label>
              <label class="flex items-center gap-2"><input type="radio" name="q3" value="Ruim"> Ruim</label>
            </div>
          </div>

          <div>
            <label class="block font-bold text-gray-800 mb-2">4. Deixe sua opinião ou sugestão sobre a experiência de não receber mercadorias aos sábados.</label>
            <textarea name="q4" rows="4" class="w-full p-3 border rounded-xl focus:outline-none" placeholder="Sua resposta..."></textarea>
          </div>

          <button type="submit" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-4 rounded-xl transition">
            Enviar Resposta
          </button>
        </form>
      `;

      document.getElementById("user-survey-form").addEventListener("submit", submitResponse);
    }

    // Gravar Resposta
    async function submitResponse(e) {
      e.preventDefault();
      const formData = new FormData(e.target);
      const now = new Date();
      const dataFormatada = now.toLocaleDateString('pt-BR') + ' ' + now.toLocaleTimeString('pt-BR');

      await addDoc(collection(db, "respostas"), {
        pesquisa_id: activeSurvey.id,
        email: currentUser.email,
        data_hora: dataFormatada,
        q1: formData.get("q1"),
        q2: formData.get("q2"),
        q3: formData.get("q3"),
        q4: formData.get("q4") || ""
      });

      loadActiveSurvey();
    }

    // --- FUNÇÕES ADMIN ---

    // Criar Nova Pesquisa com Data
    document.getElementById("create-survey-form").addEventListener("submit", async (e) => {
      e.preventDefault();
      const title = document.getElementById("survey-title").value.trim();
      const now = new Date();
      const dataFormatada = now.toLocaleDateString('pt-BR') + ' ' + now.toLocaleTimeString('pt-BR');

      await addDoc(collection(db, "pesquisas"), {
        titulo: title,
        data_criacao: dataFormatada,
        status: "ativa"
      });

      document.getElementById("survey-title").value = "";
      loadAdminData();
    });

    // Carregar dados no Painel Admin
    async function loadAdminData() {
      const listContainer = document.getElementById("admin-surveys-list");
      listContainer.innerHTML = "Carregando...";

      const pSnap = await getDocs(collection(db, "pesquisas"));
      const rSnap = await getDocs(collection(db, "respostas"));

      const respostas = rSnap.docs.map(d => ({ id: d.id, ...d.data() }));

      listContainer.innerHTML = "";

      pSnap.docs.forEach(docSnap => {
        const p = { id: docSnap.id, ...docSnap.data() };
        const pRespostas = respostas.filter(r => r.pesquisa_id === p.id);

        const card = document.createElement("div");
        card.className = "border rounded-xl p-5 bg-white space-y-4 shadow-sm";
        card.innerHTML = `
          <div class="flex flex-col sm:flex-row justify-between sm:items-center gap-2 border-b pb-3">
            <div>
              <h3 class="font-bold text-lg text-gray-900">${p.titulo}</h3>
              <p class="text-xs text-gray-500">Criada em: ${p.data_criacao} | Status: <span class="font-semibold">${p.status.toUpperCase()}</span></p>
            </div>
            <div class="flex flex-wrap gap-2">
              <button onclick="downloadExcel('${p.id}', '${p.titulo}')" class="bg-emerald-600 hover:bg-emerald-700 text-white text-xs font-bold px-3 py-2 rounded transition">
                Baixar Excel (${pRespostas.length})
              </button>
              ${p.status === 'ativa' ? `
                <button onclick="closeSurvey('${p.id}')" class="bg-amber-500 hover:bg-amber-600 text-white text-xs font-bold px-3 py-2 rounded transition">
                  Encerrar Pesquisa
                </button>
              ` : ''}
              <button onclick="deleteSurvey('${p.id}')" class="bg-red-600 hover:bg-red-700 text-white text-xs font-bold px-3 py-2 rounded transition">
                Excluir Pesquisa Completa
              </button>
            </div>
          </div>

          <!-- Tabela de respostas com lixeira individual -->
          <div class="overflow-x-auto">
            <table class="w-full text-xs text-left text-gray-600">
              <thead class="bg-gray-100 text-gray-700 uppercase">
                <tr>
                  <th class="p-2">Data/Hora</th>
                  <th class="p-2">E-mail</th>
                  <th class="p-2">Q1</th>
                  <th class="p-2">Q2</th>
                  <th class="p-2">Q3</th>
                  <th class="p-2">Q4 (Opinião)</th>
                  <th class="p-2 text-center">Ações</th>
                </tr>
              </thead>
              <tbody>
                ${pRespostas.map(r => `
                  <tr class="border-b">
                    <td class="p-2 whitespace-nowrap">${r.data_hora}</td>
                    <td class="p-2">${r.email}</td>
                    <td class="p-2">${r.q1}</td>
                    <td class="p-2">${r.q2}</td>
                    <td class="p-2">${r.q3}</td>
                    <td class="p-2 max-w-xs truncate">${r.q4}</td>
                    <td class="p-2 text-center">
                      <button onclick="deleteResponse('${r.id}')" title="Excluir Resposta" class="text-red-500 hover:text-red-700 font-bold px-2">
                        🗑️
                      </button>
                    </td>
                  </tr>
                `).join('')}
              </tbody>
            </table>
          </div>
        `;
        listContainer.appendChild(card);
      });
    }

    // Funções Globais para Ações do Admin
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
      if(confirm("Remover esta resposta individual?")) {
        await deleteDoc(doc(db, "respostas", id));
        loadAdminData();
      }
    };

    // Baixar relatório em Excel
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
        alert("Não há respostas registradas para exportar.");
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
