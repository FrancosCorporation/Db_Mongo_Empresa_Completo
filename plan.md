# Plan — Db_Mongo_Empresa_Completo

## 1. Visão geral
API Express 5 + Mongoose 9 para usuários, comentários e fotos de perfil (Cloudinary) com MongoDB. Perfis de porta/loopback, Helmet, rate limit global incluindo `/health`, senhas limitadas a 72 bytes UTF-8, JWT com `sub==userId`/`exp` inteiro, multipart restrito (1 arquivo/sem campos, 10 uploads/h/IP).

## 2. Arquitetura e tecnologias
Express 5.3, Mongoose 9.11, bcryptjs 3, JWT, file-type 22 (validação real de conteúdo), cloudinary, dotenv, cors, express-rate-limit. CI moderna.

## 3. Funcionalidades existentes
- [x] CRUD usuários/comentários/foto de perfil — implementado.
- [x] Hardening 2026-10-11 (bcrypt 72B, JWT estrito, rate limit, multipart).
- [x] CI — **modernizada nesta sessão** (Ubuntu 24.04, Actions v7 SHA, Node 22/24).

## 4. Objetivos futuros
- OBJ-01 (P2, concluído nesta sessão): CI previsível.
- OBJ-02 (P3): TEST-01/02 — suíte HTTP com mongodb-memory-server (vedada nesta esteira).
- OBJ-03 (P3): proxy TLS/backup real documentado; checkout de pagamento só com confirmação externa.

## 5–9. Melhorias/Roadmap/Riscos/Ideias
- Risco externo: rotação de credenciais antigas segue operacional (dono).
- Sem mudanças funcionais nesta esteira — API em estado de manutenção.

*(Gerado em 2026-10-14 pelo agente orquestrador)*
