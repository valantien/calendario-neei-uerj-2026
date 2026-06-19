# Calendário Interativo — Curso de Extensão NEEI/UERJ 2026

Calendário visual e cronograma interativo do **Curso de Extensão NEEI/UERJ 2026**, sobre Neurodiversidade, Síndromes Raras e o contexto da Educação Básica.

🔗 **Acesse online:** https://valantien.github.io/calendario-neei-uerj-2026/

---

## Sobre o projeto

Uma página única que reúne, em um calendário interativo, todas as aulas do curso (maio a dezembro de 2026), organizadas por módulos. Permite navegar pelos meses, filtrar por módulo e abrir os detalhes de cada aula.

Principais recursos:

- 📅 **Calendário mensal** de maio a dezembro de 2026, gerado dinamicamente.
- 🧩 **Filtro por módulo**, cada um com sua cor própria.
- 🔍 **Busca** de aulas e conteúdos.
- 🌍 **Fuso horário duplo** — exibe o horário das aulas no Brasil (quinta, 19h BRT) e em Moçambique (sexta, 00h CAT).
- 📱 **Mobile-first**, com navegação por gestos (swipe) e tema claro/escuro automático.

## Tecnologia

Projeto **estático de arquivo único**, sem build e sem dependências:

- **HTML, CSS e JavaScript** puros, todos dentro de `index.html`.
- Design **Glassmorphism** com camadas CSS (`@layer`) e design tokens em `:root`.
- Fontes [IBM Plex Sans](https://fonts.google.com/specimen/IBM+Plex+Sans) (texto) e [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) (títulos), via Google Fonts.

Não há etapa de compilação: basta abrir o `index.html` no navegador.

## Como rodar localmente

Abra o arquivo `index.html` diretamente no navegador (duplo clique), ou sirva a pasta com um servidor local simples:

```bash
# Python 3
python3 -m http.server 8000
# depois acesse http://localhost:8000
```

## Estrutura

```
.
├── index.html       # Aplicação completa (HTML + CSS + JS)
├── assets/
│   └── images/      # Logotipos (UERJ, NEEI, etc.)
├── .nojekyll        # Serve o site sem processamento Jekyll no GitHub Pages
└── README.md
```

## Hospedagem

Publicado via **GitHub Pages** a partir da branch `main` (raiz do repositório).

---

Projeto desenvolvido para o **Núcleo de Estudos em Educação Inclusiva (NEEI) — UERJ**.
