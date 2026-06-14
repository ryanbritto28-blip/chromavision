# ChromaVision — Versão PWA (Android + iOS)

## O que foi feito

Seu HTML foi transformado em um **PWA (Progressive Web App)**. Isso significa que,
quando hospedado em um endereço https://, qualquer pessoa pode "instalar" o
ChromaVision na tela inicial do celular — Android **e** iPhone — e ele se
comporta como um app normal: ícone próprio, tela cheia (sem barra do navegador)
e funcionamento offline.

Arquivos da pasta:
- `index.html` — seu app, com as tags de PWA adicionadas
- `manifest.json` — nome, ícone e cores do app
- `service-worker.js` — permite o app abrir mesmo sem internet
- `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` — ícones do app

## Por que não é um arquivo .apk?

- `.apk` é um formato **exclusivo do Android**. O iOS usa `.ipa`, que só pode
  ser gerado em um Mac, com Xcode e conta de desenvolvedor Apple.
- Gerar um app nativo "de fábrica" exige Android Studio/Gradle ou Xcode —
  ferramentas que não existem neste ambiente.
- O PWA resolve isso: **um único código, instalável nos dois sistemas**, sem
  precisar de loja de aplicativos.

## Passo 1 — Hospedar o site (necessário para o PWA funcionar)

Service workers só funcionam em `https://`. Opções gratuitas e rápidas:

- **GitHub Pages**: suba esta pasta para um repositório e ative o Pages.
- **Netlify / Vercel**: arraste a pasta no painel "Deploy" do site deles.
- **Firebase Hosting**: `firebase init hosting` → `firebase deploy`.

## Passo 2 — Instalar no Android

1. Abra o link no Chrome.
2. Toque no menu (⋮) → **"Instalar app"** (ou "Adicionar à tela inicial").
3. O ícone do ChromaVision aparece na tela inicial, abrindo em tela cheia.

## Passo 3 — Instalar no iPhone/iPad

1. Abra o link no Safari (precisa ser o Safari, não Chrome).
2. Toque no ícone de compartilhar (□ com seta para cima).
3. Escolha **"Adicionar à Tela de Início"**.
4. O ícone do ChromaVision aparece na tela inicial.

## (Opcional) Gerar um .apk real para a Play Store

Se quiser publicar na Google Play como um app de verdade, depois de hospedar
o PWA você pode usar o **Bubblewrap** (ferramenta oficial do Google para
empacotar PWAs como Trusted Web Activity):

```bash
npm install -g @bubblewrap/cli
bubblewrap init --manifest=https://seu-site.com/manifest.json
bubblewrap build
```

Isso gera um `.apk`/`.aab` real assinado, pronto para a Play Store. Esse passo
precisa ser feito na sua máquina (exige Java/Android SDK, que o Bubblewrap
instala automaticamente).

Para iOS, o caminho equivalente é empacotar o PWA com **Capacitor** e compilar
no Xcode — exige um Mac e conta de desenvolvedor Apple (US$ 99/ano) para
publicar na App Store.
