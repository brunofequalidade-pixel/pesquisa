<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pesquisa de Satisfação</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Biblioteca para gerar arquivo Excel (.xlsx) -->
  <script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"></script>
</head>
<body class="bg-gray-100 min-h-screen font-sans text-gray-800 relative pb-10">

  <!-- CABEÇALHO COM BOTÃO DA ENGRENAGEM (ADMIN) -->
  <header class="w-full bg-white border-b border-gray-200 px-6 py-4 flex justify-between items-center shadow-sm">
    <h1 class="text-xl font-bold text-gray-800">Pesquisa de Satisfação</h1>
    <button id="btn-open-admin-modal" title="Acesso Administrativo" class="p-2 rounded-full hover:bg-gray-100 text-gray-600 hover:text-gray-900 transition">
      <!-- Ícone de Engrenagem -->
      <svg class="w-7 h-7" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"></path>
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
      </svg>
    </button>
  </header>

  <main class="max-w-4xl mx-auto px-4 mt-8">

    <!-- ÁREA DO PARTICIPANTE -->
    <div id="participant-container" class="bg-white p-6 sm:p-10 rounded-2xl shadow-md">
      
      <!-- ETAPA 1: SOLICITAR E-MAIL DO PARTICIPANTE -->
      <div id="email-step" class="max-w-md mx-auto text-center space-y-6 py-4">
        <div class="space-y-2">
          <h2 class="text-2xl font-bold text-gray-900">Seja bem-vindo(a)</h2>
          <p class="text-gray-600">Por favor, informe seu e-mail para responder à pesquisa:</p>
        </div>

        <form id="participant-email-form" class="space-y-4">
          <input type="email" id="participant-email" required placeholder="seuemail@empresa.com.br"
                 class="w-full p-4 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:outline-none text-center text-lg">
          <button type="submit" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-4 rounded-xl text-lg transition">
            Iniciar Pesquisa
          </button>
        </form>
      </div>

      <!-- ETAPA 2: FORMULÁRIO DE PERGUNTAS -->
      <div id="survey-step" class="hidden space-y-8">
        <div class="border-b pb-4">
          <h2 id="survey-title-display" class="text-2xl font-bold text-gray-900"></h2>
          <p class="text-sm text-gray-500 mt-1">Respondendo como: <span id="user-email-display" class="font-semibold text-blue-600"></span></p>
        </div>

        <form id="survey-questions-form" class="space-y-8">
          <!-- Q1 -->
          <div>
            <label class="block font-bold text-gray-800 text-lg mb-3">1. Na sua opinião, houve impacto negativo nas vendas por não receber mercadorias no sábado?</label>
            <div class="space-y-2">
              <label class="flex items-center gap-3 p-3 border rounded-xl hover:bg-gray-50 cursor-pointer"><input type="radio" name="q1" value="Sim" required class="w-5 h-5 text-blue-600"> <span class="font-medium">Sim</span></label>
              <label class="flex items-center gap-3 p-3 border rounded-xl hover:bg-gray-50 cursor-pointer"><input type="radio" name="q1" value="Não" class="w-5 h-5 text-blue-600"> <span class="font-medium">Não</span></label>
              <label class="flex items-center gap-3 p-3 border rounded-xl hover:bg-gray-50 cursor-pointer"><input type="radio" name="q1" value="Não sei informar" class="w-5 h-5 text-blue-600"> <span class="font-medium">Não sei informar</span></label>
            </div>
          </div>

          <!-- Q2 -->
          <div>
            <label class="block font-bold text-gray-800 text-lg mb-3">2. Na sua opinião, não receber mercadorias no sábado facilitou a organização e a regularização das demandas da loja?</label>
            <div class="space-y-2">
              <label class="flex items-center gap-3 p-3 border rounded-xl hover:bg-gray-50 cursor-pointer"><input type="radio" name="q2" value="Sim" required class="w-5 h-5 text-blue-600"> <span class="font-medium">Sim</span></label>
              <label class="flex items-center gap-3 p-3 border rounded-xl hover:bg-gray-50 cursor-pointer"><input type="radio" name="q2" value="Não" class="w-5 h-5 text-blue-600"> <span class="font-medium">Não</span></label>
              <label class="flex items-center gap-3 p-3 border rounded-xl hover:bg-gray-50 cursor-pointer"><input type="radio" name="q2" value="Parcialmente" class="w-5 h-5 text-blue-600"> <span class="font-medium">Parcialmente</span></label>
            </div>
          </div>

          <!-- Q3 -->
          <div>
            <label class="block font-bold text-gray-800 text-lg mb-3">3. Como você avalia a experiência de não receber mercadorias no sábado?</label>
            <div class="space-y-2">
              <label class="flex items-center gap-3 p-3 border rounded-xl hover:bg-gray-50 cursor-pointer"><input type="radio" name="q3" value="Excelente" required class="w-5 h-5 text-blue-600"> <span class="font-medium">Excelente</span></label>
              <label class="flex items-center gap-3 p-3 border rounded-xl hover:bg-gray-50 cursor-pointer"><input type="radio" name="q3" value="Boa" class="w-5 h-5 text-blue-600"> <span class="font-medium">Boa</span></label>
              <label class="flex items-center gap-3 p-3 border rounded-xl hover:bg-gray-50 cursor-pointer"><input type="radio" name="q3" value="Normal" class="w-5 h-5 text-blue-600"> <span class="font-medium">Normal</span></label>
              <label class="flex items-center gap-3 p-3 border rounded-xl hover:bg-gray-50 cursor-pointer"><input type="radio" name="q3" value="Ruim" class="w-5 h-5 text-blue-600"> <span class="font-medium">Ruim</span></label>
            </div>
          </div>

          <!-- Q4 -->
          <div>
            <label class="block font-bold text-gray-800 text-lg mb-3">4. Deixe sua opinião ou sugestão sobre a experiência de não receber mercadorias aos sábados.</label>
            <textarea name="q4" rows="4" class="w-full p-4 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:outline-none" placeholder="Sua opinião ou sugestão..."></textarea>
          </div>

          <button type="submit" id="btn-submit-survey" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-4 rounded-xl text-lg transition">
            Enviar Resposta
          </button>
        </form>
      </div>

      <!-- ETAPA 3: MENSAGENS E FEEDBACK -->
      <div id="feedback-step" class="hidden text-center py-10 space-y-4">
        <!-- Renderizado via JavaScript -->
      </div>

    </div>

    <!-- PAINEL ADMINISTRATIVO (INICIALMENTE OCULTO) -->
    <div id="admin-panel" class="hidden space-y-8 bg-white p-6 sm:p-10 rounded-2xl shadow-md">
      <div class="flex justify-between items-center border-b pb-4">
        <div>
          <h2 class="text-2xl font-bold text-gray-900">Painel Administrativo</h2>
          <p class="text-sm text-gray-500">Gestão de Pesquisas e Resultados</p>
        </div>
        <button id="btn-exit-admin" class="bg-gray-200 hover:bg-gray-300 text-gray-800 font-semibold px-4 py-2 rounded-lg text-sm transition">
          Sair do Admin
        </button>
      </div>

      <!-- CRIAR NOVA PESQUISA -->
      <div class="bg-blue-50 p-6 rounded-xl border border-blue-100 space-y-4">
        <h3 class="text-lg font-bold text-blue-900">Criar Nova Pesquisa</h3>
        <form id="create-survey-form" class="flex flex-col sm:flex-row gap-4">
          <input type="text" id="survey-title-input" required placeholder="Ex: Pesquisa de Recebimento - Sábados" class="flex-grow p-3 border rounded-xl focus:outline-none">
          <button type="submit" class="bg-blue-600 hover:bg-blue-700 text-white font-bold px-6 py-3 rounded-xl transition">
            Criar Pesquisa
          </button>
        </form>
      </div>

      <!-- LISTA DE PESQUISAS -->
      <div class="space-y-6">
        <h3 class="text-xl font-bold text-gray-900">Pesquisas Cadastradas</h3>
        <div id="admin-surveys-list" class="space-y-6">
          <!-- Conteúdo gerado dinamicamente -->
        </div>
      </div>
    </div>

  </main>

  <!-- MODAL DE LOGIN ADMIN (DISPARADO PELA ENGRENAGEM) -->
  <div id="admin-login-modal" class="fixed inset-0 bg-black/50 backdrop-blur-sm hidden flex items-center justify-center p-4 z-50">
    <div class="bg-white rounded-2xl max-w-sm w-full p-6 shadow-2xl space-y-6 relative">
      <button id="btn-close-modal" class="absolute top-4 right-4 text-gray-400 hover:text-gray-600 font-bold text-xl">&times;</button>
      
      <div class="text-center space-y-1">
        <h3 class="text-xl font-bold text-gray-900">Acesso Restrito</h3>
        <p class="text-sm text-gray-500">Informe as credenciais de Administrador</p>
      </div>

      <form id="admin-login-form" class="space-y-4">
        <div>
          <label class="block text-xs font-semibold text-gray-600 uppercase mb-1">Usuário</label>
          <input type="text" id="admin-user" required class="w-full p-3 border rounded-xl focus:ring-2 focus:ring-blue-500 focus:outline-none">
        </div>
        <div>
          <label class="block text-xs font-semibold text-gray-600 uppercase mb-1">Senha</label>
          <input type="password" id="admin-pass" required class="w-full p-3 border rounded-xl focus:ring-2 focus:ring-blue-500 focus:outline-none">
        </div>
        <button type="submit" class="w-full bg-gray-900 hover:bg-black text-white font-bold py-3 rounded-xl transition">
          Entrar no Admin
        </button>
      </form>
    </div>
  </div>

  <!-- LÓGICA DO FIREBASE E APLICAÇÃO -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
    import { getFirestore, collection, addDoc, getDocs, doc, deleteDoc, updateDoc, query, where } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

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

    let currentParticipantEmail = "";
    let activeSurvey = null;

    // Elementos de UI
    const participantContainer = document.getElementById("participant-container");
    const emailStep = document.getElementById("email-step");
    const surveyStep = document.getElementById("survey-step");
    const feedbackStep = document.getElementById("feedback-step");
    const adminPanel = document.getElementById("admin-panel");
    const adminLoginModal = document.getElementById("admin-login-modal");

    // Modal de Login Admin
    document.getElementById("btn-open-admin-modal").addEventListener("click", () => {
      adminLoginModal.classList.remove("hidden");
    });

    document.getElementById("btn-close-modal").addEventListener("click", () => {
      adminLoginModal.classList.add("hidden");
    });

    // Login Admin com Usuário 'PESQUISA' e Senha 'DPSP2026'
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

    // PARTICIPANTE: Digita o E-mail e Inicia
    document.getElementById("participant-email-form").addEventListener("submit", async (e) => {
      e.preventDefault();
      currentParticipantEmail = document.getElementById("participant-email").value.trim().toLowerCase();
      if (!currentParticipantEmail) return;

      // Buscar pesquisa ativa
      const q = query(collection(db, "pesquisas"), where("status", "==", "ativa"));
      const snap = await getDocs(q);

      emailStep.classList.add("hidden");

      if (snap.empty) {
        showFeedback("Nenhuma Pesquisa Ativa", "Não há nenhuma pesquisa aberta para respostas no momento.");
        return;
      }

      activeSurvey = { id: snap.docs[0].id, ...snap.docs[0].data() };

      // Verificar se este e-mail já respondeu à pesquisa ativa
      const respQ = query(
        collection(db, "respostas"),
        where("pesquisa_id", "==", activeSurvey.id),
        where("email", "==", currentParticipantEmail)
      );
      const respSnap = await getDocs(respQ);

      if (!respSnap.empty) {
        showFeedback("Resposta já Registrada!", `O e-mail <b>${currentParticipantEmail}</b> já enviou uma resposta para a pesquisa ativa. É permitida apenas uma resposta por e-mail.`);
        return;
      }

      // Exibir o formulário da pesquisa
      document.getElementById("survey-title-display").textContent = activeSurvey.titulo;
      document.getElementById("user-email-display").textContent = currentParticipantEmail;
      surveyStep.classList.remove("hidden");
    });

    // Envio das Respostas pelo Participante
    document.getElementById("survey-questions-form").addEventListener("submit", async (e) => {
      e.preventDefault();
      const btn = document.getElementById("btn-submit-survey");
      btn.disabled = true;
      btn.textContent = "Gravando resposta...";

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
        showFeedback("Muito Obrigado!", "Sua opinião foi registrada com sucesso.");
      } catch (err) {
        alert("Erro ao gravar resposta: " + err.message);
        btn.disabled = false;
        btn.textContent = "Enviar Resposta";
      }
    });

    function showFeedback(title, message) {
      feedbackStep.innerHTML = `
        <h3 class="text-2xl font-bold text-gray-900">${title}</h3>
        <p class="text-gray-600">${message}</p>
      `;
      feedbackStep.classList.remove("hidden");
    }

    // --- PAINEL ADMINISTRATIVO (AÇÕES) ---

    // Criar Nova Pesquisa com Data
    document.getElementById("create-survey-form").addEventListener("submit", async (e) => {
      e.preventDefault();
      const input = document.getElementById("survey-title-input");
      const title = input.value.trim();
      const now = new Date();
      const dataFormatada = now.toLocaleDateString('pt-BR') + ' ' + now.toLocaleTimeString('pt-BR');

      await addDoc(collection(db, "pesquisas"), {
        titulo: title,
        data_criacao: dataFormatada,
        status: "ativa"
      });

      input.value = "";
      loadAdminData();
    });

    // Carregar Dados das Pesquisas e Respostas no Admin
    async function loadAdminData() {
      const container = document.getElementById("admin-surveys-list");
      container.innerHTML = "<p class='text-gray-500'>Carregando dados...</p>";

      const pSnap = await getDocs(collection(db, "pesquisas"));
      const rSnap = await getDocs(collection(db, "respostas"));

      const respostas = rSnap.docs.map(d => ({ id: d.id, ...d.data() }));

      if (pSnap.empty) {
        container.innerHTML = "<p class='text-gray-500'>Nenhuma pesquisa criada até o momento.</p>";
        return;
      }

      container.innerHTML = "";

      pSnap.docs.forEach(docSnap => {
        const p = { id: docSnap.id, ...docSnap.data() };
        const pRespostas = respostas.filter(r => r.pesquisa_id === p.id);

        const card = document.createElement("div");
        card.className = "border border-gray-200 rounded-xl p-5 bg-white space-y-4 shadow-sm";
        card.innerHTML = `
          <div class="flex flex-col sm:flex-row justify-between sm:items-center gap-3 border-b pb-3">
            <div>
              <h4 class="font-bold text-lg text-gray-900">${p.titulo}</h4>
              <p class="text-xs text-gray-500">Criada em: ${p.data_criacao} | Status: <span class="font-bold uppercase ${p.status === 'ativa' ? 'text-green-600' : 'text-red-600'}">${p.status}</span></p>
            </div>
            <div class="flex flex-wrap gap-2">
              <button onclick="downloadExcel('${p.id}', '${p.titulo}')" class="bg-emerald-600 hover:bg-emerald-700 text-white text-xs font-bold px-3 py-2 rounded-lg transition">
                Baixar Excel (${pRespostas.length})
              </button>
              ${p.status === 'ativa' ? `
                <button onclick="closeSurvey('${p.id}')" class="bg-amber-500 hover:bg-amber-600 text-white text-xs font-bold px-3 py-2 rounded-lg transition">
                  Encerrar Pesquisa
                </button>
              ` : ''}
              <button onclick="deleteSurvey('${p.id}')" class="bg-red-600 hover:bg-red-700 text-white text-xs font-bold px-3 py-2 rounded-lg transition">
                Excluir Pesquisa Completa
              </button>
            </div>
          </div>

          <!-- Tabela com lixeira individual para cada resposta -->
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
                  <th class="p-2 text-center">Excluir</th>
                </tr>
              </thead>
              <tbody>
                ${pRespostas.length > 0 ? pRespostas.map(r => `
                  <tr class="border-b hover:bg-gray-50">
                    <td class="p-2 whitespace-nowrap">${r.data_hora}</td>
                    <td class="p-2">${r.email}</td>
                    <td class="p-2">${r.q1}</td>
                    <td class="p-2">${r.q2}</td>
                    <td class="p-2">${r.q3}</td>
                    <td class="p-2 max-w-xs truncate" title="${r.q4}">${r.q4}</td>
                    <td class="p-2 text-center">
                      <button onclick="deleteResponse('${r.id}')" title="Excluir Resposta Individual" class="text-red-500 hover:text-red-700 font-bold p-1">
                        🗑️
                      </button>
                    </td>
                  </tr>
                `).join('') : `
                  <tr><td colspan="7" class="p-3 text-center text-gray-400">Nenhuma resposta registrada ainda.</td></tr>
                `}
              </tbody>
            </table>
          </div>
        `;
        container.appendChild(card);
      });
    }

    // Métodos Globais para Ações Administrativas
    window.closeSurvey = async (id) => {
      if(confirm("Deseja encerrar esta pesquisa? Ninguém mais poderá responder.")) {
        await updateDoc(doc(db, "pesquisas", id), { status: "encerrada" });
        loadAdminData();
      }
    };

    window.deleteSurvey = async (id) => {
      if(confirm("Tem certeza que deseja excluir a pesquisa completa? Todas as respostas associadas serão apagadas.")) {
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
