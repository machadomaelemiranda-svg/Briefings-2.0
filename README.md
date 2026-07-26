# Painel de Briefing — EasyChef

Ferramenta interna para gerar briefings de conteúdo (Instagram, TikTok, LinkedIn) por linha de produto, com benchmarking via IA e um modo dedicado a lançamentos recorrentes.

## Publicar no GitHub Pages (mesmo fluxo do formulário de auditoria de PDV)

1. Crie um repositório novo (ou reaproveite um existente) — pode ser **privado**, já que o painel usa dados internos.
2. Suba o arquivo `index.html` na raiz do repositório.
3. Crie uma pasta `assets/` e coloque nela o arquivo da logo real da EasyChef, nomeado exatamente:
   ```
   assets/logo-easychef.png
   ```
   Se esse arquivo não existir, o painel mostra automaticamente um selo laranja "EC" no lugar — não quebra nada, só fica sem a logo real.
4. Em **Settings → Pages**, selecione a branch `main` e a pasta `/root`, salve.
5. Em alguns minutos o GitHub gera uma URL do tipo `https://seu-usuario.github.io/nome-do-repo/`.

## Sobre a geração por IA fora do Claude.ai — leia antes de publicar

Dentro do Claude.ai, as chamadas de IA funcionam sem nenhuma configuração. Quando o painel é publicado como página própria (GitHub Pages), essa ponte automática não existe mais — o navegador precisa se autenticar diretamente com a API da Anthropic.

Por isso o painel tem um ícone de engrenagem (⚙) no canto do cabeçalho, com um campo para colar sua **própria chave de API da Anthropic** (gerada em [console.anthropic.com](https://console.anthropic.com)). Essa chave:
- fica salva **só no navegador** (localStorage), nunca é enviada para o repositório;
- é necessária apenas na versão publicada fora do Claude.ai — dentro do Claude.ai, deixe o campo vazio.

**Importante sobre segurança:** como a chamada é feita direto do navegador, qualquer pessoa com acesso ao painel publicado e às ferramentas de desenvolvedor do navegador consegue ver essa chave. Para um uso interno, com o repositório e o link do GitHub Pages não divulgados publicamente, isso é um risco aceitável na maioria dos casos — mas não é o ideal para algo 100% público. Se no futuro quiser eliminar esse risco por completo, o próximo passo é colocar um pequeno "proxy" (uma função serverless simples, ex. Cloudflare Worker ou Vercel Function) entre o painel e a API, para a chave nunca chegar ao navegador. Posso te ajudar a montar isso quando fizer sentido.

## O que já vem pronto
- Modo escuro com a paleta da marca (laranja `#FF6B00` + tons de marrom).
- Slot de logo real (`assets/logo-easychef.png`) com fallback automático.
- Armazenamento portátil: usa a memória do Claude.ai quando rodando lá dentro, e `localStorage` do navegador quando publicado standalone — os dados (linhas, lançamentos, períodos salvos, referências) persistem nos dois casos, mas **não são os mesmos dados** de um ambiente para o outro (não há sincronização entre Claude.ai e a versão publicada).
- Campo de "Referências de conteúdo": cole legendas/roteiros de exemplo e/ou envie imagens de textura, mockup ou print — isso entra automaticamente no prompt de geração (as imagens são enviadas como referência visual para a IA, até 3 por chamada).

## Estrutura de arquivos esperada
```
/index.html
/assets/logo-easychef.png   ← adicione o arquivo real da logo aqui
```
