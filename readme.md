# COOPERFILME - Sistema de Análise de Roteiros

Este projeto foi desenvolvido para a COOPERFILME, uma empresa que deseja disponibilizar um serviço para receber e analisar roteiros de filmes. O sistema permite que roteiros sejam submetidos para análise e acompanhem um fluxo de aprovação entre diferentes cargos: Analista, Revisor e Aprovador.

## Tecnologias Utilizadas
- **Backend:** Java 21 com Spring Boot
- **Frontend:** React com Vite
- **Banco de Dados:** MariaDB
- **Autenticação:** JWT (JSON Web Tokens)
- **Containerização:** Docker e Docker Compose

## Configuração do Ambiente

### Pré-requisitos
- Docker
- Docker Compose
- AWS CLI configurado com credenciais de acesso

### Configuração do AWS S3
1. **Crie um Bucket no S3**:
   - Acesse o [console do Amazon S3](https://s3.console.aws.amazon.com/s3/).
   - Crie um novo bucket e anote o nome, pois ele será necessário para configurar o sistema.

2. **Crie um Usuário IAM com Acesso Completo ao S3**:
   - Acesse o [console do IAM](https://console.aws.amazon.com/iam/).
   - Crie um novo usuário IAM com permissões de acesso completo ao S3 (política `AmazonS3FullAccess`).
   - Anote as chaves de acesso (Access Key e Secret Key) geradas para este usuário, pois serão usadas na configuração do sistema.

### Instalação
1. Clone o repositório:
   ```bash
   git clone https://github.com/RiumeCarlosA/CooperFilme
   ```
2. Navegue até a pasta do projeto:
   ```bash
   cd CooperFilme
   ```
3. Defina as variáveis de ambiente:
   - No arquivo `docker-compose.yml`, substitua `AWS_ACCESS_KEY`, `AWS_SECRET`, e `AWS_BUCKET_NAME` pelos valores apropriados:
     ```yaml
     - AWS_ACCESS_KEY=SEU_ACCESS_KEY
     - AWS_SECRET=SEU_SECRET_KEY
     - AWS_BUCKET_NAME=nome-do-seu-bucket
     ```

4. Execute o comando para iniciar os containers:
   ```bash
   docker-compose up --build
   ```

## Funcionalidades

### Fluxo de Status do Roteiro
1. **aguardando_analise**: Início do fluxo após envio.
2. **em_analise**: Analista avalia se o roteiro é viável.
3. **aguardando_revisao**: Revisor analisa o roteiro.
4. **em_revisao**: Revisor sugere correções.
5. **aguardando_aprovacao**: Aprovadores iniciam a votação.
6. **em_aprovacao**: Votos de aprovação ou recusa.
7. **aprovado**: Roteiro aprovado.
8. **recusado**: Roteiro recusado.

### Rotas do Sistema
- **/auth/login**: Login de usuário.
- **/scripts/upload-script**: Envio de Roteiro.
- **/scripts/status**: Consulta de Status do Roteiro.
- **/scripts/list**: Listagem de Roteiros.
- **/status/change-status**: Mudança de Status.
- **/status/vote**: Votação dos Aprovadores (incompleto).

## Usuários Padrão e Credenciais
- **Analista**: `analista@cooperfilme.com` / Senha: `analista123`
- **Revisor**: `revisor@cooperfilme.com` / Senha: `revisor123`
- **Aprovadores**:
  - `aprovador1@cooperfilme.com` / Senha: `aprovador123`
  - `aprovador2@cooperfilme.com` / Senha: `aprovador123`
  - `aprovador3@cooperfilme.com` / Senha: `aprovador123`

## Observações
1. O sistema é configurado para rodar via Docker, incluindo o backend, frontend e o banco de dados.
2. O fluxo de status segue uma ordem rígida. Qualquer tentativa de alterar o status fora do fluxo especificado resultará em um erro.
3. As configurações de acesso ao S3 são necessárias para o funcionamento completo do sistema. Certifique-se de configurar o bucket e o IAM com as permissões adequadas.
