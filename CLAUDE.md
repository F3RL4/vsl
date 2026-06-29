# CLAUDE.md — VSL (hospedagem)

Repo de **hospedagem das VSLs** via GitHub Pages. Parte do **Projeto do Milhão** (ver `D:\UmMilhao\CLAUDE.md` e memória em `repo-do-milhao/memory/`).

## O que é

Hospeda os vídeos de venda (VSL) em **HLS** servidos por GitHub Pages. Público em **https://f3rl4.github.io/vsl/** — embutido via iframe nos funis (ex.: `funil-gelatina`).

- **Público:** sim (GitHub Pages). Não colocar nada sensível aqui.
- URL de uso: `https://f3rl4.github.io/vsl/player.html?v=vsl_00X`

## Stack / estrutura

- `player.html` — player HTML + **hls.js**. Tem barra de progresso "fake" e overlay de "clique p/ ativar som". Carrega `${v}/index.m3u8`. A lista `const allowed = [...]` controla quais VSLs podem tocar.
- `vsl_00X/` — cada VSL em HLS: `index.m3u8` + segmentos `.ts`.
- `add-vsl.ps1` — ferramenta (PowerShell) pra adicionar/remover VSL: recebe um `.mp4`, roda **ffmpeg** pra gerar o HLS, cria `vsl_00X/` e atualiza a lista `allowed` no `player.html`.

## Como adicionar uma VSL

1. `.\add-vsl.ps1` → opção adicionar → arrasta o `.mp4`. (Exige ffmpeg: `winget install "FFmpeg (Essentials Build)"`.)
2. OU, se o vídeo já estiver em HLS pronto: criar `vsl_00X/` com `index.m3u8` + `.ts` e adicionar `'vsl_00X'` à lista `allowed` do `player.html` manualmente.
3. `git add . && git commit && git push origin main`.

## Regras

- **Commit + push imediato** após alterar. Commit `tipo: descrição em português`.
- Repo PÚBLICO — **nunca** commitar `.env`, tokens ou nada sensível.
- Não sobrescrever `vsl_00X` existente sem checar antes (cada slot é uma VSL real).
