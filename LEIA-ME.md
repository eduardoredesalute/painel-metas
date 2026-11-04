# Metas das Unidades

Painel semanal de OKRs das unidades. Os líderes lançam os resultados toda quarta (acumulado até terça), incluindo a nota e o total de avaliações do Google. As metas são definidas só pelo administrador.

## Estrutura

```
index.html              o painel
js/config.js            URL e chave pública do Supabase (você preenche)
js/backend.js           ligação do painel com o Supabase (login, leitura, gravação, tempo real)
supabase/01_estrutura.sql   cria tabelas, regras de acesso e usuários
supabase/02_dados.sql       dados atuais (metas e resultados de jan a nov/2026)
```

## Passo a passo

### 1. Supabase (banco gratuito)
1. Em https://supabase.com crie um projeto (plano Free).
2. Abra **SQL Editor > New query**, cole o conteúdo de `supabase/01_estrutura.sql` e clique em **Run**.
   - Antes de rodar, inclua os e-mails dos líderes no final do arquivo (item 6), com `admin = false`.
3. Nova query: cole `supabase/02_dados.sql` e clique em **Run**.
4. Em **Project Settings > API**, copie a **Project URL** e a chave **anon public** e cole em `js/config.js`.
   - A chave anon é pública por natureza; quem protege os dados são as regras de acesso do passo 2.

### 2. GitHub Pages
1. Envie todos os arquivos desta pasta para a raiz do repositório (mantendo as pastas `js` e `supabase`).
2. No repositório: **Settings > Pages > Build and deployment > Deploy from a branch**, branch `main`, pasta `/ (root)`.
3. O painel fica em `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`.

### 3. Login do administrador
Os líderes não fazem login: abrem o link e lançam os resultados.
Só o administrador entra (botão **Admin** no cabeçalho, link por e-mail) para alterar metas, dias úteis e feriados.

No Supabase, **Authentication > URL Configuration**:
- **Site URL**: o endereço do GitHub Pages do passo 2.
- **Redirect URLs**: o mesmo endereço.

### Incluir outro administrador
Supabase > **Table Editor > usuarios**: adicione uma linha com e-mail, nome e `admin` marcado.

## Regras de acesso
- Quem tem o link: vê o painel e lança resultados.
- Administrador logado: também altera metas, dias úteis e feriados.
- Atenção: como os líderes não fazem login, qualquer pessoa com o link consegue lançar resultados. Compartilhe o endereço só com os líderes.
