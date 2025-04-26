``` sql

        CREATE TABLE MODELO (
            id SERIAL PRIMARY KEY,
            modelo VARCHAR (50) NOT NULL,
            potencia VARCHAR (4) NOT NULL,
            versao VARCHAR (50) NOT NULL,
            tipo VARCHAR (100) NOT NULL,
         );

        CREATE TABLE VEICULO (
            id SERIAL PRIMARY KEY,
            modelo_id REFERENCES modelo (id) ON DELETE CASCADE,
            ano INT (4) NOT NULL,
            cor VARCHAR (30) NOT NULL,
            chassi VARCHAR (25) UNIQUE NOT NULL,
        );

        CREATE TABLE ACESSORIOS (
            id SERIAL PRIMARY KEY,  
            nome VARCHAR (100) NOT NULL,
            tipo VARCHAR (100) NOT NULL,
            descrição VARCHAR (150) NOT NULL,
            preco DOUBLE (100) NOT NULL

        );
         
         CREATE TABLE COMPATIVEL (
            id_modelo INT REFERENCES modelo(id) ON DELETE CASCADE,
            id_acessorios INT REFERENCES acessorios(id) ON DELETE CASCADE,
            PRIMARY KEY (id_modelo, id_acessorios)
        );


        CREATE TABLE EQUIPA (
            id_veiculo INT REFERENCES veiculo(id) ON DELETE CASCADE,
            id_acessorios INT REFERENCES acessorios(id) ON DELETE CASCADE,
             PRIMARY KEY (id_veiculo, id_acessorios)
        );

```