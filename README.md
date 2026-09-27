# Gestão do Negócio

Aplicação web para registar vendas em dólar (USD) e metical (MZN), com cálculo automático de:

- Custo por dólar em MZN
- Lucro por venda
- Lucro do dia
- Lucro do mês

Tem login (utilizador `jaimecossa`, password `12345`, alterável dentro da app) e tema claro/escuro.

## Ficheiros do projeto

```
├── index.html          → a aplicação (interface + lógica)
├── manifest.json        → configuração PWA (nome, cores, ícones)
├── service-worker.js    → permite a app funcionar offline
├── icons/                → ícones da app em vários tamanhos
└── README.md
```

Todos os dados (vendas, taxa de câmbio, password) ficam guardados **apenas no telemóvel/navegador do utilizador** (localStorage) — não há servidor nem base de dados.

---

## Passo 1 — Colocar no GitHub

1. Cria um repositório novo no GitHub (ex: `gestao-negocio`).
2. Envia estes ficheiros para o repositório:

```bash
cd gestao-negocio
git init
git add .
git commit -m "Primeira versão da app"
git branch -M main
git remote add origin https://github.com/TEU-USUARIO/gestao-negocio.git
git push -u origin main
```

3. Ativa o **GitHub Pages**: no repositório, vai a *Settings → Pages → Source*, escolhe a branch `main` e a pasta `/ (root)`. Guarda.
4. Ao fim de 1–2 minutos, a app fica disponível num link como:
   `https://TEU-USUARIO.github.io/gestao-negocio/`

Esse link é o que vais usar no passo seguinte para gerar o APK.

---

## Passo 2 — Gerar o APK (duas opções)

### Opção A — PWABuilder (mais simples, sem instalar nada)

1. Abre **https://www.pwabuilder.com**
2. Cola o link do GitHub Pages (passo 1.4) e clica em *Start*.
3. O PWABuilder vai ler o `manifest.json` e os ícones automaticamente.
4. Clica em **Package for Stores → Android**.
5. Descarrega o pacote gerado (vem com um `.apk` ou `.aab` pronto a instalar/publicar).

### Opção B — Capacitor (mais controlo, precisa de Android Studio)

1. Instala o Android Studio no computador.
2. No terminal, dentro da pasta do projeto:

```bash
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/android
npx cap init "Gestão do Negócio" "com.jaimecossa.gestaonegocio" --web-dir .
npx cap add android
npx cap copy
npx cap open android
```

3. O Android Studio abre o projeto — usa **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
4. O ficheiro `.apk` fica em `android/app/build/outputs/apk/debug/`.

---

## Notas

- Para atualizar a app depois de publicada, basta editar `index.html` e voltar a fazer `git push` — se usaste a Opção A (PWABuilder/TWA), a app no telemóvel atualiza-se sozinha porque carrega o conteúdo do link.
- A password de acesso (`jaimecossa` / `12345`) fica guardada no telemóvel depois do primeiro uso; pode ser alterada no botão "Alterar password" dentro da app.
- O ícone da app está em `icons/` — se quiseres um ícone diferente, basta substituir os ficheiros `icon-*.png` mantendo os mesmos nomes e tamanhos.
