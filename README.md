# Código do aplicativo 

<!DOCTYPE html>
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Papudos Marmitos - Taverna Viking Refinada</title>

    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        viking: {
                            bg: '#05050A',       // Preto Noturno Profundo
                            card: '#0B132B',     // Azul Escuro Rúnico
                            elevated: '#1C2541', // Azul Escuro Nobre
                            accent: '#3A506B',   // Azul Aço Escuro
                            silver: '#CBD5E1',   // Prata Reluzente
                            brightSilver: '#F8FAFC',
                            highlight: '#94A3B8'
                        }
                    },
                    fontFamily: {
                        cinzel: ['Cinzel', 'serif'],
                        sans: ['Plus Jakarta Sans', 'sans-serif']
                    }
                }
            }
        }
    </script>

    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@500;700;900&family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">

    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>

    <style>
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #05050A;
            color: #F8FAFC;
        }

        .font-cinzel {
            font-family: 'Cinzel', serif;
        }

        /* Efeitos Viking Prateados e Sombras Noturnas */
        .silver-border {
            border: 1px solid rgba(203, 213, 225, 0.25);
            box-shadow: 0 4px 20px -2px rgba(0, 0, 0, 0.8), inset 0 0 15px rgba(203, 213, 225, 0.05);
        }

        .silver-border-glow:hover, .silver-border-glow:focus-within {
            border-color: rgba(248, 250, 252, 0.7);
            box-shadow: 0 0 20px rgba(203, 213, 225, 0.3);
        }

        .rune-pattern {
            background-image: radial-gradient(circle at 50% 50%, rgba(28, 37, 65, 0.4) 0%, rgba(5, 5, 10, 0.95) 100%);
        }

        /* Scrollbar Personalizada Prata/Azul */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #05050A;
        }
        ::-webkit-scrollbar-thumb {
            background: #1C2541;
            border-radius: 4px;
            border: 1px solid #3A506B;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #3A506B;
        }

        /* Modos de Acessibilidade */
        .high-contrast {
            background-color: #000000 !important;
            color: #FFFFFF !important;
        }
        .high-contrast * {
            border-color: #FFFFFF !important;
            box-shadow: none !important;
        }
        .high-contrast button, .high-contrast a {
            background-color: #000000 !important;
            color: #FFFFFF !important;
            outline: 2px solid #FFFFFF !important;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between rune-pattern text-viking-brightSilver selection:bg-viking-accent selection:text-white transition-all duration-300">

    <!-- BARRA DE ACESSIBILIDADE UNIVERSAL (Sempre Visível) -->
    <header class="bg-viking-card/90 backdrop-blur-md border-b border-viking-silver/20 sticky top-0 z-40 px-4 py-3" role="banner">
        <div class="max-w-7xl mx-auto flex flex-wrap items-center justify-between gap-4">
            
            <!-- Logo & Nome da Taverna -->
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-full bg-viking-elevated silver-border flex items-center justify-center text-viking-silver">
                    <i data-lucide="shield" class="w-6 h-6"></i>
                </div>
                <div>
                    <h1 class="font-cinzel font-bold text-lg md:text-xl text-viking-brightSilver tracking-wide flex items-center gap-2">
                        PAPUDOS MARMITOS
                        <span class="text-xs font-sans px-2 py-0.5 rounded-full bg-viking-elevated silver-border text-viking-silver font-normal">Taverna Refinada</span>
                    </h1>
                </div>
            </div>

            <!-- Ferramentas Globais de Acessibilidade -->
            <nav aria-label="Controles de Acessibilidade" class="flex items-center gap-2 flex-wrap">
                <!-- Leitor de Voz Dinâmico -->
                <button id="btnVoiceToggle" onclick="toggleVoiceReadout()" aria-label="Ativar ou desativar leitura de voz por áudio" title="Leitor de Voz para Cegos" class="flex items-center gap-1.5 px-3 py-1.5 text-xs font-semibold rounded-lg bg-viking-elevated silver-border hover:bg-viking-accent focus:ring-2 focus:ring-viking-silver transition-all">
                    <i data-lucide="volume-2" class="w-4 h-4 text-viking-silver"></i>
                    <span id="voiceStatusText">Voz: OFF</span>
                </button>

                <!-- Controle de Fonte -->
                <div class="flex items-center bg-viking-elevated silver-border rounded-lg p-0.5" role="group" aria-label="Ajuste do Tamanho da Fonte">
                    <button onclick="changeFontSize(-1)" aria-label="Diminuir tamanho do texto" title="Diminuir Fonte (A-)" class="px-2 py-1 text-xs font-bold hover:bg-viking-accent rounded transition-all">A-</button>
                    <button onclick="resetFontSize()" aria-label="Restaurar tamanho padrão do texto" title="Tamanho Padrão (A)" class="px-2 py-1 text-xs font-bold hover:bg-viking-accent rounded transition-all">A</button>
                    <button onclick="changeFontSize(1)" aria-label="Aumentar tamanho do texto" title="Aumentar Fonte (A+)" class="px-2 py-1 text-xs font-bold hover:bg-viking-accent rounded transition-all">A+</button>
                </div>

                <!-- Alto Contraste -->
                <button onclick="toggleHighContrast()" aria-label="Alternar Alto Contraste para baixa visão" title="Modo Alto Contraste" class="p-1.5 rounded-lg bg-viking-elevated silver-border hover:bg-viking-accent transition-all">
                    <i data-lucide="eye" class="w-4 h-4 text-viking-silver"></i>
                </button>

                <!-- Suporte em LIBRAS -->
                <button onclick="openLibrasModal()" aria-label="Abrir assistente em LIBRAS para pessoas surdas" title="Suporte LIBRAS e Texto" class="flex items-center gap-1 px-3 py-1.5 text-xs font-semibold rounded-lg bg-viking-elevated silver-border hover:bg-viking-accent transition-all">
                    <i data-lucide="hand" class="w-4 h-4 text-viking-silver"></i>
                    <span>LIBRAS</span>
                </button>

                <!-- Botão Painel VS Code -->
                <button onclick="openDevModal()" aria-label="Abrir painel de código fonte para VS Code" title="Códigos Fonte VS Code (HTML, CSS, JS, SQL)" class="flex items-center gap-1 px-3 py-1.5 text-xs font-bold rounded-lg bg-viking-accent border border-viking-silver/50 hover:bg-viking-elevated text-viking-brightSilver transition-all ml-2">
                    <i data-lucide="code-2" class="w-4 h-4"></i>
                    <span class="hidden sm:inline">VS Code</span>
                </button>

                <!-- Ícone / Botão do Barquinho Drakkar (Carrinho) -->
                <button onclick="toggleDrakkarDrawer()" aria-label="Abrir Barquinho de compras, contém 0 itens" id="btnDrakkarCart" class="relative p-2 rounded-lg bg-viking-elevated silver-border hover:bg-viking-accent transition-all ml-1">
                    <i data-lucide="anchor" class="w-5 h-5 text-viking-silver"></i>
                    <span id="drakkarBadge" class="absolute -top-1.5 -right-1.5 bg-viking-brightSilver text-viking-bg font-extrabold text-[10px] w-5 h-5 rounded-full flex items-center justify-center border border-viking-card">0</span>
                </button>
            </nav>
        </div>
    </header>

    <!-- CONTEÚDO PRINCIPAL (TELAS DINÂMICAS) -->
    <main id="mainAppContainer" class="max-w-6xl mx-auto w-full p-4 md:p-6 flex-grow flex flex-col justify-center" role="main">

        <!-- TELAS 1: LOGIN E CADASTRO -->
        <section id="screenAuth" class="w-full max-w-md mx-auto space-y-6">
            <div class="bg-viking-card p-6 md:p-8 rounded-2xl silver-border shadow-2xl relative overflow-hidden">
                <div class="text-center space-y-2 mb-6">
                    <i data-lucide="castle" class="w-12 h-12 text-viking-silver mx-auto stroke-1"></i>
                    <h2 id="authTitle" class="font-cinzel text-2xl font-bold tracking-wider text-viking-brightSilver">Papudos Marmitos</h2>
                    <p id="authSubtitle" class="text-xs text-viking-highlight">Identifique-se para adentrar o salão nobre de banquetes</p>
                </div>

                <!-- Tabs Login / Cadastro -->
                <div class="flex bg-viking-elevated p-1 rounded-xl border border-viking-silver/20 mb-6" role="tablist">
                    <button id="tabLogin" onclick="switchAuthTab('login')" role="tab" aria-selected="true" class="flex-1 py-2 text-xs font-bold rounded-lg transition-all bg-viking-card text-viking-brightSilver silver-border">Já Sou Cadastrado</button>
                    <button id="tabRegister" onclick="switchAuthTab('register')" role="tab" aria-selected="false" class="flex-1 py-2 text-xs font-bold rounded-lg transition-all text-viking-highlight hover:text-white">Primeiro Acesso</button>
                </div>

                <!-- Form Cadastro / Login -->
                <form id="authForm" onsubmit="handleAuthSubmit(event)" class="space-y-4">
                    <!-- Campo E-mail / Telefone (Apenas no Primeiro Acesso) -->
                    <div id="fieldContactGroup" class="space-y-1 hidden">
                        <label for="inputContact" class="block text-xs font-semibold text-viking-silver">E-mail ou Telefone Valkíria</label>
                        <div class="relative">
                            <input type="text" id="inputContact" placeholder="guerreiro@valhalla.com ou (13) 99999-9999" class="w-full bg-viking-bg border border-viking-silver/30 rounded-lg px-3 py-2.5 text-sm text-white focus:outline-none focus:border-viking-silver transition-all pl-9">
                            <i data-lucide="mail" class="w-4 h-4 text-viking-highlight absolute left-3 top-3"></i>
                        </div>
                    </div>

                    <!-- Campo CPF (Sempre Ativo) -->
                    <div class="space-y-1">
                        <label for="inputCPF" class="block text-xs font-semibold text-viking-silver">CPF do Guerreiro(a) <span class="text-red-400">*</span></label>
                        <div class="relative">
                            <input type="text" id="inputCPF" required placeholder="000.000.000-00" maxlength="14" oninput="formatCPF(this)" class="w-full bg-viking-bg border border-viking-silver/30 rounded-lg px-3 py-2.5 text-sm text-white focus:outline-none focus:border-viking-silver transition-all pl-9">
                            <i data-lucide="id-card" class="w-4 h-4 text-viking-highlight absolute left-3 top-3"></i>
                        </div>
                    </div>

                    <!-- Campo Senha -->
                    <div class="space-y-1">
                        <label for="inputPassword" class="block text-xs font-semibold text-viking-silver">Chave Rúnica (Senha) <span class="text-red-400">*</span></label>
                        <div class="relative">
                            <input type="password" id="inputPassword" required placeholder="••••••••" class="w-full bg-viking-bg border border-viking-silver/30 rounded-lg px-3 py-2.5 text-sm text-white focus:outline-none focus:border-viking-silver transition-all pl-9">
                            <i data-lucide="lock" class="w-4 h-4 text-viking-highlight absolute left-3 top-3"></i>
                        </div>
                    </div>

                    <button type="submit" id="btnAuthSubmit" class="w-full py-3 mt-4 bg-viking-elevated hover:bg-viking-accent border border-viking-silver/40 text-viking-brightSilver font-cinzel font-bold text-sm tracking-widest rounded-xl silver-border-glow transition-all flex items-center justify-center gap-2">
                        <span>Entrar na Taverna</span>
                        <i data-lucide="arrow-right" class="w-4 h-4"></i>
                    </button>
                </form>
            </div>
        </section>

        <!-- TELA 2: DASHBOARD (PÁGINA INICIAL) -->
        <section id="screenDashboard" class="space-y-8 hidden">
            <!-- Boas vindas -->
            <div class="text-center space-y-2 bg-viking-card/60 p-6 rounded-2xl silver-border">
                <h2 class="font-cinzel text-2xl md:text-3xl font-extrabold text-viking-brightSilver tracking-wider">Saudações, Nobre Guerreiro!</h2>
                <p class="text-sm text-viking-highlight max-w-xl mx-auto">Seja bem-vindo ao salão de banquetes do Papudos Marmitos. Escolha seu destino para hoje:</p>
            </div>

            <!-- Três Botões Principais Destacados -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <!-- Botão 1: Cardápio -->
                <button onclick="navigateTo('menu')" class="group p-6 bg-viking-card hover:bg-viking-elevated rounded-2xl silver-border silver-border-glow text-left transition-all duration-300 flex flex-col justify-between h-56 relative overflow-hidden">
                    <div class="space-y-3">
                        <div class="w-12 h-12 rounded-xl bg-viking-elevated group-hover:bg-viking-accent silver-border flex items-center justify-center text-viking-silver">
                            <i data-lucide="utensils-crossed" class="w-6 h-6"></i>
                        </div>
                        <h3 class="font-cinzel text-xl font-bold text-viking-brightSilver">Cardápio Viking</h3>
                        <p class="text-xs text-viking-highlight leading-relaxed">Examine nossos banquetes, carnes nobres grelhadas, poções e hidroméis do Valhalla.</p>
                    </div>
                    <div class="flex items-center gap-2 text-xs font-bold text-viking-silver group-hover:translate-x-1 transition-transform">
                        <span>Explorar Pratos</span>
                        <i data-lucide="chevron-right" class="w-4 h-4"></i>
                    </div>
                </button>

                <!-- Botão 2: Reserva de Mesas -->
                <button onclick="navigateTo('tables')" class="group p-6 bg-viking-card hover:bg-viking-elevated rounded-2xl silver-border silver-border-glow text-left transition-all duration-300 flex flex-col justify-between h-56 relative overflow-hidden">
                    <div class="space-y-3">
                        <div class="w-12 h-12 rounded-xl bg-viking-elevated group-hover:bg-viking-accent silver-border flex items-center justify-center text-viking-silver">
                            <i data-lucide="calendar-check" class="w-6 h-6"></i>
                        </div>
                        <h3 class="font-cinzel text-xl font-bold text-viking-brightSilver">Reserva de Mesas</h3>
                        <p class="text-xs text-viking-highlight leading-relaxed">Garanta seu trono no salão principal. Escolha data, horário e tamanho do seu bando.</p>
                    </div>
                    <div class="flex items-center gap-2 text-xs font-bold text-viking-silver group-hover:translate-x-1 transition-transform">
                        <span>Reservar Trono</span>
                        <i data-lucide="chevron-right" class="w-4 h-4"></i>
                    </div>
                </button>

                <!-- Botão 3: Reserva de Pratos -->
                <button onclick="navigateTo('dishReserve')" class="group p-6 bg-viking-card hover:bg-viking-elevated rounded-2xl silver-border silver-border-glow text-left transition-all duration-300 flex flex-col justify-between h-56 relative overflow-hidden">
                    <div class="space-y-3">
                        <div class="w-12 h-12 rounded-xl bg-viking-elevated group-hover:bg-viking-accent silver-border flex items-center justify-center text-viking-silver">
                            <i data-lucide="sparkles" class="w-6 h-6"></i>
                        </div>
                        <h3 class="font-cinzel text-xl font-bold text-viking-brightSilver">Reserva de Pratos</h3>
                        <p class="text-xs text-viking-highlight leading-relaxed">Garanta iguarias exclusivas do Odin e banquetes lendários com antecedência.</p>
                    </div>
                    <div class="flex items-center gap-2 text-xs font-bold text-viking-silver group-hover:translate-x-1 transition-transform">
                        <span>Garantir Banquete</span>
                        <i data-lucide="chevron-right" class="w-4 h-4"></i>
                    </div>
                </button>
            </div>
        </section>

        <!-- SEÇÃO: CARDÁPIO E RESERVA DE PRATOS -->
        <section id="screenMenu" class="space-y-6 hidden">
            <div class="flex items-center justify-between border-b border-viking-silver/20 pb-4">
                <div>
                    <h2 class="font-cinzel text-2xl font-bold text-viking-brightSilver" id="menuPageTitle">Cardápio do Valhalla</h2>
                    <p class="text-xs text-viking-highlight">Selecione e adicione ao seu Barquinho de compras</p>
                </div>
                <button onclick="navigateTo('dashboard')" class="px-3 py-1.5 rounded-lg bg-viking-elevated silver-border text-xs font-bold flex items-center gap-1 hover:bg-viking-accent">
                    <i data-lucide="arrow-left" class="w-4 h-4"></i> Voltar
                </button>
            </div>

            <!-- Filtros do Cardápio -->
            <div class="flex gap-2 overflow-x-auto pb-2" role="tablist" aria-label="Categorias do Cardápio">
                <button onclick="filterMenu('all')" class="px-4 py-2 rounded-xl text-xs font-bold bg-viking-elevated silver-border text-white">Todos</button>
                <button onclick="filterMenu('banquete')" class="px-4 py-2 rounded-xl text-xs font-bold bg-viking-card hover:bg-viking-elevated text-viking-highlight">Banquetes</button>
                <button onclick="filterMenu('prato')" class="px-4 py-2 rounded-xl text-xs font-bold bg-viking-card hover:bg-viking-elevated text-viking-highlight">Pratos Principais</button>
                <button onclick="filterMenu('bebida')" class="px-4 py-2 rounded-xl text-xs font-bold bg-viking-card hover:bg-viking-elevated text-viking-highlight">Hidromel e Bebidas</button>
            </div>

            <!-- Grid de Itens do Cardápio -->
            <div id="menuItemsGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Injetado dinamicamente pelo JS -->
            </div>
        </section>

        <!-- SEÇÃO: RESERVA DE MESAS -->
        <section id="screenTables" class="space-y-6 hidden">
            <div class="flex items-center justify-between border-b border-viking-silver/20 pb-4">
                <div>
                    <h2 class="font-cinzel text-2xl font-bold text-viking-brightSilver">Reserva de Mesas e Tronos</h2>
                    <p class="text-xs text-viking-highlight">Selecione os detalhes para recepcionarmos seu bando de guerreiros</p>
                </div>
                <button onclick="navigateTo('dashboard')" class="px-3 py-1.5 rounded-lg bg-viking-elevated silver-border text-xs font-bold flex items-center gap-1 hover:bg-viking-accent">
                    <i data-lucide="arrow-left" class="w-4 h-4"></i> Voltar
                </button>
            </div>

            <form onsubmit="handleTableReservation(event)" class="bg-viking-card p-6 rounded-2xl silver-border space-y-6 max-w-2xl mx-auto">
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <!-- Data -->
                    <div class="space-y-1">
                        <label for="tableDate" class="block text-xs font-semibold text-viking-silver">Data do Banquete</label>
                        <input type="date" id="tableDate" required
                        class="w-full bg-viking-bg border border-viking-silver/30 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-viking-silver">
                    </div>

                    <!-- Horário -->
                    <div class="space-y-1">
                        <label for="tableTime" class="block text-xs font-semibold text-viking-silver">Horário da Chegada</label>
                        <select id="tableTime" required class="w-full bg-viking-bg border border-viking-silver/30 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-viking-silver">
                            <option value="">Selecione o horário</option>
                            <option value="18:00">18:00 - Abertura dos Portões</option>
                            <option value="19:30">19:30 - Banquete Noturno</option>
                            <option value="21:00">21:00 - Cerimônia Odin</option>
                            <option value="22:30">22:30 - Ceia Valhalla</option>
                        </select>
                    </div>
                </div>

                <!-- Quantidade de Guerreiros -->
                <div class="space-y-1">
                    <label for="tableGuests" class="block text-xs font-semibold text-viking-silver">Número de Guerreiros (Lugares na Mesa)</label>
                    <select id="tableGuests" required class="w-full bg-viking-bg border border-viking-silver/30 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-viking-silver">
                        <option value="2">Mesa para 2 Guerreiros (Taverna Íntima)</option>
                        <option value="4">Mesa para 4 Guerreiros (Clã)</option>
                        <option value="6">Mesa para 6 Guerreiros (Esquadra Drakkar)</option>
                        <option value="10">Mesa do Rei (Até 10 Guerreiros)</option>
                    </select>
                </div>

                <!-- Observações Especiais -->
                <div class="space-y-1">
                    <label for="tableNotes" class="block text-xs font-semibold text-viking-silver">Pedidos Especiais / Acessibilidade</label>
                    <textarea id="tableNotes" rows="3" placeholder="Ex: Cadeira de rodas, necessidade de assento próximo ao palco rúnico..." class="w-full bg-viking-bg border border-viking-silver/30 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-viking-silver"></textarea>
                </div>

                <button type="submit" class="w-full py-3 bg-viking-elevated hover:bg-viking-accent border border-viking-silver/40 text-viking-brightSilver font-cinzel font-bold text-sm tracking-widest rounded-xl silver-border-glow transition-all flex items-center justify-center gap-2">
                    <i data-lucide="anchor" class="w-4 h-4"></i>
                    <span>Adicionar Reserva de Mesa ao Barquinho</span>
                </button>
            </form>
        </section>

        <!-- TELA 4: PAGAMENTO -->
        <section id="screenCheckout" class="space-y-6 hidden max-w-3xl mx-auto w-full">
            <div class="flex items-center justify-between border-b border-viking-silver/20 pb-4">
                <div>
                    <h2 class="font-cinzel text-2xl font-bold text-viking-brightSilver">Conclusão do Tributo (Pagamento)</h2>
                    <p class="text-xs text-viking-highlight">Escolha como selar o contrato com a taverna</p>
                </div>
                <button onclick="navigateTo('dashboard')" class="px-3 py-1.5 rounded-lg bg-viking-elevated silver-border text-xs font-bold flex items-center gap-1 hover:bg-viking-accent">
                    <i data-lucide="arrow-left" class="w-4 h-4"></i> Voltar
                </button>
            </div>

            <!-- Resumo Rápido -->
            <div class="bg-viking-card p-4 rounded-xl silver-border space-y-2">
                <div class="flex justify-between items-center text-sm">
                    <span class="text-viking-highlight">Total do Barquinho:</span>
                    <span id="checkoutTotal" class="font-cinzel font-bold text-lg text-viking-brightSilver">R$ 0,00</span>
                </div>
            </div>

            <!-- Métodos de Pagamento -->
            <div class="space-y-4">
                <label class="block text-xs font-bold text-viking-silver uppercase tracking-wider">Selecione a Forma de Pagamento:</label>
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <!-- Opção 1: No local -->
                    <button type="button" onclick="selectPaymentMethod('local')" id="payBtnLocal" class="p-4 bg-viking-card hover:bg-viking-elevated rounded-xl silver-border flex flex-col items-center gap-2 text-center transition-all">
                        <i data-lucide="store" class="w-6 h-6 text-viking-silver"></i>
                        <span class="text-xs font-bold">No Local</span>
                        <span class="text-[10px] text-viking-highlight">Pague ao chegar na taverna</span>
                    </button>

                    <!-- Opção 2: Pix -->
                    <button type="button" onclick="selectPaymentMethod('pix')" id="payBtnPix" class="p-4 bg-viking-card hover:bg-viking-elevated rounded-xl silver-border flex flex-col items-center gap-2 text-center transition-all">
                        <i data-lucide="qr-code" class="w-6 h-6 text-viking-silver"></i>
                        <span class="text-xs font-bold">PIX Instantâneo</span>
                        <span class="text-[10px] text-viking-highlight">Aprovação imediata</span>
                    </button>

                    <!-- Opção 3: Cartão Virtual -->
                    <button type="button" onclick="selectPaymentMethod('card')" id="payBtnCard" class="p-4 bg-viking-card hover:bg-viking-elevated rounded-xl silver-border flex flex-col items-center gap-2 text-center transition-all">
                        <i data-lucide="credit-card" class="w-6 h-6 text-viking-silver"></i>
                        <span class="text-xs font-bold">Cartão Virtual</span>
                        <span class="text-[10px] text-viking-highlight">Crédito ou Débito</span>
                    </button>
                </div>
            </div>

            <!-- Painéis Específicos de Pagamento -->
            <div id="paymentDetailsContainer" class="bg-viking-card p-6 rounded-2xl silver-border mt-4">

                <!-- Detalhes Pagamento no Local -->
                <div id="payDetailsLocal" class="space-y-3 text-center">
                    <i data-lucide="coins" class="w-10 h-10 text-viking-silver mx-auto"></i>
                    <h3 class="font-cinzel text-base font-bold">Pagamento Presencial na Taverna</h3>
                    <p class="text-xs text-viking-highlight">Seu pedido e reserva serão garantidos. Apresente seu CPF ao chegar para acertar em Ouro, Cartão ou Pix presencialmente.</p>
                </div>

                <!-- Detalhes PIX -->
                <div id="payDetailsPix" class="space-y-4 text-center hidden">
                    <h3 class="font-cinzel text-base font-bold">Escaneie o QR Code Rúnico</h3>
                    <!-- Simulação QR Code em SVG -->
                    <div class="w-40 h-40 bg-white p-2 mx-auto rounded-xl flex items-center justify-center">
                        <svg class="w-full h-full" viewBox="0 0 100 100">
                            <rect width="100" height="100" fill="white"/>
                            <path d="M10 10h30v30h-30zM15 15h20v20h-20zM60 10h30v30h-30zM65 15h20v20h-20zM10 60h30v30h-30zM15 65h20v20h-20zM45 10h10v10h-10zM45 30h10v20h-10zM10 45h20v10h-20zM60 45h30v10h-30zM50 70h20v20h-20zM80 60h10v30h-10z" fill="black"/>
                        </svg>
                    </div>
                    <div class="space-y-1">
                        <span class="text-[11px] text-viking-highlight block">Chave PIX Aleatória:</span>
                        <div class="flex items-center justify-center gap-2">
                            <code class="bg-viking-bg px-3 py-1.5 rounded border border-viking-silver/30 text-xs font-mono text-viking-brightSilver">pix@papudosmarmitos.com.br</code>
                            <button onclick="copyPixKey()" class="px-3 py-1.5 bg-viking-elevated text-xs rounded hover:bg-viking-accent">Copiar</button>
                        </div>
                    </div>
                </div>

                <!-- Detalhes Cartão Virtual -->
                <div id="payDetailsCard" class="space-y-4 hidden">
                    <h3 class="font-cinzel text-base font-bold text-center">Dados do Cartão Virtual</h3>
                    <div class="space-y-3 max-w-md mx-auto">
                        <div class="space-y-1">
                            <label class="block text-xs font-semibold text-viking-silver">Número do Cartão</label>
                            <input type="text" placeholder="0000 0000 0000 0000" maxlength="19" class="w-full bg-viking-bg border border-viking-silver/30 rounded-lg px-3 py-2 text-sm text-white">
                        </div>
                        <div class="grid grid-cols-2 gap-3">
                            <div class="space-y-1">
                                <label class="block text-xs font-semibold text-viking-silver">Validade (MM/AA)</label>
                                <input type="text" placeholder="12/28" maxlength="5" class="w-full bg-viking-bg border border-viking-silver/30 rounded-lg px-3 py-2 text-sm text-white">
                            </div>
                            <div class="space-y-1">
                                <label class="block text-xs font-semibold text-viking-silver">CVV</label>
                                <input type="password" placeholder="123" maxlength="4" class="w-full bg-viking-bg border border-viking-silver/30 rounded-lg px-3 py-2 text-sm text-white">
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Botão de Confirmação com Ritual Viking -->
            <button onclick="processFinalOrder()" class="w-full py-4 bg-viking-elevated hover:bg-viking-accent border border-viking-silver text-viking-brightSilver font-cinzel font-bold text-base tracking-widest rounded-xl silver-border-glow transition-all flex items-center justify-center gap-2">
                <i data-lucide="flame" class="w-5 h-5 text-viking-silver"></i>
                <span>Selar Pedido com Ritual Viking</span>
            </button>
        </section>

    </main>

    <!-- DRAKKAR DRAWER (CARRINHO DE COMPRAS VIKING LATERAL) -->
    <div id="drakkarDrawer" class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 hidden transition-opacity duration-300" onclick="toggleDrakkarDrawer()">
        <div class="absolute right-0 top-0 bottom-0 w-full max-w-md bg-viking-card border-l border-viking-silver/30 p-6 flex flex-col justify-between shadow-2xl" onclick="event.stopPropagation()">
            
            <!-- Cabeçalho do Carrinho -->
            <div class="flex items-center justify-between border-b border-viking-silver/20 pb-4">
                <div class="flex items-center gap-2">
                    <i data-lucide="anchor" class="w-6 h-6 text-viking-silver"></i>
                    <h3 class="font-cinzel font-bold text-lg text-viking-brightSilver">O Barquinho Viking</h3>
                </div>
                <button onclick="toggleDrakkarDrawer()" aria-label="Fechar carrinho Barquinho" class="p-1 rounded-lg hover:bg-viking-elevated">
                    <i data-lucide="x" class="w-5 h-5 text-viking-highlight"></i>
                </button>
            </div>

            <!-- Lista de Itens do Barquinho -->
            <div id="drakkarItemsList" class="flex-grow my-4 overflow-y-auto space-y-3 pr-1">
                <!-- Injetado Dinamicamente -->
            </div>

            <!-- Rodapé e Finalização -->
            <div class="border-t border-viking-silver/20 pt-4 space-y-4">
                <div class="space-y-1">
                    <div class="flex justify-between text-xs text-viking-highlight">
                        <span>Subtotal das Iguarias:</span>
                        <span id="drakkarSubtotal">R$ 0,00</span>
                    </div>
                    <div class="flex justify-between text-base font-bold text-viking-brightSilver">
                        <span>Total do Barquinho:</span>
                        <span id="drakkarTotal" class="font-cinzel text-lg">R$ 0,00</span>
                    </div>
                </div>

                <button onclick="goToCheckout()" class="w-full py-3 bg-viking-elevated hover:bg-viking-accent border border-viking-silver/40 text-viking-brightSilver font-cinzel font-bold text-sm tracking-wider rounded-xl silver-border-glow transition-all flex items-center justify-center gap-2">
                    <span>Avançar para Pagamento</span>
                    <i data-lucide="arrow-right" class="w-4 h-4"></i>
                </button>
            </div>
        </div>
    </div>

    <!-- MODAL LIBRAS & SUPORTE EM TEXTO -->
    <div id="librasModal" class="fixed inset-0 bg-black/80 z-50 flex items-center justify-center p-4 hidden" onclick="closeLibrasModal()">
        <div class="bg-viking-card border border-viking-silver/40 p-6 rounded-2xl max-w-lg w-full space-y-4 shadow-2xl relative" onclick="event.stopPropagation()">
            <div class="flex justify-between items-center border-b border-viking-silver/20 pb-3">
                <div class="flex items-center gap-2">
                    <i data-lucide="hand" class="w-6 h-6 text-viking-silver"></i>
                    <h3 class="font-cinzel font-bold text-lg">Assistente LIBRAS e Texto</h3>
                </div>
                <button onclick="closeLibrasModal()" class="p-1 rounded hover:bg-viking-elevated"><i data-lucide="x" class="w-5 h-5"></i></button>
            </div>

            <div class="aspect-video bg-viking-bg rounded-xl border border-viking-silver/20 flex flex-col items-center justify-center p-4 text-center space-y-2">
                <i data-lucide="video" class="w-10 h-10 text-viking-silver animate-pulse"></i>
                <p class="text-xs font-semibold text-viking-brightSilver">Intérprete Virtual de LIBRAS Conectado</p>
                <p class="text-[11px] text-viking-highlight">O intérprete fará a tradução em sinais de todas as opções de reservas e pratos selecionados.</p>
            </div>

            <div class="bg-viking-elevated p-3 rounded-lg border border-viking-silver/10 space-y-1">
                <span class="text-xs font-bold text-viking-silver block">Suporte Direto por Texto em Tempo Real:</span>
                <p class="text-xs text-viking-highlight">Caso necessite de atendimento especial surdo-mudo, nossa equipe de recepção está pronta para chat direto ao chegar na taverna.</p>
            </div>
        </div>
    </div>

    <!-- MODAL CÓDIGOS FONTE VS CODE (HTML, CSS, JS, SQL) -->
    <div id="devModal" class="fixed inset-0 bg-black/85 backdrop-blur-md z-50 flex items-center justify-center p-2 sm:p-4 hidden" onclick="closeDevModal()">
        <div class="bg-viking-card border border-viking-silver/50 rounded-2xl max-w-5xl w-full h-[85vh] flex flex-col justify-between shadow-2xl overflow-hidden" onclick="event.stopPropagation()">
            
            <!-- Topbar Modal VS Code -->
            <div class="bg-viking-elevated px-4 py-3 border-b border-viking-silver/20 flex flex-wrap items-center justify-between gap-2">
                <div class="flex items-center gap-2">
                    <i data-lucide="code-2" class="w-5 h-5 text-viking-silver"></i>
                    <h3 class="font-cinzel font-bold text-sm sm:text-base text-viking-brightSilver">Painel de Código Fonte para VS Code</h3>
                </div>
                <button onclick="closeDevModal()" class="p-1 rounded hover:bg-viking-accent"><i data-lucide="x" class="w-5 h-5"></i></button>
            </div>

            <!-- Abas do Código Fonte -->
            <div class="flex bg-viking-bg border-b border-viking-silver/20 px-4 pt-2 gap-2 overflow-x-auto">
                <button onclick="switchCodeTab('html')" id="codeTabHtml" class="px-4 py-2 text-xs font-mono font-bold rounded-t-lg bg-viking-card border-t border-x border-viking-silver/30 text-viking-brightSilver">index.html</button>
                <button onclick="switchCodeTab('css')" id="codeTabCss" class="px-4 py-2 text-xs font-mono font-bold rounded-t-lg text-viking-highlight hover:text-white">style.css</button>
                <button onclick="switchCodeTab('js')" id="codeTabJs" class="px-4 py-2 text-xs font-mono font-bold rounded-t-lg text-viking-highlight hover:text-white">script.js</button>
                <button onclick="switchCodeTab('sql')" id="codeTabSql" class="px-4 py-2 text-xs font-mono font-bold rounded-t-lg text-viking-highlight hover:text-white">banco_de_dados.sql</button>
            </div>

            <!-- Área do Código com Scroll -->
            <div class="flex-grow p-4 bg-[#05050A] font-mono text-xs overflow-auto relative">
                <button onclick="copyCodeSnippet()" class="absolute top-6 right-6 px-3 py-1.5 bg-viking-elevated silver-border rounded hover:bg-viking-accent text-xs flex items-center gap-1.5 z-10">
                    <i data-lucide="copy" class="w-3.5 h-3.5"></i>
                    <span>Copiar Código</span>
                </button>
                <pre><code id="codeViewer" class="text-viking-silver leading-relaxed whitespace-pre-wrap"></code></pre>
            </div>

            <!-- Footer Modal -->
            <div class="bg-viking-elevated px-4 py-2 border-t border-viking-silver/20 flex justify-between items-center text-[11px] text-viking-highlight">
                <span>Estrutura Pronta para Desenvolvimento Web Completo</span>
                <span>Papudos Marmitos v2.0</span>
            </div>
        </div>
    </div>

    <!-- RODAPÉ DA TAVERNA -->
    <footer class="bg-viking-card/80 border-t border-viking-silver/20 py-4 px-4 text-center text-xs text-viking-highlight space-y-1">
        <p class="font-cinzel text-viking-brightSilver">Papudos Marmitos - Taverna Viking Refinada © 2026</p>
        <p>Acessibilidade Universal | Projeto com Suporte Web Speech API & LIBRAS</p>
    </footer>

    <!-- LOGICA JAVASCRIPT PRINCIPAL -->
    <script>
        // ESTADO GLOBAL DA APLICAÇÃO
        let appState = {
            voiceEnabled: false,
            highContrast: false,
            fontSizeLevel: 0, // -1, 0, +1
            cart: [],
            menu: [
                { id: 1, title: 'Banquete Valhalla Supremus', category: 'banquete', price: 189.90, desc: 'Costela bovina defumada em lenha nobre, javali assado, pães de centeio e hidromel real.', icon: 'crown' },
                { id: 2, title: 'Prato Especial do Odin', category: 'prato', price: 89.90, desc: 'Filé de salmão grelhado na pedra vulcânica com purê de raízes rúnicas.', icon: 'fish' },
                { id: 3, title: 'Marmita do Guerreiro Ragnar', category: 'prato', price: 49.90, desc: 'Pernil suíno temperado em ervas nórdicas, arroz selvagem e vegetais rústicos.', icon: 'drumstick' },
                { id: 4, title: 'Garrafa de Hidromel dos Deuses (750ml)', category: 'bebida', price: 65.00, desc: 'Fermentado ancestral de mel silvestre maturado em barris de carvalho.', icon: 'wine' },
                { id: 5, title: 'Poção Rúnica de Frutas Vermelhas', category: 'bebida', price: 18.00, desc: 'Bebida artesanal revigorante sem álcool para os grandes guerreiros.', icon: 'cup-soda' }
            ]
        };

        // INICIALIZAÇÃO
        window.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();
            renderMenuItems('all');
            updateCartUI();
        });

        // 1. VOIZ / ACCESSIBILIDADE DE AUDIO (Web Speech API)
        function toggleVoiceReadout() {
            appState.voiceEnabled = !appState.voiceEnabled;
            const statusEl = document.getElementById('voiceStatusText');
            statusEl.innerText = appState.voiceEnabled ? 'Voz: ON' : 'Voz: OFF';

            if (appState.voiceEnabled) {
                speakText("Leitor de voz ativado com sucesso. Os principais botões e alertas do aplicativo serão lidos.");
            } else {
                window.speechSynthesis.cancel();
            }
        }

        function speakText(text) {
            if (!appState.voiceEnabled || !('speechSynthesis' in window)) return;
            window.speechSynthesis.cancel(); // Parar falas anteriores
            const utterance = new SpeechSynthesisUtterance(text);
            utterance.lang = 'pt-BR';
            utterance.rate = 1.0;
            window.speechSynthesis.speak(utterance);
        }

        // 2. AJUSTE DE FONTE E ALTO CONTRASSTE
        function changeFontSize(delta) {
            const body = document.body;
            if (delta === 0) {
                body.style.fontSize = '16px';
                appState.fontSizeLevel = 0;
            } else {
                appState.fontSizeLevel += delta;
                if (appState.fontSizeLevel > 2) appState.fontSizeLevel = 2;
                if (appState.fontSizeLevel < -1) appState.fontSizeLevel = -1;
                
                const newSize = 16 + (appState.fontSizeLevel * 2);
                body.style.fontSize = newSize + 'px';
            }
            speakText("Tamanho do texto alterado");
        }

        function resetFontSize() {
            changeFontSize(0);
        }

        function toggleHighContrast() {
            appState.highContrast = !appState.highContrast;
            document.body.classList.toggle('high-contrast', appState.highContrast);
            speakText(appState.highContrast ? "Modo alto contraste ativado" : "Modo alto contraste desativado");
        }

        // 3. ATENDIMENTO LIBRAS
        function openLibrasModal() {
            document.getElementById('librasModal').classList.remove('hidden');
            speakText("Modal de assistência em Libras aberto");
        }

        function closeLibrasModal() {
            document.getElementById('librasModal').classList.add('hidden');
        }

        // 4. MASCARA CPF
        function formatCPF(input) {
            let value = input.value.replace(/\D/g, "");
            if (value.length > 11) value = value.slice(0, 11);
            value = value.replace(/(\d{3})(\d)/, "$1.$2");
            value = value.replace(/(\d{3})(\d)/, "$1.$2");
            value = value.replace(/(\d{3})(\d{1,2})$/, "$1-$2");
            input.value = value;
        }

        // 5. TELAS DE AUTENTICAÇÃO (LOGIN / CADASTRO)
        function switchAuthTab(tab) {
            const isReg = tab === 'register';
            document.getElementById('fieldContactGroup').classList.toggle('hidden', !isReg);
            
            document.getElementById('tabLogin').className = isReg 
                ? "flex-1 py-2 text-xs font-bold rounded-lg transition-all text-viking-highlight hover:text-white"
                : "flex-1 py-2 text-xs font-bold rounded-lg transition-all bg-viking-card text-viking-brightSilver silver-border";

            document.getElementById('tabRegister').className = isReg 
                ? "flex-1 py-2 text-xs font-bold rounded-lg transition-all bg-viking-card text-viking-brightSilver silver-border"
                : "flex-1 py-2 text-xs font-bold rounded-lg transition-all text-viking-highlight hover:text-white";

            document.getElementById('btnAuthSubmit').querySelector('span').innerText = isReg ? 'Cadastrar e Entrar' : 'Entrar na Taverna';
            speakText(isReg ? "Aba de primeiro acesso selecionada" : "Aba de cliente já cadastrado selecionada");
        }

        function handleAuthSubmit(event) {
            event.preventDefault();
            speakText("Acesso permitido. Bem-vindo ao salão nobre Papudos Marmitos");
            navigateTo('dashboard');
        }

        // 6. NAVEGAÇÃO ENTRE TELAS
        function navigateTo(screenName) {
            const screens = ['screenAuth', 'screenDashboard', 'screenMenu', 'screenTables', 'screenCheckout'];
            screens.forEach(s => document.getElementById(s).classList.add('hidden'));

            if (screenName === 'dashboard') {
                document.getElementById('screenDashboard').classList.remove('hidden');
                speakText("Página inicial da Taverna. Escolha entre Cardápio, Reserva de Mesas ou Reserva de Pratos.");
            } else if (screenName === 'menu') {
                document.getElementById('menuPageTitle').innerText = 'Cardápio Completo Valhalla';
                document.getElementById('screenMenu').classList.remove('hidden');
                speakText("Exibindo Cardápio Viking");
            } else if (screenName === 'dishReserve') {
                document.getElementById('menuPageTitle').innerText = 'Reserva Antecipada de Pratos Nobres';
                document.getElementById('screenMenu').classList.remove('hidden');
                speakText("Exibindo Tela de Reserva de Pratos e Banquetes Especializados");
            } else if (screenName === 'tables') {
                document.getElementById('screenTables').classList.remove('hidden');
                speakText("Tela de Reserva de Mesas e Tronos");
            } else if (screenName === 'checkout') {
                document.getElementById('screenCheckout').classList.remove('hidden');
                speakText("Página de pagamento do tributo");
            }
        }

        // 7. RENDERIZAÇÃO DO CARDÁPIO E PRATOS
        function renderMenuItems(category) {
            const container = document.getElementById('menuItemsGrid');
            container.innerHTML = '';

            const filtered = category === 'all' 
                ? appState.menu 
                : appState.menu.filter(i => i.category === category);

            filtered.forEach(item => {
                const card = document.createElement('div');
                card.className = "bg-viking-card p-5 rounded-2xl silver-border flex flex-col justify-between space-y-4 hover:border-viking-silver/60 transition-all";
                card.innerHTML = `
                    <div class="space-y-2">
                        <div class="flex justify-between items-start">
                            <div class="w-10 h-10 rounded-xl bg-viking-elevated silver-border flex items-center justify-center text-viking-silver">
                                <i data-lucide="${item.icon}" class="w-5 h-5"></i>
                            </div>
                            <span class="font-cinzel font-bold text-sm text-viking-brightSilver">R$ ${item.price.toFixed(2)}</span>
                        </div>
                        <h3 class="font-cinzel font-bold text-base text-viking-brightSilver">${item.title}</h3>
                        <p class="text-xs text-viking-highlight leading-relaxed">${item.desc}</p>
                    </div>
                    <button onclick="addToCart(${item.id}, '${item.title}', ${item.price})" class="w-full py-2 bg-viking-elevated hover:bg-viking-accent border border-viking-silver/30 rounded-xl text-xs font-bold text-viking-brightSilver flex items-center justify-center gap-1.5 transition-all">
                        <i data-lucide="plus" class="w-4 h-4"></i>
                        <span>Adicionar ao Barquinho</span>
                    </button>
                `;
                container.appendChild(card);
            });
            lucide.createIcons();
        }

        function filterMenu(cat) {
            renderMenuItems(cat);
        }

        // 8. GERENCIAMENTO DO BARQUINHO (CARRINHO)
        function addToCart(id, title, price, extraInfo = '') {
            const existing = appState.cart.find(i => i.id === id && i.extraInfo === extraInfo);
            if (existing) {
                existing.qty++;
            } else {
                appState.cart.push({ id, title, price, qty: 1, extraInfo });
            }
            updateCartUI();
            speakText(`${title} adicionado ao Barquinho`);
        }

        function updateCartQty(index, delta) {
            appState.cart[index].qty += delta;
            if (appState.cart[index].qty <= 0) {
                appState.cart.splice(index, 1);
            }
            updateCartUI();
        }

        function updateCartUI() {
            const listEl = document.getElementById('drakkarItemsList');
            const badge = document.getElementById('drakkarBadge');
            const subtotalEl = document.getElementById('drakkarSubtotal');
            const totalEl = document.getElementById('drakkarTotal');
            const checkoutTotalEl = document.getElementById('checkoutTotal');

            listEl.innerHTML = '';
            let total = 0;
            let count = 0;

            if (appState.cart.length === 0) {
                listEl.innerHTML = `
                    <div class="text-center py-10 space-y-2 text-viking-highlight">
                        <i data-lucide="anchor" class="w-10 h-10 mx-auto stroke-1"></i>
                        <p class="text-xs">O Barquinho Viking está vazio.</p>
                    </div>
                `;
            } else {
                appState.cart.forEach((item, idx) => {
                    total += item.price * item.qty;
                    count += item.qty;

                    const row = document.createElement('div');
                    row.className = "bg-viking-elevated p-3 rounded-xl border border-viking-silver/20 flex justify-between items-center";
                    row.innerHTML = `
                        <div class="space-y-0.5">
                            <h4 class="text-xs font-bold text-viking-brightSilver">${item.title}</h4>
                            ${item.extraInfo ? `<p class="text-[10px] text-viking-highlight">${item.extraInfo}</p>` : ''}
                            <span class="text-xs text-viking-silver font-semibold">R$ ${(item.price * item.qty).toFixed(2)}</span>
                        </div>
                        <div class="flex items-center gap-2 bg-viking-bg rounded-lg border border-viking-silver/20 px-2 py-1">
                            <button onclick="updateCartQty(${idx}, -1)" class="text-xs font-bold hover:text-red-400">-</button>
                            <span class="text-xs font-bold">${item.qty}</span>
                            <button onclick="updateCartQty(${idx}, 1)" class="text-xs font-bold hover:text-green-400">+</button>
                        </div>
                    `;
                    listEl.appendChild(row);
                });
            }

            badge.innerText = count;
            subtotalEl.innerText = `R$ ${total.toFixed(2)}`;
            totalEl.innerText = `R$ ${total.toFixed(2)}`;
            checkoutTotalEl.innerText = `R$ ${total.toFixed(2)}`;
            lucide.createIcons();
        }

        function toggleDrakkarDrawer() {
            const drawer = document.getElementById('drakkarDrawer');
            drawer.classList.toggle('hidden');
            if (!drawer.classList.contains('hidden')) {
                speakText("Barquinho Viking aberto com o resumo dos seus itens.");
            }
        }

        // 9. RESERVA DE MESAS
        function handleTableReservation(e) {
            e.preventDefault();
            const date = document.getElementById('tableDate').value;
            const time = document.getElementById('tableTime').value;
            const guests = document.getElementById('tableGuests').value;

            const title = `Reserva de Mesa (${guests} Guerreiros)`;
            const extraInfo = `Data: ${date} às ${time}`;

            addToCart(`table-${Date.now()}`, title, 0.00, extraInfo);
            speakText("Reserva de mesa adicionada ao Barquinho com sucesso.");
            toggleDrakkarDrawer();
        }

        // 10. METODOS DE PAGAMENTO
        function selectPaymentMethod(method) {
            document.getElementById('payDetailsLocal').classList.add('hidden');
            document.getElementById('payDetailsPix').classList.add('hidden');
            document.getElementById('payDetailsCard').classList.add('hidden');

            if (method === 'local') {
                document.getElementById('payDetailsLocal').classList.remove('hidden');
                speakText("Pagamento no local selecionado.");
            } else if (method === 'pix') {
                document.getElementById('payDetailsPix').classList.remove('hidden');
                speakText("Pagamento via PIX selecionado.");
            } else if (method === 'card') {
                document.getElementById('payDetailsCard').classList.remove('hidden');
                speakText("Pagamento com Cartão Virtual selecionado.");
            }
        }

        function copyPixKey() {
            navigator.clipboard.writeText("pix@papudosmarmitos.com.br");
            speakText("Chave PIX copiada para a área de transferência.");
        }

        function goToCheckout() {
            toggleDrakkarDrawer();
            navigateTo('checkout');
        }

        function processFinalOrder() {
            if (appState.cart.length === 0) {
                speakText("Seu Barquinho está vazio. Adicione pratos ou reservas antes de finalizar.");
                return;
            }
            speakText("Ritual de pedido concluído com sucesso! Os deuses do Valhalla aguardam sua chegada.");
            alert("⚔️ RITUAL CONCLUÍDO DA RESERVA ⚔️\n\nSeu pedido foi gravado nas runas de Papudos Marmitos! Apresente seu CPF ao chegar.");
            appState.cart = [];
            updateCartUI();
            navigateTo('dashboard');
        }

        // 11. PAINEL DE CÓDIGOS PARA VS CODE
        const codeSnippets = {
            html: `<!-- ========================================== -->
<!-- PAPUDOS MARMITOS - INDEX.HTML (VS CODE)    -->
<!-- ========================================== -->
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Papudos Marmitos - Taverna Viking</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header role="banner">
        <h1>PAPUDOS MARMITOS</h1>
        <button id="btnVoice">Leitor de Voz</button>
    </header>

    <main id="app">
        <!-- Container Principal -->
    </main>

    <script src="script.js"><\/script>
</body>
</html>`,
            css: `/* ========================================== */
/* PAPUDOS MARMITOS - STYLE.CSS (VS CODE)     */
/* Paleta: Azul Noturno, Preto e Prata       */
/* ========================================== */
:root {
    --bg-dark: #05050A;
    --card-dark: #0B132B;
    --elevated-dark: #1C2541;
    --accent-blue: #3A506B;
    --silver: #CBD5E1;
    --bright-silver: #F8FAFC;
}

body {
    background-color: var(--bg-dark);
    color: var(--bright-silver);
    font-family: 'Plus Jakarta Sans', sans-serif;
    margin: 0;
}

.silver-border {
    border: 1px solid rgba(203, 213, 225, 0.25);
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.8);
}

.high-contrast {
    background-color: #000000 !important;
    color: #FFFFFF !important;
}`,
            js: `// ==========================================
// PAPUDOS MARMITOS - SCRIPT.JS (VS CODE)     
// ==========================================
const cart = [];

function speak(text) {
    if ('speechSynthesis' in window) {
        const synth = new SpeechSynthesisUtterance(text);
        synth.lang = 'pt-BR';
        window.speechSynthesis.speak(synth);
    }
}

function addToCart(item) {
    cart.push(item);
    speak(item.name + " adicionado ao Barquinho");
}`,
            sql: `-- ========================================================
-- PAPUDOS MARMITOS - BANCO_DE_DADOS.SQL (MYSQL / VS CODE)
-- ========================================================

CREATE DATABASE IF NOT EXISTS papudos_marmitos_db;
USE papudos_marmitos_db;

-- 1. Tabela de Clientes
CREATE TABLE clientes (
    id_cliente INT AUTO_INCREMENT PRIMARY KEY,
    cpf VARCHAR(14) NOT NULL UNIQUE,
    email_telefone VARCHAR(150),
    senha_hash VARCHAR(255) NOT NULL,
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 2. Tabela de Mesas da Taverna
CREATE TABLE mesas (
    id_mesa INT AUTO_INCREMENT PRIMARY KEY,
    numero_mesa INT NOT NULL UNIQUE,
    capacidade INT NOT NULL,
    status ENUM('livre', 'reservada', 'manutencao') DEFAULT 'livre'
);

-- 3. Tabela do Cardápio de Pratos
CREATE TABLE pratos (
    id_prato INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    categoria ENUM('banquete', 'prato', 'bebida') NOT NULL,
    preco DECIMAL(10, 2) NOT NULL,
    descricao TEXT
);

-- 4. Tabela de Reservas de Mesas
CREATE TABLE reservas_mesas (
    id_reserva_mesa INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT NOT NULL,
    id_mesa INT NOT NULL,
    data_reserva DATE NOT NULL,
    horario TIME NOT NULL,
    qtd_guerreiros INT NOT NULL,
    observacoes TEXT,
    FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente),
    FOREIGN KEY (id_mesa) REFERENCES mesas(id_mesa)
);

-- 5. Tabela de Pedidos Principais
CREATE TABLE pedidos (
    id_pedido INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT NOT NULL,
    valor_total DECIMAL(10, 2) NOT NULL,
    metodo_pagamento ENUM('local', 'pix', 'cartao_virtual') NOT NULL,
    status_pedido ENUM('pendente', 'confirmado', 'concluido') DEFAULT 'pendente',
    data_pedido TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente)
);

-- 6. Tabela de Itens do Pedido (Relacionamento Pratos <-> Pedido)
CREATE TABLE itens_pedido (
    id_item INT AUTO_INCREMENT PRIMARY KEY,
    id_pedido INT NOT NULL,
    id_prato INT NOT NULL,
    quantidade INT NOT NULL,
    preco_unitario DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (id_pedido) REFERENCES pedidos(id_pedido),
    FOREIGN KEY (id_prato) REFERENCES pratos(id_prato)
);`
        };

        function openDevModal() {
            document.getElementById('devModal').classList.remove('hidden');
            switchCodeTab('html');
            speakText("Painel de códigos fonte para VS Code aberto.");
        }

        function closeDevModal() {
            document.getElementById('devModal').classList.add('hidden');
        }

        function switchCodeTab(lang) {
            const tabs = ['html', 'css', 'js', 'sql'];
            tabs.forEach(t => {
                const btn = document.getElementById(`codeTab${t.charAt(0).toUpperCase() + t.slice(1)}`);
                if (t === lang) {
                    btn.className = "px-4 py-2 text-xs font-mono font-bold rounded-t-lg bg-viking-card border-t border-x border-viking-silver/30 text-viking-brightSilver";
                } else {
                    btn.className = "px-4 py-2 text-xs font-mono font-bold rounded-t-lg text-viking-highlight hover:text-white";
                }
            });

            document.getElementById('codeViewer').innerText = codeSnippets[lang];
        }

        function copyCodeSnippet() {
            const codeText = document.getElementById('codeViewer').innerText;
            navigator.clipboard.writeText(codeText);
            speakText("Código copiado para a área de transferência.");
        }
    </script>
</body>
</html>
