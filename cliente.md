```sql

CREATE TABLE cliente (
    id SERIAL PRIMARY KEY,
    ativo BOOLEAN NOT NULL DEFAULT TRUE
);

CREATE TABLE pessoa_fisica (
    id INTEGER PRIMARY KEY REFERENCES cliente(id) ON DELETE CASCADE,
    nome VARCHAR(100) NOT NULL,
    cpf VARCHAR(14) UNIQUE NOT NULL,
    nascimento DATE NOT NULL
);

CREATE TABLE pessoa_juridica (
    id INTEGER PRIMARY KEY REFERENCES cliente(id) ON DELETE CASCADE,
    nome_fantasia VARCHAR(100) NOT NULL,
    razao_social VARCHAR(100) NOT NULL,
    cnpj VARCHAR(18) UNIQUE NOT NULL
);

CREATE TABLE endereco (
    id SERIAL PRIMARY KEY,
    cliente_id INTEGER REFERENCES cliente(id) ON DELETE CASCADE,
    logradouro VARCHAR(100) NOT NULL,
    numero VARCHAR(10),
    complemento VARCHAR(100),
    bairro VARCHAR(100),
    cidade VARCHAR(100) NOT NULL,
    estado VARCHAR(2) NOT NULL,
    cep VARCHAR(9) NOT NULL,
    tipo VARCHAR(12) NOT NULL CHECK (tipo IN ('Comercial', 'Residencial')) DEFAULT 'Residencial'
);

CREATE TABLE telefone (
    id SERIAL PRIMARY KEY,
    cliente_id INTEGER REFERENCES cliente(id) ON DELETE CASCADE,
    ddd VARCHAR(2) NOT NULL,
    numero VARCHAR(10) NOT NULL,
    tipo VARCHAR(12) NOT NULL CHECK (tipo IN ('Movel', 'Fixo', 'Recado')) DEFAULT 'Fixo'
);

CREATE TABLE email (
    id SERIAL PRIMARY KEY,
    cliente_id INTEGER REFERENCES cliente(id) ON DELETE CASCADE,
    email VARCHAR(200) NOT NULL
);

```


