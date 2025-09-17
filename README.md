# Ticket Counter Site (PT-BR)

Site estático com contador de ingressos + barra de progresso em tempo real, usando Firebase (Firestore + Auth).

## O que vem no pacote
- `index.html` — página pública (exibe vendidos, restantes, % e barra)
- `admin.html` — painel de admin (login + ajustar contador/meta)
- `firestore.rules` — regras de segurança do Firestore
- `README.md` — este guia

## Passo a passo (10–15 min)
1) **Criar projeto Firebase**
   - Acesse https://console.firebase.google.com → Adicionar Projeto (sem Google Analytics).
   - Em *Build → Firestore Database* → Criar banco (modo bloqueado).
   - Em *Build → Authentication* → Método de login → Habilite **Email/Senha** e crie um usuário admin (seu e-mail e uma senha forte).
   - Em *Project settings → Your apps → Web app* → **Register app** e copie o objeto de configuração (apiKey, authDomain, etc).

2) **Configurar os arquivos**
   - Abra `index.html` e `admin.html` e SUBSTITUA o objeto `firebaseConfig` pelos dados do seu projeto.
   - (Opcional) No `index.html`, ajuste `const GOAL = 500;` e `const EVENT_NAME = "Meu Evento"`.

3) **Publicar as Regras**
   - Em *Firestore → Rules*, copie o conteúdo de `firestore.rules` e publique.
   - As regras permitem **leitura pública** de `eventStats/*` e **escrita apenas autenticada**.

4) **Criar os documentos iniciais (uma vez)**
   - Abra `admin.html` localmente, faça login com seu e-mail/senha criados no Firebase.
   - Clique em **Salvar valores** (ex.: Vendidos 0, Meta 500). Isso criará/atualizará:
     - `eventStats/sales` com `{ sold, updatedAt }`
     - `eventStats/config` com `{ goal }`

5) **Hospedar**
   - Qualquer hospedagem estática serve (Firebase Hosting, Vercel, Netlify, GitHub Pages).
   - **Firebase Hosting (rápido):**
     ```bash
     npm i -g firebase-tools
     firebase login
     firebase init hosting   # selecione seu projeto, "dist" não, use a pasta atual
     firebase deploy
     ```
   - **Vercel/Netlify:** arraste e solte a pasta, ou conecte ao Git.

6) **Como atualizar o número vendido**
   - Use `admin.html` (em um local seguro) para somar +1, +5 ou definir manualmente o total.
   - A página pública `index.html` atualiza em tempo real.

## Dicas
- Para adicionar o contador ao seu site principal, incorpore `index.html` via `<iframe>` ou copie o HTML/CSS/JS.
- Se quiser várias categorias (lotes, pistas, camarotes), crie docs extras (ex.: `eventStats/sales_pista`, `eventStats/sales_vip`) e mais blocos na UI.
- Quer mostrar o total de **arrecadação**? Adicione um campo `price` e calcule em tempo real.

## Suporte
- Qualquer dúvida, edite `admin.html`/`index.html` e ajuste layout/textos conforme seu evento.
