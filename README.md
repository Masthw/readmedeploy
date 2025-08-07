# 🚀 Deploy de Aplicações com Docker

Este guia mostra como realizar deploy da sua aplicação utilizando o Docker.

---

## 📦 Adicionando o Projeto no Servidor:

### 1. Acessar o servidor

- O primeiro passo é acessar o servidor em que faremos o deploy da aplicação

```bash
ssh usuario@endereco-do-seu-servidor
```

### 2. Navegar até o diretório desejado

```bash
cd /caminho/para/destino
```

### 3. Clonar o repositório

```bash
#Exemplo clonando do Git Lab

git clone https://gitlab.com/usuario/repositorio.git
```

### 4. Acessar a pasta do repositório clonado

- Após clonar com sucesso podemos acessar o repositório

```bash
cd nome-do-repositorio
```

---

## 🛠️ Configurar Variáveis de Ambiente:

### 1. Verificar portas:

- Verificar a disponibilidade de portas para serem utilizadas no docker, contatar um admin do servidor para liberar portas necessárias da aplicação, Frontend e Backend (Banco de dados nem sempre é um requisito ser liberada)

### 2. Copiar .env:

- Copiar os arquivos .env.example para .env.
  Esse processo deve ser feito para os três ambientes do projeto:

```bash
cp .env.example .env

cp ./backend/.env.example ./backend/.env

cp ./frontend/.env.example ./frontend/.env
```

### 3. Editar os arquivos:

- Nessa etapa você deve inserir valores importantes como acessos de banco de dados e jwt_secrets no env do servidor.

- Você pode usar o nano ou qualquer editor de sua preferência

```bash
#Exemplo acessando com o nano

nano .env

nano ./backend/.env

nano ./frontend/.env
```

Deve ser atualizado valores necessários para que o docker-compose esteja correto (se necessário):

### ⚠️ Importante:

- Certifique-se de substituir valores placeholders por dados reais.
- Não utilize nomes de serviços internos do Docker, como docx_back ou docx_db, na BASE_URL (frontend) das chamadas de API. Use o domínio ou IP público real do servidor

---

## ⬆️ Subir os containers com Docker Compose:

### 1. Subir o Compose:

- Após configurar todas as variáveis de ambiente já estamos prontos para subir os containers, para isso utilize o comando

```bash
sudo docker compose up -d --build
```

- Onde, o parâmetro -d faz o docker rodar em segundo plano, ou seja, não bloqueia o terminal, e o –build garante que a imagem será reconstruída com base nas últimas alterações.

### 2. Validar a disponibilidade dos containers criados:

```bash
sudo docker ps -a
```

### ⚠️ Importante:

- Se as variáveis, mesmo após atualizadas não estão sendo refletidas no docker sera necessário dar um compose down, e depois buildar de novo.

```bash
sudo docker compose down <nome_do_servico>
```

---

## 🛂 Banco de Dados:

- De acordo com o tipo do banco do projeto será necessário fazer ou não uma migration inicial, isso dependerá do banco escolhido e de seu funcionamento (relacional ou não relacional).

### Recomendações da Equipe:

|                        |    MongoDb     | PostgresSql |   MySql    |   SqLite   |
| :--------------------- | :------------: | :---------: | :--------: | :--------: |
| `Tipo do Banco`        | Não Relacional | Relacional  | Relacional | Relacional |
| `Recomendado`          |       ✅       |     ✅      |     ❌     |     ❌     |
| `Precisa de migration` |       ❌       |     ✅      |     ✅     |     ✅     |

- Para realizar a migration em MySql ou PostgresSql é recomendado que seja feita a conexão do **computador do colaborador** para o banco no **servidor**, não recomendável fazer a migration direto com o código do servidor.

---

## 🔗 Validações finais:

- Após concluir o Deploy, é importante realizar os testes para garantir que a comunicação do sistema está sendo feita de maneira correta.
<h3 align="center">
 Frontend ↔️ Backend ↔️ Banco de dados
</h3>

- Ao validar a comunicação, você concluiu seu deploy com sucesso, parabéns!

---
