# Clínica Santa Lourdes — site

Site institucional de página única. O CSS, o JavaScript e as imagens ficam
todos dentro de `public/index.html`, então não há etapa de build.

## Estrutura

| Arquivo | Função |
| --- | --- |
| `public/index.html` | O site |
| `public/_headers` | Cabeçalhos de segurança (mesmo formato usado na Netlify) |
| `wrangler.jsonc` | Configuração da Cloudflare: publica só a pasta `public/` |
| `skills-lock.json` | Skills do Claude Code usadas no desenvolvimento (não vai para o ar) |

## Hospedagem: Cloudflare Workers (arquivos estáticos)

A Cloudflare publica o conteúdo de `public/` automaticamente a cada push na
branch `main`.

Configuração inicial (uma vez só) no painel da Cloudflare:

1. **Workers & Pages → Create application → Import a repository**.
2. Conecte o GitHub e escolha o repositório `Gabnagawo/clinica-santa-lourdes`.
3. Mantenha o nome do projeto `clinica-santa-lourdes`, que precisa ser igual
   ao `name` do `wrangler.jsonc`. Deixe o *build command* vazio e o
   *deploy command* como `npx wrangler deploy`.
4. Clique em **Deploy**. O site fica disponível em
   `https://clinica-santa-lourdes.<seu-subdominio>.workers.dev`.

### Domínio próprio

1. Adicione o domínio na Cloudflare (**Add a domain**, plano Free). Na revisão
   dos registros DNS, confira se os de e-mail (MX, SPF) vieram e apague os que
   apontam para a Netlify (A `75.2.60.5` ou CNAME `*.netlify.app`).
2. No registrador (ex.: Registro.br), troque os nameservers pelos dois que a
   Cloudflare indicar.
3. No projeto do site: **Settings → Domains & Routes → Add → Custom domain**,
   uma vez para o domínio e outra para o `www`.
4. Quando o site abrir pela Cloudflare, remova o domínio do site na Netlify.

## Testar localmente

```sh
npx wrangler dev
```

O site abre em http://localhost:8787, já com os cabeçalhos do `_headers`.
