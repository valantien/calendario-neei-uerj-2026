# Guia de Agentes de IA (AGENTS.md)

Este documento destina-se a futuros agentes de Inteligência Artificial ou assistentes de codificação (como Antigravity) que venham a colaborar neste repositório. Ele explica as diretrizes de design, arquitetura e convenções técnicas aplicadas ao projeto **"Curso de Extensão NEEI/UERJ 2026: Calendário Interativo"**.

---

## 🤖 Perfil do Agente e Diretrizes Operacionais

Ao trabalhar neste projeto, você deve assumir o papel de um engenheiro front-end sênior especializado em **Modern Web Guidance** e design de interfaces premium.

### Diretrizes de Comportamento
1. **Idioma do Repositório**: Toda a interface visível ao usuário, dados de aulas, nomes de professores e textos do painel interativo devem permanecer em **Português (pt-BR)** de alto nível.
2. **Preservação de Estilo**: O design segue o conceito de **Glassmorphism** premium. Não quebre a harmonia das cores de módulos ou as transparências com CSS ad-hoc. Use sempre as variáveis de design tokens declaradas em `:root`.
3. **Arquitetura de Arquivo Único**: O aplicativo é contido em um único arquivo `index.html`. Não introduza frameworks complexos ou dependências de build (como webpack/vite/npm) a menos que explicitamente solicitado pelo usuário. O projeto deve rodar diretamente no navegador, sem compilação.
4. **Foco Mobile-First**: O aplicativo é otimizado para celulares. Qualquer nova alteração visual no menu lateral ou no calendário deve ser validada sob a ótica de usabilidade em smartphones (especialmente os swipes horizontais e tamanhos de alvos de toque).

---

## 🎨 Especificações de Design (Design Tokens)

O projeto utiliza a especificação de camadas em CSS (`@layer reset, design-tokens, base, layouts, components, utilities`) para manter a legibilidade das folhas de estilo e evitar colisões.

### Variáveis CSS Importantes (`:root`)
* **Fontes**: `Outfit` para títulos e cabeçalhos; `Inter` para legibilidade de textos longos.
* **Módulos**: Cada módulo acadêmico possui uma cor RGB específica mapeada em variáveis CSS (ex: `--color-m5-rgb` para Chatbot IARA, `--color-m3-rgb` para CIF). Utilize essas variáveis com transparências para criar efeitos de hover consistentes.
* **Temas**: Suporte a auto-detecção de tema escuro/claro (`color-scheme: dark light`) com variáveis ajustadas sob `@media (prefers-color-scheme)`.

---

## 🛠️ Arquitetura de Interação

1. **Date Math**: O gerador de meses calcula dinamicamente os grids mensais de maio a dezembro de 2026. Se precisar adicionar eventos em novos meses, atualize a constante `COURSE_EVENTS` e ajuste a array `months` dentro da função `renderDashboard()`.
2. **Fuso Horário Dual (Moçambique +5h)**:
   * Horário Base no Brasil: Quintas-feiras às 19:00 BRT.
   * Horário Calculado em Moçambique: Sextas-feiras às 00:00 CAT.
   * Ao manipular datas de aulas síncronas, sempre calcule o deslocamento de +1 dia utilizando o objeto `Date` no JavaScript para exibir as datas correspondentes em Maputo.

---

## 📄 Estrutura de Arquivos do Workspace

```
curso_ext_neei/
├── index.html            # Ponto de entrada único (HTML, CSS em estilo interno, JS)
├── AGENTS.md             # Este manual de diretrizes para agentes de IA
├── handoff.md            # Documento de transição e próximos passos do projeto
├── assets/
│   └── images/
│       └── logos.png     # Imagem oficial dos logotipos (UERJ, NEEI, etc.)
└── docs/                 # Documentos locais de especificação do curso (Não vai para Deploy)
    ├── PROFESSORES COLABORADORES DO CURSO.pdf
    └── PROGRAMAÇÃO DO CURSO E CRONOGRAMA 15-04-26.pdf
```
