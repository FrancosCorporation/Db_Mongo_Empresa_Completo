# Segurança

Se você encontrar uma vulnerabilidade, informe o mantenedor em particular pela
opção **Report a vulnerability** na aba Security deste repositório. Inclua os
passos para reproduzir o problema e o impacto observado. Evite publicar detalhes
exploráveis antes de uma correção estar disponível.

Não envie senhas, tokens ou credenciais em issues públicas. Credenciais de
produção devem ser armazenadas nas variáveis de ambiente do provedor de deploy.
Senhas são limitadas a 72 bytes UTF-8 para respeitar o limite do bcrypt. O upload
de foto aceita apenas uma parte de arquivo até 5 MB e tem uma cota por endereço IP.
Tokens protegidos exigem `sub` igual ao `userId` e um `exp` inteiro válido, além
da assinatura, emissor e público. O limite global inclui `/health`; login,
cadastro e upload têm cotas adicionais.
