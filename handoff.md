# Documento de Transição (handoff.md)

Este documento apresenta o estado atual do projeto **"Curso de Extensão NEEI/UERJ 2026: Calendário Interativo"** e serve como guia de transição para o próximo desenvolvedor ou agente que assumir a manutenção do código.

---

## 📋 Status do Projeto

O desenvolvimento do calendário interativo unificado foi concluído com sucesso, cobrindo todos os requisitos acadêmicos, de marca e de internacionalização. O produto final é uma página única de altíssimo apelo visual (**Glassmorphism**) e otimização cirúrgica para visualização em celulares.

---

## 🌟 Funcionalidades Prontas e Entregues

### 1. Adequação da Carga Horária (Exatamente 100 horas)
* Ajustamos a carga horária do **Trabalho Final do Módulo 3** de forma assíncrona para exatamente **9 horas**, somando um total de **17 horas** para o Módulo 3 e totalizando precisamente **100 horas** em todo o curso (ajustando a discrepância de 1 hora a mais detectada no cronograma original).
* Expandimos todas as abreviações de carga horária para texto completo (ex: *"2 horas Síncronas + 2 horas Assíncronas"*), conforme diretriz de clareza.

### 2. Alinhamento de Identidade Visual e Links
* Nome do curso padronizado em todas as instâncias como: **"Curso de Extensão NEEI/UERJ 2026"**.
* Distintivo da barra lateral ajustado para **"Calendário Interativo"**.
* Integração direta da sala do **Google Classroom** oficial (`https://classroom.google.com/c/ODY0NDUzNjc2OTI1`) em múltiplos botões interativos e links de ação rápida.
* Banco de dados de docentes e colaboradores integrado a partir do arquivo PDF do curso, exibindo nomes completos e links dinâmicos para os respectivos **Currículos Lattes**.
* Novo diretório de ativos **`assets/images/`** criado para conter o arquivo **`logos.png`** (logotipos oficiais da UERJ/NEEI), garantindo que a pasta local **`docs/`** (que não será enviada para o deploy) fique isolada e que a build de produção seja 100% autônoma.

### 3. Integração de Fuso Horário Internacional (Moçambique - Opção 2)
* Implementação de exibição dual permanente (Brasil/Moçambique) sem o uso do termo "Madrugada".
* **Mecânica do Fuso**: Aulas ocorrem nas quintas-feiras às 19:00 BRT no Brasil, o que equivale a **Sextas-feiras às 00:00 CAT** em Maputo (Moçambique).
* O sistema calcula dinamicamente a data futura no território moçambicano somando +1 dia no objeto JavaScript, exibindo com as bandeiras oficiais 🇧🇷 e 🇲🇿 na Sidebar, no banner de destaque das próximas aulas (Spotlight) e na gaveta lateral de detalhes (Drawer).

### 4. Otimização Cirúrgica Mobile-First
* **Branding Compacto**: Ocultação automática de subtítulos e descrições longas em smartphones para economizar a área útil inicial da tela.
* **Listas Horizontais Swipeable (Deslizantes)**: O grid de estatísticas da sidebar e o menu vertical com 8 filtros de módulos convertem-se em listagens horizontais de rolagem suave com o polegar em celulares (estilo app Spotify/YouTube), otimizando radicalmente a rolagem vertical.
* **Aspect-Ratio Quadrado**: Células de dias do calendário (`.day-cell`) ajustam-se com proporção de tela `1:1` em celulares para emular o design de calendários nativos de smartphones e evitar toques acidentais.
* **Gaveta com Barra de Arraste (Bottom Sheet Drag Handle)**: O Drawer lateral de detalhes transforma-se em um painel que desliza de baixo para cima com uma barra cinza de arraste no topo, gerando familiaridade visual de aplicativo mobile.
* **Tema Padrão (Modo Escuro)**: Configurado o Modo Escuro (*Dark Mode*) como o padrão de carregamento inicial absoluto (caso não existam escolhas salvas no `localStorage`), destacando o design tokens premium do projeto e atualizando programaticamente o botão ativo correspondente na barra de aparência. O rótulo **"Aparência"** recebeu um ícone de sol (SVG com `currentColor`, acompanhando o tema).

---

## 🔎 Revisão de Design e Acessibilidade (2026-05-24)

Rodada de auditoria visual (desktop 1440px, mobile 375px e estados do Drawer) com correções implementadas e validadas em navegador:

* **Reordenação Mobile (foco no dashboard)**: No mobile/tablet (`≤1024px`), a `.sidebar` passou a usar `display: contents` e seus filhos são reordenados via `order`. A ordem visual agora é: branding → estatísticas → busca → filtros → **Spotlight + Calendário** → blocos secundários (Google Classroom, parceria institucional e seletor de tema), que descem para o rodapé. O calendário, que antes começava a ~1257px de rolagem, passou a aparecer a ~874px. **O layout desktop (grid de 2 colunas) permanece inalterado.**
* **Drawer com Scrim + Acessibilidade**: Adicionado overlay semi-transparente (`#drawerOverlay`) que escurece/desfoca o conteúdo atrás do painel. O Drawer recebeu `role="dialog"`/`aria-modal`, **focus trap** no Tab, foco que entra no painel ao abrir e retorna ao gatilho ao fechar, e fechamento por **ESC** e **clique no scrim** (vale para o painel lateral no desktop e o bottom-sheet no mobile). Lógica centralizada em `openDrawer()` / `closeDrawer()`.
* **Legibilidade do Calendário**: Abreviações dos dias da semana trocadas de `D S T Q Q S S` (ambíguas) para `DOM SEG TER QUA QUI SEX SÁB`. Dias de feriado agora usam vermelho de contraste adequado e sensível ao tema via token `--holiday-color` (`#f87171` no escuro, `#dc2626` no claro), em negrito e com anel de contorno mais visível.

---

## 🛠️ Detalhes da Arquitetura Técnica

* **Core Stack**: HTML5 semântico, CSS3 (organizado por **Cascade Layers** no arquivo `index.html`) e Vanilla JavaScript (sem frameworks externos, garantindo carregamento instantâneo offline).
* **Date Engine**: A construção do calendário mensal de maio a dezembro de 2026 é feita por algoritmos JavaScript que interpretam a array `COURSE_EVENTS` e calculam o primeiro dia de cada mês no grid 7x6 do calendário gregoriano.
* **Integrações de Agenda**:
  * **Google Agenda**: Constrói dinamicamente URLs de convites com parâmetros de evento, data, descrição sanitizada (sem tags HTML) e local.
  * **ICS Invites**: Um compilador JavaScript nativo gera arquivos de convite `.ics` em formato Blob e aciona o download automático para importação direta no Apple Calendar ou Outlook do smartphone.

---

## 🚀 Próximos Passos & Sugestões de Evolução

1. **Substituição por Links Reais do Meet**: Atualmente, os botões *"Entrar na Sala Virtual"* direcionam para o Google Classroom. Conforme o curso avançar, os links diretos de cada transmissão/sala do Google Meet podem ser associados às chaves de cada aula na array `COURSE_EVENTS`.
2. **Deploy Estático**: Por se tratar de um arquivo único (`index.html`) acompanhado apenas da pasta de ativos (`assets/`), o projeto está 100% pronto para ser hospedado gratuitamente no GitHub Pages, Vercel ou Netlify em menos de 1 minuto (a pasta local `docs/` não deve subir para a hospedagem de produção).
3. **Auditoria de Acessibilidade Adicional**: A rodada de 2026-05-24 já cobriu focus trap no Drawer, contraste de feriados e clareza dos dias da semana. Como evolução, realizar testes contínuos com leitores de tela em celulares e validar o contraste do tema **Claro** (botão "Claro"), garantindo inclusão máxima para todos os estudantes.
