# 📖 Documentação Técnica — luiz.dev

> Guia completo de todas as seções do portfólio: o que cada parte faz, o que ela altera visualmente, como modificá-la corretamente e boas práticas para manutenção e expansão futuras.

---

## Sumário

1. [Estrutura Geral dos Arquivos](#1-estrutura-geral-dos-arquivos)
2. [O `<head>` — Metadados, SEO e Recursos](#2-o-head--metadados-seo-e-recursos)
3. [Navegação — `<header>` e `<nav>`](#3-navegação--header-e-nav)
4. [Hero — Apresentação Principal](#4-hero--apresentação-principal)
5. [Sobre Mim — `#sobre`](#5-sobre-mim--sobre)
6. [Formação Acadêmica — `#formacao`](#6-formação-acadêmica--formacao)
7. [Habilidades & Tecnologias — `#habilidades`](#7-habilidades--tecnologias--habilidades)
8. [Áreas de Conhecimento — `#areas`](#8-áreas-de-conhecimento--areas)
9. [Certificações (Carrossel) — `#certs`](#9-certificações-carrossel--certs)
10. [Contato — `#contato`](#10-contato--contato)
11. [Rodapé — `<footer>`](#11-rodapé--footer)
12. [Páginas Secundárias](#12-páginas-secundárias)
    - [projetos.html](#projectshtml)
    - [now.html](#nowhtml)
13. [O `style.css` — Como o CSS está organizado](#13-o-stylecss--como-o-css-está-organizado)
14. [O `script.js` — Como o JavaScript está organizado](#14-o-scriptjs--como-o-javascript-está-organizado)
15. [Boas Práticas Gerais](#15-boas-práticas-gerais)

---

## 1. Estrutura Geral dos Arquivos

```
portfolio/
│
├── index.html              ← Página principal
├── projetos.html           ← Galeria de projetos
├── now.html                ← Now Page (foco atual)
├── style.css               ← Todos os estilos do site
├── script.js               ← Todo o JavaScript do site
├── site.webmanifest        ← Configuração de PWA
│
└── assets/
    ├── img/
    │   └── idk.jpg         ← Foto de perfil
    └── icons/
        └── favicon_io/
            ├── favicon-32x32.png
            ├── android-chrome-192x192.png
            └── android-chrome-512x512.png
```

**Regra de ouro:** cada arquivo tem uma responsabilidade única. O HTML estrutura o conteúdo, o CSS cuida da aparência e o JS gerencia os comportamentos. Nunca misture estilos inline (`style="..."`) no HTML, a não ser para valores verdadeiramente dinâmicos — e mesmo assim, prefira classes CSS.

---

## 2. O `<head>` — Metadados, SEO e Recursos

O `<head>` não é visível na página, mas é lido por navegadores, buscadores (Google) e plataformas de compartilhamento (LinkedIn, WhatsApp). Está presente em **todos os três arquivos HTML**.

### O que cada tag faz

```html
<!-- Define o idioma da página para leitores de tela e buscadores -->
<html lang="pt-BR">

<!-- Codificação de caracteres — garante acentos e símbolos corretos -->
<meta charset="UTF-8" />

<!-- Faz o site ser responsivo em celulares -->
<meta name="viewport" content="width=device-width, initial-scale=1.0" />

<!-- Texto que aparece nos resultados de busca do Google (até ~160 caracteres) -->
<meta name="description" content="..." />

<!-- Palavras-chave para SEO (menos relevante hoje, mas boa prática) -->
<meta name="keywords" content="..." />

<!-- Autor do conteúdo -->
<meta name="author" content="Luiz" />
```

### Open Graph (compartilhamentos)

```html
<!-- Título que aparece no card de compartilhamento (WhatsApp, LinkedIn etc.) -->
<meta property="og:title" content="Luiz Neves | Dev Back-end & Cibersegurança" />

<!-- Subtítulo/descrição do card -->
<meta property="og:description" content="Transformando lógica em soluções seguras e eficientes." />

<!-- Tipo de conteúdo (website é o padrão para portfólios) -->
<meta property="og:type" content="website" />

<!-- URL canônica da página — evita duplicatas de indexação -->
<meta property="og:url" content="https://druthy1227.github.io/Portfolio/" />

<!-- Imagem do card (precisa ser URL absoluta, mín. 1200x630px) -->
<!-- ⚠️ Esta tag ainda está faltando — adicione quando tiver a imagem de capa -->
<meta property="og:image" content="https://druthy1227.github.io/Portfolio/assets/img/og-cover.jpg" />
```

### Twitter Card

```html
<!-- Define o estilo do card no Twitter/X -->
<meta name="twitter:card" content="summary" />
<!-- "summary_large_image" para exibir uma imagem grande — recomendado -->
```

### Favicon e Fontes

```html
<!-- Ícone da aba do navegador -->
<link rel="icon" href="assets/icons/favicon_io/favicon-32x32.png" type="image/png" />
<!-- ⚠️ O atributo type está incorreto no arquivo atual. O correto é type="image/png" -->

<!-- Pré-conecta ao servidor do Google Fonts antes de baixar — melhora performance -->
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />

<!-- Carrega as duas fontes usadas no site -->
<!-- Share Tech Mono → textos de código, labels, tags -->
<!-- Syne → títulos e texto de corpo -->
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet" />
```

### O que alterar aqui

| Situação | O que mudar |
|---|---|
| Mudar o título da aba | `<title>` e `og:title` |
| Mudar a descrição no Google | `<meta name="description">` |
| Adicionar imagem de compartilhamento | Adicionar tag `og:image` com URL absoluta |
| Trocar o favicon | Substituir os arquivos em `assets/icons/favicon_io/` |
| Corrigir o `type` do favicon | Trocar `type="favicon_io32x32.png"` por `type="image/png"` |

---

## 3. Navegação — `<header>` e `<nav>`

**Arquivo:** `index.html`, `projetos.html`, `now.html`
**CSS:** Seção `05. NAV / HEADER` do `style.css`
**JS:** Função hamburger menu no `script.js`

A navbar é **fixa no topo** (`position: fixed`) com `backdrop-filter: blur(14px)`, o que cria o efeito de vidro fosco sobre o conteúdo que passa por baixo ao rolar. O fundo semitransparente usa `rgba(22, 27, 34, 0.88)` — quase o `--bg-secondary`, mas com 12% de transparência.

### Estrutura HTML

```
<header>          ← Elemento semântico de cabeçalho (role="banner")
  <nav>           ← Elemento de navegação
    .nav-logo     ← Logo "luiz.dev" / botão de retorno em páginas secundárias
    .hamburger    ← Botão visível apenas em mobile (≤ 1023px)
    #navLinks     ← Lista de links (oculta em mobile até ser aberta)
  </nav>
</header>
```

### Comportamento por página

| Página | Logo | Links de `#âncora` | Links externos |
|---|---|---|---|
| `index.html` | `luiz.dev` → vai ao `#hero` | Apontam para seções da própria página | `projetos.html`, `now.html` |
| `projetos.html` | `← luiz.dev` → volta ao `index.html` | Apontam para `index.html#secao` | `now.html` |
| `now.html` | `← luiz.dev` → volta ao `index.html` | Apontam para `index.html#secao` | `projetos.html` |

A classe `.active` e o atributo `aria-current="page"` são aplicados manualmente no HTML das páginas secundárias, e automaticamente pelo JavaScript no `index.html` (via scroll).

### Como adicionar um novo link na nav

Acrescente um `<li>` na `<ul id="navLinks">` em **todos os três arquivos HTML**:

```html
<ul class="nav-links" id="navLinks" role="list">
  <!-- links existentes... -->
  <li><a href="nova-pagina.html">./nova-pagina</a></li>
</ul>
```

> **Boa prática:** mantenha o padrão `./nome` nos textos dos links — faz parte da identidade visual de terminal do site.

---

## 4. Hero — Apresentação Principal

**Arquivo:** `index.html` — seção `#hero`
**CSS:** Seção `06. HERO` do `style.css`

É a primeira coisa que o visitante vê. Ocupa 100% da altura da tela (`min-height: 100svh`). Em mobile, a foto fica acima do texto; em desktop (≥ 1024px), o texto fica à esquerda e a foto à direita, lado a lado.

### Componentes e o que cada um faz

**`.hero-tag`** — A faixa de texto acima do nome (`DISPONÍVEL PARA OPORTUNIDADES`). Comunica disponibilidade de forma imediata. Para alterar o status:

```html
<p class="hero-tag" aria-label="Status: disponível para oportunidades">
  DISPONÍVEL PARA OPORTUNIDADES  ← altere este texto
</p>
```

**`.hero-name`** — O `<h1>` da página. Por ser o único `<h1>`, tem peso máximo para SEO. A classe `.accent` no `iz` aplica a cor roxa com glow. Para trocar o nome, edite apenas o texto, mantendo a estrutura:

```html
<h1 class="hero-name" id="hero-name">
  Lu<span class="accent">iz</span>
</h1>
```

**`.hero-title`** — O subtítulo com o cursor piscante. O `<span class="cursor">` é puramente decorativo (`aria-hidden="true"`) e é animado pelo CSS (keyframe `blink`).

**`.hero-call`** — A frase de efeito dentro de um `<blockquote>`. A barra roxa à esquerda vem do CSS (`border-left: 3px solid var(--accent-color)`).

**`.hero-buttons`** — Container dos três botões de ação. Cada botão usa a classe `.hero-cta`. O segundo botão (`MEUS PROJETOS`) usa `.hero-now-btn` visualmente diferente (borda, sem preenchimento) para criar hierarquia visual — mas **atenção**: no arquivo atual os três usam `.hero-cta`. Se quiser diferenciar o estilo do segundo e terceiro botão, troque a classe pelo `.hero-now-btn` definido no CSS.

**`<figure class="hero-photo">`** — Container da foto. Os efeitos de moldura animada vêm dos pseudo-elementos `::before` e `::after` definidos no CSS. A foto em si é a `<img>` com `class="hero-photo-img"`.

### Como trocar a foto

```html
<figure class="hero-photo" aria-label="Foto de perfil">
  <img
    src="assets/img/sua-nova-foto.jpg"   ← caminho da imagem
    class="hero-photo-img"
    alt="Descrição visual detalhada da foto"  ← obrigatório para acessibilidade
  />
</figure>
```

---

## 5. Sobre Mim — `#sobre`

**Arquivo:** `index.html`
**CSS:** Seção `07. SEÇÃO: SOBRE MIM`
**Label de navegação:** `01 // ABOUT`

Layout em grid de duas colunas no desktop: texto biográfico à esquerda, quatro cards de destaque à direita. Em mobile, empilha verticalmente.

### Componentes

**`.sobre-text`** — Os parágrafos biográficos. Use `<strong>` para destacar termos técnicos importantes (nomes de tecnologias, instituições). Evite colocar mais de 3-4 parágrafos — o objetivo é ser escaneável, não exaustivo.

**`.sobre-stats` / `.stat-box`** — Quatro cards de destaque. Cada um tem um `stat-num` (o valor grande em roxo) e um `stat-label` (a descrição em monospace). São puramente informativos e podem ter qualquer texto curto.

```html
<article class="stat-box" role="listitem">
  <span class="stat-num" aria-label="Descrição acessível do valor">VALOR</span>
  <span class="stat-label">// descrição curta</span>
</article>
```

> **Boa prática:** sempre preencha o `aria-label` do `stat-num` com uma descrição por extenso. `aria-label="SI"` não diz nada para um leitor de tela — `aria-label="Curso: Sistemas de Informação"` diz tudo.

---

## 6. Formação Acadêmica — `#formacao`

**Arquivo:** `index.html`
**CSS:** Seção `07b. SEÇÃO: FORMAÇÃO ACADÊMICA`
**Label de navegação:** `02 // EDUCATION`

Lista vertical de cards de formação. Cada item tem ícone, título, período, instituição e descrição.

### Estrutura de um item

```html
<article class="formacao-item reveal" aria-labelledby="form4-title">
  <!-- Ícone decorativo — use um emoji temático -->
  <div class="formacao-icon" aria-hidden="true">🏛️</div>

  <div class="formacao-content">
    <div class="formacao-header">
      <!-- id deve ser único: form4-title, form5-title... -->
      <h3 class="formacao-title" id="form4-title">Nome do Curso ou Grau</h3>
      <!-- Período no formato "AAAA – AAAA" ou "AAAA – atual" -->
      <span class="formacao-period">2026 – atual</span>
    </div>
    <p class="formacao-institution">Nome da Instituição</p>
    <p class="formacao-desc">Breve descrição do foco ou disciplinas relevantes.</p>
  </div>
</article>
```

> **Boa prática:** mantenha a ordem cronológica reversa (mais recente primeiro). Isso é uma convenção de currículos que recrutadores esperam.

---

## 7. Habilidades & Tecnologias — `#habilidades`

**Arquivo:** `index.html`
**CSS:** Seção `08. SEÇÃO: HABILIDADES`
**Label de navegação:** `03 // SKILLS`

Grid de cards por categoria. Ao hover, uma linha roxa percorre a borda inferior do card (animação CSS pura via `::after` e transição de `width`).

### Dois tipos de card

**Card com tags** (`.skill-tags`) — Para listar tecnologias individuais como pílulas clicáveis:

```html
<article class="skill-card reveal" aria-labelledby="skill-novo">
  <div class="skill-card-icon" aria-hidden="true">☁️</div>
  <h3 class="skill-card-title" id="skill-novo">// CLOUD</h3>
  <ul class="skill-tags" aria-label="Tecnologias de cloud">
    <li class="skill-tag">AWS</li>
    <li class="skill-tag">Docker</li>
  </ul>
</article>
```

**Card com descrição** (`.skill-card-desc`) — Para habilidades que precisam de contexto, como o card de IA:

```html
<article class="skill-card reveal" aria-labelledby="skill-desc">
  <div class="skill-card-icon" aria-hidden="true">🤖</div>
  <h3 class="skill-card-title" id="skill-desc">// CATEGORIA</h3>
  <p class="skill-card-desc">Texto descritivo da habilidade e como ela é aplicada.</p>
</article>
```

### Bloco de Idiomas

O bloco `.languages-block` vive fora do grid, abaixo de todos os cards. Cada idioma é um `.language-item` com bandeira, nome e nível:

```html
<li class="language-item">
  <span class="language-flag" aria-hidden="true">🇩🇪</span>
  <div class="language-info">
    <span class="language-name">Alemão</span>
    <span class="language-level">Básico</span>
  </div>
</li>
```

---

## 8. Áreas de Conhecimento — `#areas`

**Arquivo:** `index.html`
**CSS:** Seção `09. SEÇÃO: ÁREAS DE CONHECIMENTO`
**Label de navegação:** `04 // KNOWLEDGE`

Grid de 3 colunas no desktop, 2 no tablet e 1 no mobile. Cada card tem um número decorativo enorme em roxo (quase transparente) no canto superior direito, ícone, título e descrição.

### Estrutura de um card

```html
<article class="area-card reveal" aria-labelledby="area-novo">
  <!-- Número decorativo (aria-hidden pois é puramente visual) -->
  <span class="area-card-num" aria-hidden="true">04</span>
  <div class="area-icon" aria-hidden="true">🔧</div>
  <!-- id deve ser único: area-novo, area-outro... -->
  <h3 class="area-title" id="area-novo">Nome da Área</h3>
  <p class="area-desc">
    Descrição concisa do que você sabe e como aplica nessa área.
  </p>
</article>
```

> **Boa prática:** mantenha os números dos cards sequenciais e em ordem. Eles não têm função técnica, mas ajudam o visitante a perceber a quantidade de áreas de forma visual.

---

## 9. Certificações (Carrossel) — `#certs`

**Arquivo:** `index.html`
**CSS:** Seção `10. SEÇÃO: CERTIFICAÇÕES` do `style.css`
**JS:** Função `initCertsCarousel()` no `script.js`
**Label de navegação:** `05 // CERTS`

Esta é a seção mais complexa tecnicamente. O carrossel usa `scroll-snap` para o encaixe nativo dos itens e JavaScript para o comportamento de loop infinito e os dots de navegação.

### Como funciona o loop infinito

O JavaScript clona o **último item real** e o coloca antes do primeiro, e clona o **primeiro item real** e o coloca depois do último. Assim, quando o usuário chega no final e avança, o carrossel "pula" imperceptivelmente de volta ao início real. Você nunca vê isso acontecer porque o pulo ocorre instantaneamente enquanto o item clonado ainda está visível.

```
DOM final após JS inicializar:
[clone do último] [item 1] [item 2] [item 3] [clone do primeiro]
```

### Como adicionar um certificado

Insira um novo `<article>` **dentro** do `<div id="certsCarousel">`, antes do fechamento do `</div>`. O `data-index` não precisa ser atualizado — ele é informativo apenas:

```html
<article class="carousel-cert-item" role="listitem" data-index="4">
  <div class="cert-bullet" aria-hidden="true"></div>
  <div class="cert-card-content">
    <h3 class="cert-name">Nome do Certificado</h3>
    <p class="cert-org">Instituição Emissora</p>
  </div>
</article>
```

O JavaScript detecta automaticamente a nova quantidade de itens e reconstrói os dots de navegação. Não é necessário alterar nada no `script.js`.

> **Boa prática:** mantenha os certificados em ordem cronológica reversa (mais recente primeiro), pois o carrossel começa no índice 0.

---

## 10. Contato — `#contato`

**Arquivo:** `index.html`
**CSS:** Seção `11. SEÇÃO: CONTATO`
**JS:** Função de feedback do formulário no `script.js`
**Label de navegação:** `06 // CONTACT`

Layout em duas colunas: links sociais à esquerda, formulário à direita.

### Links sociais

Cada link é um `<a class="social-link">`. Para adicionar uma nova rede:

```html
<a
  href="https://URL-DA-REDE.com/seu-usuario"
  class="social-link"
  target="_blank"
  rel="noopener noreferrer"
  aria-label="Nome da rede (abre em nova aba)"
>
  <!-- SVG do ícone da rede social -->
  <svg ...>...</svg>
  texto-visível/link-curto
</a>
```

### Formulário

O formulário tem **apenas feedback visual** — ele não envia e-mail por padrão. O JavaScript exibe "ENVIANDO..." por 1.2 segundos e depois "✓ ENVIADO!", mas nenhum dado chega a lugar nenhum.

Para tornar o formulário funcional, você tem duas opções sem precisar de back-end:

**Opção 1 — Formspree (gratuito):** substitua o `<form>` assim:
```html
<form action="https://formspree.io/f/SEU_ID" method="POST" ...>
```

**Opção 2 — EmailJS:** inicializa um SDK JavaScript e envia via API. Requer criar uma conta em [emailjs.com](https://emailjs.com).

> **Boa prática:** mesmo usando um serviço externo, mantenha o `novalidate` no `<form>` e a validação customizada em JS — a validação nativa do browser tem aparência inconsistente entre navegadores e não respeita o design do site.

---

## 11. Rodapé — `<footer>`

**Arquivo:** todos os três HTMLs
**CSS:** Seção `12. FOOTER`

Puramente decorativo. Exibe a linha de terminal `root@luiz:~$ portfolio --version 1.0.0`. Para atualizar a versão conforme o site evolui:

```html
<footer role="contentinfo">
  <p>
    <span aria-hidden="true">root@luiz:~$</span>
    portfolio --version 2.0.0   ← altere aqui
    &nbsp;|&nbsp;
    Feito com <span aria-label="amor">♥</span> &amp; ☕
  </p>
</footer>
```

> **Boa prática:** mantenha o rodapé idêntico nas três páginas. Se alterar em uma, altere nas outras. Uma forma de evitar desincronização no futuro seria usar um componente compartilhado — mas para um site estático simples, edição manual em três lugares é aceitável.

---

## 12. Páginas Secundárias

### projetos.html

Página dedicada aos projetos. Compartilha `style.css` e `script.js`. O grid muda de 1 coluna (mobile) para 2 (tablet) para 3 colunas (desktop).

**Anatomia de um card de projeto:**

```
.project-card
├── .project-card-header
│   ├── .project-number       ← "01", "02"...
│   └── .project-status       ← badge colorido de status
├── .project-card-body
│   ├── .project-title        ← nome do projeto
│   ├── .project-tags         ← lista de <li class="project-tag">
│   └── .project-desc         ← descrição com <strong> para destaques
└── .project-card-footer
    ├── .project-link--github ← botão cinza → roxo no hover
    └── .project-link--demo   ← botão roxo → branco no hover (opcional)
```

**Três variantes de status** com cores distintas:

| Classe | Cor | Uso |
|---|---|---|
| `.project-status--mvp` | Verde | Projeto finalizado / script concluído |
| `.project-status--dev` | Amarelo | Em desenvolvimento ativo |
| `.project-status--study` | Azul | Estudo prático / laboratório |

**Contador no hero:** os números `02 // projetos listados` e `06 // tecnologias usadas` são editados manualmente no HTML. Lembre-se de atualizá-los ao adicionar projetos.

---

### now.html

A Now Page funciona como um diário público de foco. Deve ser atualizada toda vez que seu foco de estudos ou projetos mudar.

**Cards de foco (`.now-card`)** — Cada área de atenção atual. A barra roxa à esquerda é um `::before` no CSS. Use emojis temáticos no `.now-card-icon` para diferenciação visual rápida.

**Radar de Leituras (`.books-grid`)** — Grid de livros. Em mobile exibe 1 coluna, tablet 2 colunas, desktop 3 colunas. Cada `.book-card` desliza levemente para a direita no hover (`transform: translateX(4px)`).

**Data no hero:** sempre atualize a tag de data quando revisar a página:

```html
<p class="hero-tag">ATUALIZADO EM MARÇO DE 2026</p>  ← atualize o mês/ano
<span class="stat-num accent" aria-label="Março">MAR</span>  ← e a abreviação
```

---

## 13. O `style.css` — Como o CSS está organizado

O arquivo tem **15 seções numeradas e comentadas**. Cada seção cobre uma responsabilidade:

```
01. Custom Properties (:root)  ← tema inteiro vive aqui
02. Reset & Base               ← normalização cross-browser
03. Utilitários                ← classes genéricas reutilizáveis
04. Scrollbar                  ← estilização da barra de rolagem
05. Nav / Header               ← navbar fixa
06. Hero                       ← seção de apresentação
07. Sobre                      ← texto + stat boxes
07b. Formação Acadêmica        ← cards de educação
08. Habilidades                ← skill cards + idiomas
09. Áreas de Conhecimento      ← knowledge cards
10. Certificações              ← carrossel
11. Contato                    ← social links + formulário
12. Footer                     ← rodapé
13. Animações                  ← keyframes (blink, frame-pulse)
14. Media Queries              ← breakpoints tablet (640px) e desktop (1024px)
15. Página de Projetos         ← estilos exclusivos de projetos.html
+ Now Page                     ← estilos de now.html (leituras, cards)
```

### O bloco `:root` — onde o tema vive

```css
:root {
  --bg-primary:    #0D1117;   /* fundo do body */
  --bg-secondary:  #161B22;   /* cards, nav */
  --text-primary:  #C9D1D9;   /* texto */
  --accent-color:  #9D4EDD;   /* roxo — cor de destaque */

  --accent-dim:    #7b3ab0;              /* hover de botões */
  --accent-glow:   rgba(157,78,221,.45); /* sombra neon */
  --accent-subtle: rgba(157,78,221,.08); /* fundo de badges */
  --border-color:  rgba(157,78,221,.18); /* bordas */

  --font-mono: 'Share Tech Mono', monospace; /* código, labels */
  --font-sans: 'Syne', sans-serif;           /* títulos, corpo */

  --glow:       0 0 14px var(--accent-glow);
  --transition: 0.3s ease;

  --section-padding: 3.5rem 1.5rem; /* mobile */
  --container-max:   1100px;
}
```

### Como o Mobile-First funciona na prática

O CSS base é escrito para mobile (telas menores). As media queries **adicionam** estilos para telas maiores, nunca sobrescrevem o mobile de forma destrutiva:

```css
/* Base: mobile — 1 coluna */
.skills-grid {
  grid-template-columns: 1fr;
}

/* Tablet (≥ 640px): 2 colunas */
@media (min-width: 640px) {
  .skills-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Desktop (≥ 1024px): 3 colunas */
@media (min-width: 1024px) {
  .skills-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

---

## 14. O `script.js` — Como o JavaScript está organizado

O arquivo é compartilhado pelas três páginas. Cada bloco tem uma guarda `if` que verifica se o elemento existe antes de tentar manipulá-lo — isso evita erros no console quando uma função tenta agir sobre algo que não existe naquela página.

### Bloco 1 — Hamburger Menu

Controla a abertura/fechamento da nav em mobile. Alterna a classe `.open` na `<ul>` e atualiza os atributos `aria-expanded` e `aria-label` do botão para acessibilidade.

```js
if (hamburger && navLinks) { ... }
```

### Bloco 2 — Scroll Reveal

Usa `IntersectionObserver` para adicionar a classe `.visible` em elementos `.reveal` quando eles entram no viewport. O `threshold: 0.08` significa que a animação dispara quando 8% do elemento está visível. O `setTimeout` escalonado (`i * 80ms`) cria o efeito de cascata quando múltiplos elementos entram ao mesmo tempo.

```js
const revealObserver = new IntersectionObserver((entries) => {
  entries.forEach((entry, i) => {
    if (entry.isIntersecting) {
      setTimeout(() => entry.target.classList.add('visible'), i * 80);
      revealObserver.unobserve(entry.target); // para de observar após animar
    }
  });
}, { threshold: 0.08 });
```

### Bloco 3 — Nav Active Link

Só funciona no `index.html`. Escuta o evento de scroll e compara a posição do `scrollY` com o `offsetTop` de cada seção para determinar qual está no viewport e aplica `.active` no link correspondente.

### Bloco 4 — Formulário

Intercepta o `submit` do formulário (`e.preventDefault()`), exibe estados de loading e sucesso com `setTimeout`, e limpa o formulário ao final.

### Bloco 5 — Carrossel (`initCertsCarousel`)

IIFE (função auto-executável) que inicializa o carrossel. Veja a explicação completa na [seção 9](#9-certificações-carrossel--certs).

A função `afterScroll` usa o evento nativo `scrollend` quando disponível (Chrome 114+, Firefox 109+), com fallback de `setTimeout(500ms)` para navegadores mais antigos:

```js
function afterScroll(callback) {
  if ('onscrollend' in window) {
    track.addEventListener('scrollend', callback, { once: true });
  } else {
    setTimeout(callback, 500);
  }
}
```

---

## 15. Boas Práticas Gerais

### Acessibilidade — regras que nunca devem ser quebradas

**Todo elemento interativo precisa de um label acessível.** Botões sem texto visível (como o hamburger e os botões de seta do carrossel) precisam obrigatoriamente de `aria-label`:

```html
<!-- ✅ Correto -->
<button aria-label="Abrir menu de navegação">...</button>

<!-- ❌ Errado — leitor de tela não sabe o que este botão faz -->
<button>...</button>
```

**Toda imagem precisa de `alt` descritivo.** Imagens decorativas usam `alt=""`. Imagens com conteúdo descrevem o que está na imagem:

```html
<!-- ✅ Foto de conteúdo -->
<img src="foto.jpg" alt="Foto de Luiz, de terno azul e óculos" />

<!-- ✅ Imagem decorativa -->
<img src="decoracao.svg" alt="" aria-hidden="true" />
```

**SVGs decorativos sempre com `aria-hidden="true"`** para que leitores de tela não tentem interpretar o código de path:

```html
<svg aria-hidden="true" focusable="false" ...>...</svg>
```

**IDs devem ser únicos na página.** Nunca repita um `id`. Se adicionar uma nova seção com `id="sobre-2"`, garanta que não há outro elemento com esse `id`.

---

### Semântica HTML — use a tag certa

| Situação | Tag correta | Não use |
|---|---|---|
| Título principal da página | `<h1>` (apenas um por página) | `<div class="titulo">` |
| Subtítulos de seção | `<h2>`, `<h3>`... em ordem | Pular de `<h1>` para `<h3>` |
| Grupo de itens relacionados | `<article>`, `<section>` | `<div>` genérico |
| Lista de links de navegação | `<nav>` + `<ul>` + `<li>` | `<div>` com links soltos |
| Citação | `<blockquote>` | `<p class="quote">` |
| Imagem com legenda | `<figure>` + `<figcaption>` | `<div>` + `<p>` |

---

### Adicionando novos elementos — checklist

Sempre que adicionar qualquer novo elemento ao HTML:

- [ ] A tag é semanticamente correta para o conteúdo?
- [ ] Imagens têm `alt`? SVGs têm `aria-hidden`?
- [ ] Elementos interativos têm `aria-label` se não tiverem texto visível?
- [ ] IDs são únicos na página?
- [ ] Adicionou a classe `.reveal` para a animação de entrada?
- [ ] Testou em mobile (≤ 640px) e desktop (≥ 1024px)?
- [ ] O CSS novo foi adicionado na seção correta do `style.css`?
- [ ] Usou variáveis CSS (`var(--accent-color)`) em vez de valores hardcoded?

---

### Convenções de nomenclatura do CSS

O projeto usa uma convenção similar ao BEM (Block, Element, Modifier):

```
.nome-do-bloco              → bloco pai
.nome-do-bloco-elemento     → elemento filho
.nome-do-bloco--modificador → variação do bloco
```

Exemplos reais do projeto:
```
.project-card               → bloco
.project-card-header        → elemento filho do card
.project-card-body          → elemento filho do card
.project-status             → bloco de status
.project-status--mvp        → modificador: variante mvp (verde)
.project-status--dev        → modificador: variante dev (amarelo)
.project-status--study      → modificador: variante study (azul)
```

Siga este padrão ao criar novos componentes CSS.

---

### Nunca use valores hardcoded de cor

```css
/* ❌ Errado — se mudar a paleta, precisa caçar este valor em todo o arquivo */
.meu-elemento {
  color: #9D4EDD;
  border-color: rgba(157, 78, 221, 0.18);
}

/* ✅ Correto — muda junto com o tema ao alterar o :root */
.meu-elemento {
  color: var(--accent-color);
  border-color: var(--border-color);
}
```

---

### Versionamento com Git — mensagens de commit

Para manter o histórico do projeto legível, use mensagens de commit descritivas:

```bash
# ✅ Boas mensagens
git commit -m "feat: adiciona projeto Whisper ao projetos.html"
git commit -m "fix: corrige type incorreto do favicon no head"
git commit -m "update: atualiza now page para março de 2026"
git commit -m "style: ajusta espaçamento do hero em mobile"

# ❌ Mensagens ruins
git commit -m "atualização"
git commit -m "mudanças"
git commit -m "fix"
```

O prefixo indica o tipo de mudança: `feat` (nova funcionalidade), `fix` (correção), `update` (atualização de conteúdo), `style` (ajuste visual), `docs` (documentação).
