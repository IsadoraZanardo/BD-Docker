```sql

## EXERCÍCIO 1 - Inserir um novo cliente (ativo por padrão) e associá-lo a uma pessoa física chamada "Ana Lima", CPF 123.456.789-01, nascida em 1992-04-15
    DO $$
    DECLARE
	    novo_id INT;
    BEGIN
        INSERT INTO cliente (ativo) VALUES (true) RETURNING id INTO novo_id;

        INSERT INTO pessoa_fisica (id, nome, cpf, nascimento)
    VALUES (novo_id, 'Ana Lima', '123.456.789-01', '1992-04-15');
    END $$;


## EXERCÍCIO 2 - Insira um endereço residencial para o cliente da questão anterior: Rua Central, número 150, cidade Campinas, estado SP, CEP 13000-000
    DO $$
    DECLARE
	    novo_id INT;
    BEGIN
        INSERT INTO cliente (ativo) VALUES (true) RETURNING id INTO novo_id;

        INSERT INTO endereco (cliente_id, logradouro, numero, cidade, estado, cep, tipo)
    VALUES (novo_id, 'Rua Central', '150', 'Campinas', 'SP', '13000-000', 'Residencial');
    END $$;.


## EXERCÍCIO 3 - Insira um telefone do tipo "Móvel", DDD 19, número 99887766, para o mesmo cliente
Insira um telefone do tipo "Móvel", DDD 19, número 99887766, para o mesmo cliente.DO $$
    DECLARE
	    novo_id INT;
    BEGIN
        INSERT INTO cliente (ativo) VALUES (true) RETURNING id INTO novo_id;

        INSERT INTO telefone (cliente_id, ddd, numero, tipo)
    VALUES (novo_id, '19', '99887766', 'Movel');
    END $$;


## EXERCÍCIO 4 - Remova o telefone do cliente com CPF 123.456.789-01
    UPDATE pessoa_fisica
    SET nome = 'Ana Maria Lima'
    WHERE cpf = '123.456.789-01';


## EXERCÍCIO 5 - Atualize o nome da pessoa física com CPF 123.456.789-01 para "Ana Maria Lima"
    DELETE FROM cliente
    WHERE id = (
        SELECT id FROM pessoa_fisica WHERE cpf = '123.456.789-01'
    );

## EXERCÍCIO 6 - Insira um cliente do tipo pessoa jurídica chamado "Tech Mais", razão social "Tech Mais Soluções LTDA", CNPJ 12.345.678/0001-90, utilizando INSERT INTO ... SELECT com CTE para capturar o ID

## EXERCÍCIO 7 - Insira um endereço comercial para o cliente da questão anterior: Av. das Indústrias, 500, cidade São Paulo, estado SP, CEP 01100-000

## EXERCÍCIO 8 - Adicione dois e-mails para esse cliente (mesmo ID): contato@techmais.com.br e suporte@techmais.com.br, usando subconsultas

## EXERCÍCIO 9 - Atualize o nome fantasia da empresa com CNPJ 12.345.678/0001-90 para "Tech Mais Soluções"

## EXERCÍCIO 10 - Remova o cliente com CNPJ 12.345.678/0001-90 e todos os dados relacionados

## EXERCÍCIO 11 - Crie um script que insira 3 novos clientes pessoa física, com dados completos (nome, CPF, nascimento, endereço, telefone e e-mail) utilizando apenas INSERT INTO ... SELECT com CTEs encadeadas

## EXERCÍCIO 12 - Atualize todos os clientes com nome iniciado por "João" (tabela pessoa_fisica), adicionando " - Cliente Premium" ao final do nome

## EXERCÍCIO 13 - Remova todos os clientes inativos (cliente.ativo = FALSE) e todos os seus dados associados

## EXERCÍCIO 14 - Mova todos os telefones do tipo "Recado" para o tipo "Fixo", apenas se o cliente tiver mais de um número cadastrado

## EXERCÍCIO 15 - Crie um backup temporário da tabela email em uma nova tabela chamada email_backup, inserindo os dados usando INSERT INTO email_backup SELECT .... Em seguida, apague todos os e-mails de clientes cujo nome contenha "Maria"

```
