# Melhorias implementadas — Db Mongo Empresa Completo

Atualização de outubro de 2026, baseada na auditoria deste projeto.

## Implementado

- Corrigido o IDOR no upload: a foto é vinculada à identidade assinada no JWT.
- JWT exige segredo forte, algoritmo HS256, emissor, público, expiração e cabeçalho Bearer válido.
- Login, cadastro e API têm limites de requisição; senhas são validadas e armazenadas com bcrypt.
- Upload em memória limitado a 5 MB, com validação de conteúdo por assinatura e tipos JPEG, PNG e WebP.
- Cloudinary é configurado sob demanda; credenciais ausentes não impedem outras rotas.
- Feed de comentários segue público, tem paginação limitada e não faz consulta por comentário.
- Avaliações, conteúdo e existência do usuário são validados antes de gravar.
- CORS usa lista permitida, Helmet adiciona cabeçalhos, e os corpos JSON e URL-encoded têm limite de 100 KB.
- Conexão MongoDB falha de forma explícita no início local e retorna indisponibilidade no health check.
- Configuração de ambiente centralizada; removidos segredos do estado atual do código e adicionados `.env.example` e `.gitignore` para arquivos sensíveis.
- Dependências diretas reduzidas ao runtime necessário; lockfile npm adicionado.
- Docker atualizado para Node 24, usuário sem privilégios, health check e Compose com banco persistente e porta local restrita.
- OpenAPI gerado localmente, sem manter o JSON gerado no Git; README, SECURITY.md e CI adicionados.

## Verificações desta atualização

- `npm run build`: aprovado.
- `npm audit --audit-level=high`: aprovado sem vulnerabilidades de alta severidade.
- Verificação sintática dos arquivos JavaScript: aprovada.
- `docker compose config --quiet`: aprovado.
- `docker build`: aprovado.
- A suíte de testes não foi executada; o projeto ainda não contém casos automatizados.

## Pendências externas

As credenciais que existiam em versões antigas devem ser rotacionadas nos serviços
MongoDB/Cloudinary correspondentes. Como elas permanecem no histórico Git, a
limpeza desse histórico exige coordenação com quem consome o repositório e deve
ser feita depois da rotação. Nenhuma credencial foi mantida em arquivos da versão
atual.
