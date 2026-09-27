# Clínica Santa Lourdes — site

Site institucional de página única. O CSS e o JavaScript ficam dentro de
`public/index.html` e as imagens em `public/fotos/` e `public/logo/`, então
não há etapa de build.

## Estrutura

| Arquivo | Função |
| --- | --- |
| `public/index.html` | O site |
| `public/fotos/` | Fotos da equipe e da fachada |
| `public/logo/` | Logos e ícone da aba do navegador |
| `public/_headers` | Cabeçalhos de segurança (mesmo formato usado na Netlify) |
| `wrangler.jsonc` | Configuração da Cloudflare: publica só a pasta `public/` |
| `skills-lock.json` | Skills do Claude Code usadas no desenvolvimento (não vai para o ar) |

## Hospedagem: Cloudflare Pages

O site fica em https://clinicasantalourdes.pages.dev e é publicado com o
Wrangler, a ferramenta de linha de comando da Cloudflare (precisa do Node.js 22
ou mais novo). Na pasta do projeto:

```sh
npx wrangler login
npx wrangler pages deploy
```

O `login` só é necessário na primeira vez. Na primeira publicação, o Wrangler
pergunta se deve criar o projeto (escolha **Create a new project**) e qual é a
branch de produção (aperte Enter para aceitar a sugestão).

### Domínio próprio

1. Adicione o domínio na Cloudflare (**Add a domain**, plano Free). Na revisão
   dos registros DNS, confira se os de e-mail (MX, SPF) vieram e apague os que
   apontam para a Netlify (A `75.2.60.5` ou CNAME `*.netlify.app`).
2. No registrador (ex.: Registro.br), troque os nameservers pelos dois que a
   Cloudflare indicar.
3. No painel, em **Workers & Pages → clinicasantalourdes → Custom domains →
   Set up a custom domain**, adicione o domínio e depois o `www`.
4. Quando o site abrir pela Cloudflare, remova o domínio do site na Netlify.

## Testar localmente

```sh
npx wrangler pages dev
```

O site abre em http://localhost:8788, já com os cabeçalhos do `_headers`.
