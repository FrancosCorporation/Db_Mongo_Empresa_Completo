# Db Mongo Empresa Completo

API REST para cadastro e autenticação de usuários, comentários avaliados e fotos
de perfil. Usa Node.js 24, Express, MongoDB, JWT, bcryptjs e Cloudinary. A
documentação interativa fica em `/api-docs`.

## Requisitos

- Node.js 24 e npm 10 ou superior
- MongoDB local ou remoto
- Docker Compose, se preferir executar o conjunto local isolado

## Configuração local

```bash
cp .env.example .env
openssl rand -hex 32
```

Copie o valor gerado para `JWT_SECRET` no `.env` e configure `MONGO_URI`. Para
uploads, preencha também `CLOUDINARY_USER` (nome da conta Cloudinary),
`CLOUDINARY_KEY` e `CLOUDINARY_SECRET`. Esses três campos só são necessários
quando a rota de foto for usada.

```bash
npm ci
npm start
```

A API inicia em `http://127.0.0.1:3000`; o Swagger fica em
`http://127.0.0.1:3000/api-docs`. O processo local não inicia se o MongoDB não
estiver acessível.

## Executar com Docker Compose

```bash
cp .env.example .env
openssl rand -hex 32
# configure JWT_SECRET no .env

docker compose up --build -d
```

A API fica em `http://127.0.0.1:3100`. O Compose sobe um MongoDB local com
volume persistente, aguarda a verificação de saúde do banco e publica a API
somente na interface de loopback do computador. Use um serviço MongoDB gerenciado
para produção.

## Variáveis de ambiente

| Variável | Obrigatória | Uso |
|---|---|---|
| `JWT_SECRET` | Sim | Segredo aleatório com pelo menos 32 bytes; gere um valor diferente por ambiente. |
| `MONGO_URI` | Sim | URI `mongodb://` ou `mongodb+srv://`. |
| `CLOUDINARY_USER` | Para fotos | Nome da conta Cloudinary. |
| `CLOUDINARY_KEY` | Para fotos | Chave da API Cloudinary. |
| `CLOUDINARY_SECRET` | Para fotos | Segredo da API Cloudinary. |
| `CORS_ORIGINS` | Não | Origens web permitidas, separadas por vírgula; vazio bloqueia origens de navegador externas. |
| `PORT` | Não | Porta HTTP; padrão `3000`. |
| `HOST` | Não | Interface de rede; padrão `127.0.0.1` (o Compose usa `0.0.0.0` dentro do contêiner). |
| `TRUST_PROXY` | Não | Use `1` somente quando a API estiver atrás de um proxy confiável. |
| `JWT_ISSUER` / `JWT_AUDIENCE` | Não | Emissor e público dos tokens; têm valores padrão específicos deste serviço. |

Em deploy na Vercel, configure as variáveis no painel do projeto. Use uma URI
MongoDB acessível pelo deploy, `JWT_SECRET` próprio do ambiente e as credenciais
do Cloudinary se for habilitar uploads. Configure `CORS_ORIGINS` com as origens
reais do frontend. Não armazene segredos em `vercel.json` nem no repositório.

## Rotas

| Método | Rota | Acesso | Descrição |
|---|---|---|---|
| `GET` | `/` | Público | Confirma que a API respondeu. |
| `GET` | `/health` | Público | Verifica a conexão com o MongoDB. |
| `POST` | `/register` | Público | Cria uma conta com nome, e-mail e senha. |
| `POST` | `/login` | Público | Retorna um JWT válido por duas horas. |
| `POST` | `/upload_foto_profile` | JWT | Atualiza a foto do usuário autenticado; aceita JPEG, PNG ou WebP de até 5 MB. |
| `GET` | `/comentarios` | Público | Lista comentários recentes paginados (`page`, `limit`, máximo 50). |
| `POST` | `/comentarios` | JWT | Cria um comentário com avaliação de 1 a 5. |

Rotas protegidas recebem `Authorization: Bearer <token>`. A rota de upload usa a
identidade do token; não aceita e-mail enviado pelo cliente para escolher a conta.
O feed público retorna nome, comentário, avaliação e foto, sem expor e-mail ou
senha.

Senhas novas exigem pelo menos 8 caracteres e aceitam até 72 bytes UTF-8 para evitar o limite de truncamento do bcrypt. O upload aceita somente um arquivo (`fotoPerfil`), de até 5 MB, e tem limite de 10 tentativas por hora e endereço IP.
Há também um limite geral de 120 requisições por minuto e IP, incluindo `/health`, com limites adicionais para login e cadastro.

## Desenvolvimento e validações

- `npm run build` gera `swagger_output.json` localmente; o arquivo é ignorado pelo Git.
- `npm run dev` regenera a documentação e inicia o modo watch do Node.js.
- `npm audit --audit-level=high` verifica vulnerabilidades de dependências.
- A CI instala pelo lockfile, gera a documentação, verifica o audit e valida a sintaxe JavaScript.

O repositório ainda não contém testes automatizados. A suíte de testes não foi
executada durante esta atualização.

## Segurança

Consulte [SECURITY.md](SECURITY.md) para comunicar vulnerabilidades. Nunca
versione `.env`; `.env.example` contém somente nomes e exemplos sem credenciais.

## Licença

MIT — consulte [LICENSE](LICENSE).
