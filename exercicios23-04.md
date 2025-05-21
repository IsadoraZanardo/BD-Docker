```sql

    SELECT [campos]
    FROM [tabelas]
    JOIN [tabelas] ON [relacionamento]
    WHERE [critérios] 
    GROUP BY [campos]
    HAVING [critérios]
    ORDER BY [campos]


## EXERCÍCIO 1 - Listar todos os clientes pessoa física com seus nomes e CPFs
    SELECT nome, cpf
    FROM pessoa_fisica
    ORDER BY nome;
    

## EXERCÍCIO 2 - Exibir o nome fantasia e CNPJ de todas as pessoas jurídicas cadastradas
    SELECT nome_fantasia, cnpj
    FROM pessoa_juridica
    ORDER BY nome_fantasia;
    

## EXERCÍCIO 3 - Listar todos os emails cadastrados no sistema
    SELECT email
    FROM email;


## EXERCÍCIO 4 - Exibir todos os endereços do tipo "Residencial", mostrando logradouro, número e cidade
    SELECT logradouro, numero, cidade
    FROM endereco
    WHERE tipo LIKE 'Residencial';
    

## EXERCÍCIO 5 - Listar todos os números de telefone do tipo "Movel"
	SELECT numero
    FROM telefone
    WHERE tipo LIKE 'Movel';


## EXERCÍCIO 6 - Listar o nome e CPF de todas as pessoas físicas ativas
	SELECT pf.nome, pf.cpf
    FROM pessoa_fisica pf
    JOIN cliente c ON pf.id = c.id
	WHERE c.ativo = TRUE;


## EXERCÍCIO 7 - Listar o nome fantasia e a quantidade de telefones cadastrados por pessoa jurídica
    SELECT pj.nome_fantasia, COUNT(t.numero) AS Quantidades
	FROM pessoa_juridica pj
	INNER JOIN cliente c ON pj.id = c.id
	LEFT JOIN telefone t ON t.cliente_id = c.id
	GROUP BY nome_fantasia;


## EXERCÍCIO 8 - Exibir o nome (PF ou PJ), o tipo de cliente e a cidade de todos os clientes que possuem endereço
    SELECT DISTINCT 
       COALESCE(pessoa_fisica.nome, pessoa_juridica.nome_fantasia) AS nome,
	   CASE
	      WHEN pessoa_fisica.id IS NOT NULL THEN 'Pessoa Física'
		  WHEN pessoa_juridica.id IS NOT NULL THEN 'Pessoa Jurídica'
	   END AS tipo_cliente,
	   endereco.cidade
    FROM cliente
    LEFT JOIN pessoa_fisica ON cliente.id = pessoa_fisica.id
    LEFT JOIN pessoa_juridica ON cliente.id = pessoa_juridica.id
    INNER JOIN endereco ON cliente.id = endereco.cliente_id;
    

## EXERCÍCIO 9 - Exibir o nome e email de todas as pessoas físicas que possuem mais de um email cadastrado
    SELECT nome, count(email) AS qtdEmail
    FROM pessoa_fisica 
    INNER JOIN cliente ON pessoa_fisica.id = cliente.id
    INNER JOIN email ON email.cliente_id = cliente.id
    GROUP BY nome
    HAVING count(email) > 1;


## EXERCÍCIO 10 - Listar todos os clientes (PF e PJ) que não possuem nenhum telefone cadastrado
    SELECT c.*
    FROM cliente c
    LEFT JOIN telefone t ON c.id = t.cliente_id
    WHERE t.cliente_id IS NULL;


## EXERCÍCIO 11 - Listar o nome (PF ou PJ) de todos os clientes que possuem pelo menos dois telefones e pelo menos um email
    SELECT c.id,
    COALESCE(pf.nome, pj.nome_fantasia) AS nome_cliente,
    COUNT(DISTINCT t.id) AS Qtstelefones,
    COUNT(DISTINCT e.id) AS Qtdsemails
    FROM cliente c
    LEFT JOIN pessoa_fisica pf ON pf.id = c.id
    LEFT JOIN pessoa_juridica pj ON pj.id = c.id
    LEFT JOIN telefone t ON t.cliente_id = c.id
    LEFT JOIN email e ON e.cliente_id = c.id
    GROUP BY c.id, nome_cliente
    HAVING COUNT(DISTINCT t.id) >= 2 AND COUNT(DISTINCT e.id) >= 1;


## EXERCÍCIO 12 - Listar os nomes e cidades dos clientes (PF ou PJ) que têm endereços tanto residenciais quanto comerciais



## EXERCÍCIO 13 - Listar todos os clientes (PF e PJ) com todos os seus contatos (email, telefone e endereço), mesmo que alguns desses dados estejam ausentes
   



## EXERCÍCIO 14 - Exibir a quantidade total de clientes ativos e inativos, separando por tipo (PF e PJ)
    


## EXERCÍCIO 15 - Para cada cliente, exibir:
## tipo (PF ou PJ),
## nome,
## total de emails,
## total de telefones,
## total de endereços. Ordenar pelo total de contatos (soma dos três)
 