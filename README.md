# 🍽️ Refeição Solidária

## Tecnologia a serviço da solidariedade

O **Refeição Solidária** é um projeto social que busca utilizar a tecnologia para combater o desperdício de alimentos e facilitar a conexão entre pessoas, estabelecimentos e instituições que desejam realizar ou receber doações de alimentos e refeições.

## 🎯 Objetivo

Criar uma solução tecnológica simples e acessível para organizar e facilitar o processo de doação de alimentos que ainda estejam próprios para consumo.

## 💡 Problema

Todos os dias, alimentos que poderiam ser consumidos acabam sendo desperdiçados enquanto muitas pessoas enfrentam dificuldades para ter acesso a uma alimentação adequada.

O projeto busca utilizar a tecnologia para aproximar quem possui alimentos disponíveis de quem pode recebê-los e distribuí-los.

## 👥 Público beneficiado

O projeto poderá beneficiar:

- Pessoas em situação de vulnerabilidade social;
- Instituições assistenciais;
- Cozinhas comunitárias;
- Organizações sociais;
- Restaurantes;
- Mercados;
- Pequenos estabelecimentos;
- Voluntários interessados em ajudar.

## 🚀 Como funcionará

O sistema permitirá que um estabelecimento ou pessoa cadastre uma doação informando:

- Tipo de alimento;
- Quantidade;
- Data de disponibilidade;
- Prazo para retirada;
- Local;
- Observações.

Instituições ou responsáveis poderão consultar as doações disponíveis e realizar a solicitação.

### Fluxo básico

```text
DOADOR
   ↓
Cadastro da doação
   ↓
Sistema
   ↓
Instituição identifica a doação
   ↓
Reserva
   ↓
Retirada
   ↓
Doação concluída

refeicao-solidaria/
│
├── README.md
├── docs/
├── database/
├── src/
├── tests/
├── images/
└── .gitignore


### `database/schema.sql`

Já podemos deixar o banco preparado para a primeira versão:

```sql
CREATE DATABASE IF NOT EXISTS refeicao_solidaria;

USE refeicao_solidaria;

CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(150) NOT NULL,
    email VARCHAR(150) NOT NULL UNIQUE,
    telefone VARCHAR(20),
    tipo ENUM('DOADOR', 'INSTITUICAO', 'VOLUNTARIO') NOT NULL,
    data_cadastro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE doacoes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    usuario_id INT NOT NULL,
    alimento VARCHAR(150) NOT NULL,
    descricao TEXT,
    quantidade DECIMAL(10,2) NOT NULL,
    unidade VARCHAR(30) NOT NULL,
    data_disponibilidade DATE NOT NULL,
    data_validade DATE,
    endereco VARCHAR(255),
    status ENUM(
        'DISPONIVEL',
        'RESERVADA',
        'RETIRADA',
        'CONCLUIDA',
        'CANCELADA'
    ) DEFAULT 'DISPONIVEL',
    data_cadastro TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_doacao_usuario
        FOREIGN KEY (usuario_id)
        REFERENCES usuarios(id)
);
