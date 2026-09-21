# Db Mongo Empresa Completo

API REST em **Node.js/Express** com **MongoDB**: autenticação JWT, cadastro de
usuários, comentários e upload de fotos (Cloudinary), documentada com
**Swagger** e preparada para deploy na **Vercel**.

![Node.js](https://img.shields.io/badge/Node.js-18-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-black?style=flat-square&logo=jsonwebtokens)
![Swagger](https://img.shields.io/badge/Swagger-85EA2D?style=flat-square&logo=swagger&logoColor=black)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)
![Status](https://img.shields.io/badge/status-2023-legacy-lightgrey?style=flat-square)

## Sobre

Back-end criado em 2023 como base "completa" de estudo para uma aplicação web
com banco MongoDB: cobre o fluxo de registro/login, proteção de rotas por
middleware e operações de escrita com imagens (upload e armazenamento em
nuvem), tudo documentado automaticamente.

## Funcionalidades

Comprovadas pelo código:

- **Autenticação**: registro e login com hash de senha (bcryptjs) e emissão
  de **JWT** (`controllers/authController.js`); middleware de proteção
  (`controllers/authMiddleware.js`).
- **Usuários**: model `user` com `uuid` e papéis.
- **Comentários**: model `comentario` com rotas associadas.
- **Upload de fotos**: integração com **Cloudinary** e `multer`
  (`controllers/upload_fotos.js`).
- **Documentação Swagger** gerada por `swagger-autogen`
  (`swagger.js` → `swagger_output.json`) e servida em `/api-docs`.
- **Deploy**: `vercel.json` configurado para serverless.

## Como rodar

```bash
npm install
# crie o .env com:
# PORT=3001
# MONGO_URI=mongodb://...
# JWT_SECRET=...
# CLOUDINARY_URL=cloudinary://...
npm run generate-swagger   # regenera a documentação
npm start                  # nodemon app.js
```

A documentação interativa fica em `http://localhost:<PORT>/api-docs`.

## Estrutura do projeto

```
app.js                  # bootstrap do Express + Swagger
config/db.js            # conexão Mongo
controllers/            # auth, middleware e upload de fotos
models/                 # schemas mongoose (user, comentario)
routes/                 # rotas de autenticação
swagger.js / swagger_output.json
vercel.json             # deploy serverless
```

> O `package.json` lista dependências transitivas como diretas (gerado por
> engano em 2023); o instalador resolve normalmente, mas vale limpar com
> `npm prune`/regeneração quando o projeto voltar a ser usado.

## Licença

MIT — veja [LICENSE](LICENSE).
