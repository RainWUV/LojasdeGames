# Sistema de Gerenciamento de Vendas em Loja de Periféricos

![Funcionamento do Sistema](Videoapresentação.gif)

## Descrição

Este sistema foi desenvolvido para gerenciar vendas em uma loja de games, oferecendo uma interface intuitiva para clientes e vendedores. Os clientes podem navegar pelos produtos disponíveis, adicionar itens ao carrinho e finalizar compras. Os vendedores têm funcionalidades específicas para registrar vendas e gerenciar o estoque.

## Funcionalidades

- **Visualização de Produtos**: Clientes podem visualizar uma vitrine de produtos organizados por categoria (PlayStation, Xbox, Nintendo).
- **Carrinho de Compras**: Adição de múltiplos produtos ao carrinho com visualização e modificação do conteúdo antes da finalização.
- **Finalização de Compras**: Suporte para múltiplas formas de pagamento, incluindo Pix, Boleto e Cartão de Crédito.
- **Gestão de Vendas**: Vendedores podem registrar vendas e acompanhar o histórico.

## Tecnologias Utilizadas

- **Java**: Linguagem de programação principal.
- **Swing**: Biblioteca gráfica para interface de usuário.
- **SQLite**: Banco de dados relacional para armazenamento dos dados.

## Como Executar

### Pré-requisitos

- **Java JDK 8** ou superior instalado.

### Clonar o Repositório

```bash
https://github.com/RainWUV/LojasdeGames/tree/main

### Subir o Banco de Dados

O banco de dados SQLite está integrado ao sistema e será criado automaticamente.
Caso deseje modificar ou adicionar dados, você pode editar o arquivo script.sql.

# Compilar
javac TelaVitrineProdutos.java

# Executar
java TelaVitrineProdutos

## Estrutura do Banco de Dados
O banco de dados possui as seguintes tabelas:

Carrinho
Cliente
Estoque
FinalizandoCompra
ItemVenda
LojaDePerifericos
Pessoa
Produto
Venda
Vendedor

## Script SQL para criação das tabelas
O script database.sql está incluído no repositório. Ele pode ser executado para criar todas as tabelas necessárias:

-- Script para criar as tabelas do banco de dados

CREATE TABLE Cliente (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL
);

CREATE TABLE Produto (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    preco REAL NOT NULL,
    estoque INTEGER NOT NULL
);

CREATE TABLE Carrinho (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    cliente_id INTEGER,
    FOREIGN KEY(cliente_id) REFERENCES Cliente(id)
);

CREATE TABLE ItemVenda (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    venda_id INTEGER,
    produto_id INTEGER,
    quantidade INTEGER,
    preco REAL,
    FOREIGN KEY(venda_id) REFERENCES Venda(id),
    FOREIGN KEY(produto_id) REFERENCES Produto(id)
);

CREATE TABLE Estoque (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    produto_id INTEGER,
    quantidade INTEGER,
    FOREIGN KEY(produto_id) REFERENCES Produto(id)
);

CREATE TABLE Venda (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    cliente_id INTEGER,
    vendedor_id INTEGER,
    data DATE,
    total REAL,
    FOREIGN KEY(cliente_id) REFERENCES Cliente(id),
    FOREIGN KEY(vendedor_id) REFERENCES Vendedor(id)
);

CREATE TABLE Vendedor (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL
);

CREATE TABLE Pessoa (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    endereco TEXT,
    telefone TEXT
);

CREATE TABLE LojaDePerifericos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    endereco TEXT,
    telefone TEXT
);

CREATE TABLE FinalizandoCompra (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    venda_id INTEGER,
    forma_pagamento TEXT,
    FOREIGN KEY(venda_id) REFERENCES Venda(id)
);

## Diagrama de Classe
