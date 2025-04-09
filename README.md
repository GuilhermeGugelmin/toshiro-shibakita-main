# Toshiro Shibakita - Exemplo Prático com PHP, Docker e NGINX

Este projeto demonstra um ambiente básico de microsserviços utilizando **PHP**, **Docker** e **NGINX como Load Balancer**, com conexão a um banco de dados **MySQL**. A estrutura foi baseada em uma live coding do instrutor Denilson Bonatti (DIO).

---

## 📁 Estrutura do Projeto

- `index.php`: Script PHP que:
  - Estabelece conexão com MySQL.
  - Gera dados aleatórios.
  - Insere dados na tabela `dados`.
- `banco.sql`: Script de criação da tabela `dados`.
- `nginx.conf`: Configuração do load balancer NGINX com três servidores upstream.
- `dockerfile`: Instruções básicas para containerizar a aplicação.
  
---

## 🧱 Requisitos

- Docker e Docker Compose instalados.
- MySQL acessível (no exemplo, IP: `54.234.153.24`, user: `root`, senha: `Senha123`, banco: `meubanco`).

---

## 🔧 Execução

1. **Banco de dados**: Certifique-se de que a instância do MySQL esteja ativa e com a tabela criada:

```sql
CREATE TABLE dados (
    AlunoID int,
    Nome varchar(50),
    Sobrenome varchar(50),
    Endereco varchar(150),
    Cidade varchar(50),
    Host varchar(50)
);
```

2. **Build do container PHP**:

```bash
docker build -t toshiro-php .
```

3. **Execução (exemplo simples)**:

```bash
docker run -d -p 80:80 toshiro-php
```

4. **NGINX como Load Balancer**:

- O `nginx.conf` define 3 servidores para balanceamento:

```nginx
upstream all {
    server 172.31.0.37:80;
    server 172.31.0.151:80;
    server 172.31.0.149:80;
}
```

- O servidor escuta na porta `4500` e repassa para os containers PHP.

---

## 🛠️ Observações Técnicas

- O PHP exibe a versão atual e insere registros randômicos no banco.
- `display_errors` está ativado para facilitar o debug.
- O host de origem do container é registrado na tabela (`gethostname()`).

---

## 🧑‍💻 Autor

Guilherme Gugelmin  
Este projeto é de uso educacional e demonstração técnica.