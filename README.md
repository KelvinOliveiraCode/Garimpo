# Garimpo — Curadoria de ofertas da Shopee, 100% client-side

![HTML5](https://img.shields.io/badge/HTML5-e34f26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572b6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-f7df1e?style=flat-square&logo=javascript&logoColor=black)
![GitHub Pages](https://img.shields.io/badge/Live-GitHub_Pages-121013?style=flat-square&logo=githubpages&logoColor=white)

**Garimpo** é um site de curadoria de ofertas da Shopee construído em HTML, CSS e JavaScript puro — zero frameworks, zero build step, zero backend. O `index.html` tem 841 linhas e faz todo o trabalho: carrega `produtos.json` (a fonte única de verdade, com 131 produtos curados), renderiza os cards, aplica filtros e busca, e gerencia a wishlist do usuário direto no `localStorage`. Criado em 2026, está no ar em [kelvinoliveiracode.github.io/Garimpo](https://kelvinoliveiracode.github.io/Garimpo/). É um exemplo de como vanilla JS bem escrito resolve um produto completo de vitrine sem nenhuma dependência.

---

## 🇧🇷 Português

### O que é

Um aggregator de ofertas onde cada produto listado passou por curadoria manual. O usuário filtra por categoria, busca por texto, favorita produtos e vai direto ao link da Shopee. Nada é processado no servidor: o navegador baixa o JSON e faz todo o resto.

### Catálogo

131 produtos curados em `produtos.json`, distribuídos por categoria:

| Categoria | Produtos |
|---|---|
| Casa | 46 |
| Natal | 27 |
| Moda | 20 |
| Beleza | 15 |
| Tech | 11 |
| Ferramentas | 5 |
| Pets | 4 |
| Fitness | 3 |

Preços a partir de R$ 17. Cada produto carrega os mesmos campos: `id`, `categoria`, `titulo`, `preco`, `loja`, `selo`, `rating`, `img` (WebP em `img/`), além do link curto `s.shopee.com.br` e do `productLink` completo.

Selos de destaque aplicados na curadoria: MAIS VENDIDO (41 produtos), VIRAL (27), 4.8 (27), NATAL (23) e NOVO (13).

### Funcionalidades

- **Chips de filtro por categoria** — navegação por categoria em um clique.
- **Busca com debounce de 160ms** — digitar não dispara render a cada tecla; o debounce segura o evento até o usuário parar.
- **Paginação** — o catálogo inteiro não despeja de uma vez na tela.
- **Wishlist em localStorage** — chave `garimpo_wishlist`, favoritos persistem entre sessões sem login.
- **Estados vazios** — busca sem resultado tem tratamento visual dedicado, não tela branca.
- **SEO e PWA basics** — `sitemap.xml`, `robots.txt`, `favicon` e `apple-touch-icon` configurados.

### Arquitetura

```
Garimpo/
├── index.html      # 841 linhas — markup + lógica de render/filtro/wishlist
├── produtos.json   # fonte única de verdade — 131 produtos curados
├── img/            # imagens dos produtos em WebP
├── sitemap.xml
├── robots.txt
└── favicon, apple-touch-icon, logos
```

O fluxo de dados é unidirecional e simples: `fetch("produtos.json")` → array em memória → funções de filtro/busca → render de cards. A wishlist lê e escreve em `localStorage` sob a chave `garimpo_wishlist`.

Decisões técnicas:

- **JSON como fonte única** — adicionar produto é editar um arquivo; não existe banco, não existe CMS.
- **Vanilla JS** — para uma vitrine com filtro e wishlist, framework seria peso morto; o resultado fala por si.
- **Debounce de 160ms** — equilíbrio entre responsividade percebida e custo de re-render durante a digitação.

### Como rodar

Por usar apenas arquivos estáticos, basta abrir `index.html` no navegador — ou servir a pasta com qualquer servidor estático (o `fetch` do JSON exige HTTP, não `file://`):

```bash
npx serve .
```

Deploy é GitHub Pages, já live em [kelvinoliveiracode.github.io/Garimpo](https://kelvinoliveiracode.github.io/Garimpo/).

---

## 🇺🇸 English

### What it is

An offer curation site where every listed product went through manual curation. The user filters by category, searches by text, favorites products, and goes straight to the Shopee link. Nothing is processed server-side: the browser downloads the JSON and does all the rest.

### Catalog

131 curated products in `produtos.json`, distributed by category:

| Category | Products |
|---|---|
| Home | 46 |
| Christmas | 27 |
| Fashion | 20 |
| Beauty | 15 |
| Tech | 11 |
| Tools | 5 |
| Pets | 4 |
| Fitness | 3 |

Prices starting at R$ 17. Every product carries the same fields: `id`, `categoria`, `titulo`, `preco`, `loja`, `selo`, `rating`, `img` (WebP in `img/`), plus the short `s.shopee.com.br` link and the full `productLink`.

Highlight badges applied during curation: MAIS VENDIDO / best-seller (41 products), VIRAL (27), 4.8 (27), NATAL / Christmas (23), and NOVO / new (13).

### Features

- **Category filter chips** — one-click category navigation.
- **Search with 160ms debounce** — typing does not trigger a render per keystroke; the debounce holds the event until the user pauses.
- **Pagination** — the full catalog does not dump onto the screen at once.
- **localStorage wishlist** — key `garimpo_wishlist`, favorites persist across sessions with no login.
- **Empty states** — a fruitless search gets dedicated visual treatment, not a blank screen.
- **SEO and PWA basics** — `sitemap.xml`, `robots.txt`, `favicon`, and `apple-touch-icon` configured.

### Architecture

```
Garimpo/
├── index.html      # 841 lines — markup + render/filter/wishlist logic
├── produtos.json   # single source of truth — 131 curated products
├── img/            # product images in WebP
├── sitemap.xml
├── robots.txt
└── favicon, apple-touch-icon, logos
```

The data flow is unidirectional and simple: `fetch("produtos.json")` → in-memory array → filter/search functions → card rendering. The wishlist reads and writes to `localStorage` under the key `garimpo_wishlist`.

Technical decisions:

- **JSON as single source of truth** — adding a product means editing one file; no database, no CMS.
- **Vanilla JS** — for a storefront with filters and a wishlist, a framework would be dead weight; the result speaks for itself.
- **160ms debounce** — balance between perceived responsiveness and re-render cost while typing.

### Running it

Since it is pure static files, opening `index.html` in a browser works — or serve the folder with any static server (the JSON `fetch` requires HTTP, not `file://`):

```bash
npx serve .
```

Deployment is GitHub Pages, already live at [kelvinoliveiracode.github.io/Garimpo](https://kelvinoliveiracode.github.io/Garimpo/).

---

## Autor

**Kelvin Oliveira**

- GitHub: [KelvinOliveiraCode](https://github.com/KelvinOliveiraCode)
- LinkedIn: [kelvin-oliveira-code](https://www.linkedin.com/in/kelvin-oliveira-code/)

## Licença

Distribuído sob a licença MIT. Consulte o arquivo de licença do repositório para detalhes.
