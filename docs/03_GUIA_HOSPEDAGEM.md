# 🚀 Guia de Hospedagem Web (Mantendo o Código Privado)

Como o código contém fotos pessoais e textos íntimos, este guia explica as melhores opções para colocar o site no ar de forma rápida, gratuita e com **código 100% privado no GitHub**.

---

## Opção 1: Vercel *(Recomendada — 1 Minuto e Grátis)*

A Vercel conecta diretamente a repositórios **privados** do GitHub sem cobrar nada e gera um link seguro `https://...`:

1. Acesse [vercel.com](https://vercel.com) e faça login com sua conta do GitHub.
2. Clique em **"Add New..."** $\to$ **"Project"**.
3. Selecione o repositório privado `IsraelMdc/presente-gessy`.
4. Em **Framework Preset**, deixe como `Other`.
5. Em **Root Directory**, deixe `./`.
6. Clique em **Deploy**.
7. Pronto! Em 20 segundos você terá um link como:
   `https://presente-gessy.vercel.app` (você pode customizar o nome ou vincular domínio próprio).

---

## Opção 2: Cloudflare Pages *(100% Grátis com Tráfego Ilimitado)*

1. Acesse o painel da [Cloudflare](https://dash.cloudflare.com/) $\to$ **Workers & Pages**.
2. Clique em **Create application** $\to$ aba **Pages** $\to$ **Connect to Git**.
3. Autorize o acesso ao seu repositório privado `IsraelMdc/presente-gessy`.
4. Em *Build settings*, deixe os campos de build vazios e *Build output directory* como `/`.
5. Clique em **Save and Deploy**.
6. Seu site estará ativo em `https://presente-gessy.pages.dev`.

---

## Opção 3: GitHub Pages

> [!NOTE]
> No GitHub Free, o GitHub Pages só funciona diretamente em repositórios **Públicos**. Se a sua conta do GitHub for **GitHub Pro** ou **Student Developer Pack**, o GitHub Pages funciona normalmente em repositórios **Privados**!

Para ativar no GitHub:
1. No repositório, vá em **Settings** $\to$ **Pages**.
2. Em **Build and deployment** $\to$ **Source**, selecione **Deploy from a branch**.
3. Escolha a branch `main` e pasta `/ (root)`.
4. Salve e aguarde 1 minuto. O link será `https://israelmdc.github.io/presente-gessy/`.

