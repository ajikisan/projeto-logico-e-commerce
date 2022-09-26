[ecommerce.zip](https://github.com/ajikisan/projeto-logico-e-commerce/files/9642169/ecommerce.zip)
### Desafio Construindo seu Primeiro Projeto Lógico de Banco de Dados E-COMMERCE
<p>Aluna: Mirian Ajiki Molicawa </p>
<p>Digital Innovation One </p>
<p>Instrutora:Juliana Mascarenhas </p>

<h2> Tecnologias </h2>
<br> - [x] Navegador Google Chrome
<br> - [x] ![SQL Online IDE](https://sqliteonline.com/) 
<br> - [x] ![BD E-Commerce](https://github.com/ajikisan/BD-E-Commerce/)


<h2> Descrição do Desafio </h2>
Replique a modelagem do projeto lógico de banco de dados para o cenário de e-commerce. Fique atento as definições de chave primária e estrangeira, assim como as constraints presentes no cenário modelado. Perceba que dentro desta modelagem haverá relacionamentos presentes no modelo EER. Sendo assim, consulte como proceder para estes casos. Além disso, aplique o mapeamento de modelos aos refinamentos propostos no módulo de modelagem conceitual.

Assim como demonstrado durante o desafio, realize a criação do Script SQL para criação do esquema do banco de dados. Posteriormente, realize a persistência de dados para realização de testes. Especifique ainda queries mais complexas dos que apresentadas durante a explicação do desafio. Sendo assim, crie queries SQL com as cláusulas abaixo:

<h2>Recuperações simples com SELECT Statement</h2>
Filtros com WHERE Statement
Crie expressões para gerar atributos derivados
Defina ordenações dos dados com ORDER BY
Condições de filtros aos grupos – HAVING Statement
Crie junções entre tabelas para fornecer uma perspectiva mais complexa dos dados
Diretrizes
Não há um mínimo de queries a serem realizadas;
Os tópicos supracitados devem estar presentes nas queries;
Elabore perguntas que podem ser respondidas pelas consultas;
As cláusulas podem estar presentes em mais de uma query;
O projeto deverá ser adicionado a um repositório do Github para futura avaliação do desafio de projeto. Adicione ao Readme a descrição do projeto lógico para fornecer o contexto sobre seu esquema lógico apresentado.

<h2>Objetivo:</h2>
“Refine o modelo apresentado acrescentando os seguintes pontos”
Cliente PJ e PF – Uma conta pode ser PJ ou PF, mas não pode ter as duas informações;
Pagamento – Pode ter cadastrado mais de uma forma de pagamento;
Entrega – Possui status e código de rastreio;
Algumas das perguntas que podes fazer para embasar as queries SQL:

Quantos pedidos foram feitos por cada cliente?
Algum vendedor também é fornecedor?
Relação de produtos fornecedores e estoques;
Relação de nomes dos fornecedores e nomes dos produtos;
Agora é a sua vez de ser o protagonista! Implemente o desafio sugerido pela expert e suba seu projeto para um repositório próprio, com isso, você aumentará ainda mais seu portfólio de projetos no GitHub!



<h2>Criação do banco de dados para o cenário de E-Commerce</h2>
Utilizou-se a ferramenta SQL Online IDE
create database ecommerce;
use ecommerce;

</p>
-- Criação tabela Cliente
create table cliente (
ID_Cliente integer auto_increment,
Nome_Cliente varchar(45),
CPF_CNPJ_Cliente varchar(18),
Endereco varchar(45),
Email varchar(45),
Telefone varchar(21),
Login_Usuario varchar(45),
Senha_Usuario varchar(8),
Status_Login boolean default false,
Forma_Pagamento varchar(48),
Data_Envio date,
Valor_Total_Compra float);
</p>

-- Criação da tabela Endereco
Create table endereco (
ID_Endereco integer auto_increment,
UF string(2),
Cidade varchar(100),
Bairro varchar(100),
Rua varchar(100),
Complemento varchar(100),
Numero varchar,
CEP varchar,
ID_Cliente integer);
</p>
-- Criação da tabela Pessoa Jurídica
create table pessoa_juridica (
CNPJ integer(14),
Razao_Social varchar(100),
Nome_Fantasia varchar(100),
Data_Cadastro_PJ date,
ID_Cliente integer);
</p>
-- Criação da tabela Pessoa Física
create table pessoa_fisica (
CPF integer(11),
Nome varchar(100),
Sobrenome varchar(100),
Data_Nascimento date,
ID_Cliente integer);
</p>
-- Criação tabela Produto
create table produto (
ID_Produto integer auto_increment,
Categoria varchar(45),
Sub_Categoria varchar(45),
Descricao varchar(45),
Valor float,
Quantidade_Estoque integer);
</p>
-- Criação da tabela Fornecedor
Create table fornecedor (
ID_Fornecedor integer auto_increment,
Razao_Social varchar(45));
</p>
-- Criação tabela Terceiro Vendedor
Create table terceiro_vendedor (
ID_Terceiro_Vendedor integer auto_increment,
Razao_Social varchar(45), 
Local varchar(45));
</p>
-- Criação tabela Estoque 
create table estoque (
 ID_Estoque integer auto_increment, 
 Local varchar(45));
</p>
-- Criação tabela Pedido
create table pedido (
ID_Pedido integer auto_increment,
Descricao_Pedido varchar(45),
Status_Pedido boolean default false,
Data_Solicitacao date,
Data_Cancelamento date,
Data_Entrega date,
Valor_Total float,
Codigo_Envio varchar(45),
Data_Envio date,
ID_Envio integer,
ID_Cliente integer);
</p>

-- Criação da tabela da Relação Produto com Pedido
create table produto_pedido (
Quantidade varchar(45),
ID_Produto integer,
ID_Pedido integer);
</p>
-- Criação da tabela Disponibilizando um Produto
create table disponibilizando_produto(
ID_Fornecedor integer, 
ID_Produto integer );
</p>
-- Criação da tabela Produto em Estoque
Create table produto_has_estoque (
ID_Produto integer,
ID_Estoque integer,
Quantidade integer);
</p>
-- Criação da tabela Produtos por Vendedor Terceirizado
Create table produtos_por_vendedor_terceiro (
ID_Terceiro_Vendedor integer auto_increment,
ID_Produto integer,
Quantidade integer);
</p>
-- Criação da tabela Forma de Pagamento
Create table forma_pagamento (
ID_Forma_Pagamento integer auto_increment,
Boleto_Bancario varchar(48),
Cartao_Credito varchar(48),
Cartao_Debito varchar(48),
Pix varchar(48),
Transferencia_Bancaria varchar(48),
Descricao varchar(45),
ID_Cliente integer);
</p>
-- Criação da tabela Forma_Envio
Create table forma_envio (
ID_Envio integer auto_increment,
Forma_Envio varchar(45),
Custo_Envio float,
Endereco varchar,
Codigo_Envio varchar(45));
</p>
======

<h2>Inserção de Dados</h2>
</p>
--Inserção de dados na tabela Cliente
Insert INTO cliente
(ID_Cliente,
Nome_Cliente,
CPF_CNPJ_Cliente,
Endereco,
Email,
Telefone,
Login_Usuario,
Senha_Usuario,
Status_Login,
Forma_Pagamento,
Data_Envio,
Valor_Total_Compra)
VALUES (1,
'Fulano', '29724237044',
'Endereco', 'fulano@email.com',
'216545555', 'fulano', 'senha',true,'Boleto',
'24012022', 150.00);

Insert INTO cliente
VALUES (2,
'Sicrano', '54917136008',
'Endereco 2', 'sicrano@email.com',
'546545575', 'sicrano', 'senha2',true,'Cartão de Crédito',
'28012021', 435.00);

Insert INTO cliente
VALUES (3,
'Beltrano', '88914588050',
'Endereco 2', 'beltrano@email.com',
'1165445585', 'beltrano', 'senha3',true,'Cartão de Débito',
'28012021', 55.00);

Insert INTO cliente
VALUES (4,
'Provocação LTDA', '08864245000179',
'Endereco 4', 'provocacao@noemail.com',
'1175545582', 'provocacao', 'senha4',true,'Pix',
'23032022', 60.00);

Insert INTO cliente
VALUES (5,
'Instigação LTDA', '49484385000107',
'Endereco 5', 'instigacao@noemail.com',
'1175545582', 'instigacao', 'senha5',true,'Transferência Bancária',
'14082022', 2000.00);

Insert INTO cliente
VALUES (6,
'Desafio1 LTDA', '18784114000135',
'Endereco 6', 'desafio1@noemail.com',
'1175545582', 'desafio1', 'senha6',true,'Transferência Bancária',
'22072021', 2000.00);
</p>

-- Inserção de dados na tabela Pessoa Jurídica
Insert into pessoa_juridica (
CNPJ,
Razao_Social,
Nome_Fantasia,
Data_Cadastro_PJ,
ID_Cliente)
Values (
18784114000135,
'Desafio1 LTDA',
'Desafio Ecommerce',
'25092022',4);

Insert into pessoa_juridica 
Values
 (
08864245000179,
'Provocação LTDA',
'Provocação Ecommerce',
'20042022',5);

Insert into pessoa_juridica 
Values
 (
49484385000107,
'Instigação LTDA',
'Instigação Ecommerce',
'12022022',6);
</p>

-- Inserção de dados na tabela de Pessoa Física
Insert into pessoa_fisica (
CPF,
Nome,
Sobrenome,
Data_Nascimento,
ID_Cliente)
Values
(29724237044,
'Fulano',
'D',
'01011954',1);

Insert into pessoa_fisica 
Values (54917136008,'Sicrano', 'C',
'22061967',2);


Insert into pessoa_fisica 
Values (88914588050,'Beltrano', 'X',
'15092001',3);
</p>
=============

-- Inserção na tabela de Endereço
Insert into endereco (
ID_Endereco,
UF,
Cidade,
Bairro,
Rua,
Complemento,
Numero,
CEP,
ID_Cliente) 
Values
(1,'MS','Sidrolândia','Paraíso','Rua das Flores','Bloco 1 Apto 101', 125, '79170-000',1);
Insert into endereco
Values (2,'SP','Bauru','Tatuapé','Rua Moema','Condomínio Swiss Park', 1545, '08090-000',2);
Insert into endereco
Values (3,'RJ','Rio de Janeiro','Jacarepaguá','Av Centro','Perto da Escola Cachambi', 46, '2050-000',3);
Insert into endereco
Values (4,'MG','Uberaba','Montes Claros','Av das Quatro estações','Fábrica de Sapatos', 25, '3950-000',4);
Insert into endereco
Values (5,'AM','Manaus','Santo Agostinho','Travessa 01','Fábrica de Sapatos', 25, '45820-000',5);
Insert into endereco
Values (6,'MA','São Luís','Bairro Ramal','Av João','UEMA', 00025, '65695-000',6);
</p>
-- Inserção na tabela de Produtos
Insert into produto (
ID_Produto,
Categoria,
Sub_Categoria,
Descricao,
Valor,
Quantidade_Estoque)
Values
(1,'Calçados','Corrida','Tênis para corrida a longas distâncias', 150.00, 100);

Insert into produto
Values 
(2,'Roupas','Yoga','Roupas elasticas', 145.00, 20);
  
Insert into produto
Values
(3,'Relógios','Acessórios', 'Relógio de bolso com MP3', 55.00, 10);

Insert into produto
Values
(4,'Bola','Esporte', 'Bola de Basquete', 60.00, 15);

Insert into produto
Values
(5,'Patins','Corridas', 'Patins para corridas', 2000.00, 5);

Insert into produto
Values
(6,'Faixa Elástica','Yogas', 'Faixa para esticar', 30, 6);
</p>
=========

-- Inserção de dados na tabela de Fornecedor
Insert into fornecedor (
ID_Fornecedor,
Razao_Social)
Values (1 , 'DesafioDIO LTDA');
</p>
=======


-- Inserção na tabela do Vendedor terceirizado
Insert into terceiro_vendedor (
ID_Terceiro_Vendedor,
Razao_Social, 
Local)
Values (1,'Color Bela Fashion','São Paulo');
</p>
=========

-- Inserção na tabela de Estoque

insert into estoque (
 ID_Estoque, 
 Local)
Values (1,'Deposito Loja 1');

insert into estoque 
Values (2,'Deposito Loja 2');

insert into estoque 
Values (3,'Deposito Loja 3');
</p>

========
-- Inserção na tabela da Relação Produto com Pedido
 insert into produto_pedido (
Quantidade,
ID_Produto,
ID_Pedido)
Values( 1, 1, 1); 
  
insert into produto_pedido 
Values(3, 2, 2);

insert into produto_pedido
Values( 1, 3, 3);

insert into produto_pedido
Values( 255, 3, 2);

insert into produto_pedido
Values( 1, 5, 4);

insert into produto_pedido
Values( 1, 5, 5);

insert into produto_pedido
Values( 1, 4, 6);
</p>
========
--Inserção na tabela Disponibilizando o produto
insert into disponibilizando_produto (
ID_Fornecedor, 
ID_Produto)
Values (1,2);

insert into disponibilizando_produto 
Values (1,1);

insert into disponibilizando_produto 
Values (1,3);

insert into disponibilizando_produto 
Values (1,4);

insert into disponibilizando_produto 
Values (1,5);

insert into disponibilizando_produto 
Values (1,6);
</p>
==========
-- Inserção na tabela Forma_Envio
Insert into forma_envio (
ID_Envio,
Forma_Envio,
Custo_Envio,
Endereco,
Codigo_Envio
)
Values (1,'Terrestre','10.00', 1,'Te01');

Insert into forma_envio
Values (2,'Marítimo','30.00', 2,'Ma02');

Insert into forma_envio
Values (3,'Aéreo','50.00', 3,'Ae03');
</p>
=====

-- Inserção na tabela Pedido
Insert into pedido (
ID_Pedido,
Descricao_Pedido,
Status_Pedido,
Data_Solicitacao,
Data_Cancelamento,
Data_Entrega,
Valor_Total,
Codigo_Envio,
Data_Envio,
ID_Cliente,
ID_Envio)
Values
(1, 'Tênis para corrida a longas distâncias',True,'01092022',NULL,'25092022',150.00,'Te01','05092022', 1, 1);

Insert into pedido Values
(2, 'Roupas elasticas',True,'06092022',NULL,'25092022',435.00,'Te01','10092022',2,1);

Insert into pedido Values
(3, 'Relógio de bolso com MP3',True,'03092022',NULL,'20092022',55.00,'Ma02','16092022',3,2);

Insert into pedido Values
(4, 'Bola de Basquete',True,'22092022',NULL,'23092022',60.00,'Ma02','24092022',4,2);

Insert into pedido Values
(5, 'Patins',True,'12092022',NULL,'13092022',2000.00,'Ae03','15092022',5,3);

Insert into pedido Values
(6, 'Patins',True,'12092022',NULL,'13092022',2000.00,'Ae03','15092022',6,3);
</p>
===============

-- Inserção na tabela Produto em Estoque
Insert into produto_has_estoque (
ID_Produto,
ID_Estoque, 
Quantidade)
Values (1,1,100);

Insert into produto_has_estoque 
Values (2,2,20);

Insert into produto_has_estoque 
Values (3,3,10);

Insert into produto_has_estoque 
Values (4,4,15);

Insert into produto_has_estoque 
Values (5,5,5);

Insert into produto_has_estoque 
Values (6,6,6);
</p>


=====
Inserção na tabela de Vendedor Terceirizado
Insert into produtos_por_vendedor_terceiro (
ID_Terceiro_Vendedor,
ID_Produto,
Quantidade)
Values (1, 255, 12);
</p>
=====

-- Inserção na tabela Forma de Pagamento
Insert into forma_pagamento (
ID_Forma_Pagamento,
Boleto_Bancario,
Cartao_Credito,
Cartao_Debito,
Pix,
Transferencia_Bancaria,
Descricao,
ID_Cliente)
Values (1,'Boleto da CEF', Null, Null, Null, Null,'Código de barras é aceito em Caixas Lotéricas',1);

Insert into forma_pagamento
Values (2,Null,'Cartão de Crédito', Null, Null, Null,'5347 0569 6937 1171 XXX 25/08/2022',2);

Insert into forma_pagamento
Values (3,Null, Null,'Cartão de Débito', Null, Null,'5196160992331525 XXX 14/05/2023',3);

Insert into forma_pagamento
Values (4,Null, Null, Null, 'Pix', Null,'Chave PIX',4);

Insert into forma_pagamento
Values (5,Null, Null, Null, Null,'Transferencia Bancária','Conta Corrente - Agencia - Banco',5);


Insert into forma_pagamento
Values (6,Null, Null, Null, Null,'Transferencia Bancária','Conta Corrente - Agencia - Banco',6);
</p>

--------------
<h2> Consultas SQL </h2>

--Seleção das empresas e seus logins
SELECT nome_fantasia, login_usuario FROM cliente c
 INNER JOIN pessoa_juridica pj on c.ID_Cliente = pj.ID_Cliente

--Seleção distinguindo as categorias de produtos comprados
SELECT DISTINCT nome_fantasia, login_usuario, categoria FROM cliente c
 INNER JOIN pessoa_juridica pj on c.ID_Cliente = pj.ID_Cliente
 Inner join produto pr on pr.id_produto = pj.ID_Cliente

-- Seleção com contagem dos clientes
Select count(*) nome_cliente from cliente c

-- Seleção com a soma do Custo de Envio
select  SUM(custo_envio), local from estoque e
inner join forma_envio fe on id_envio = e.ID_Estoque
inner join disponibilizando_produto dp on e.ID_Estoque = dp.ID_Produto

-- Seleção ordenada por cidades
SELECT cidade FROM endereco
order by cidade ASC

-- Seleção de dados dos clientes pela UF e somando os valores de compra
SELECT UF, nome_cliente, count(*)valor_total_compra FROM cliente
INNER JOIN endereco
WHERE UF like '%m%'

-- Seleção de locais que possuem estoque maior que 50
SELECT local, SUM(quantidade) AS 'Quantidade em Estoque'
FROM estoque e
inner JOIN produto_has_estoque phe on e.ID_Estoque = phe.ID_Estoque
GROUP BY local
HAVING SUM(Quantidade) > 50

-- Seleção dos vendedores terceirizados que atenderam pedidos
SELECT razao_social, nome_cliente from terceiro_vendedor tv
INNER join produto_pedido pp on tv.ID_Terceiro_Vendedor = pp.id_pedido
INNER join cliente c on pp.ID_Pedido = c.ID_Cliente

-- Seleção de pedido efetuado pelos clientes.
SELECT * from cliente c
INNER join pedido pe on c.id_cliente = pe.id_cliente
INNER Join produto_pedido pp on pp.id_pedido = pe.id_pedido
GROUP by nome_cliente;

=======
![Mi](https://user-images.githubusercontent.com/91148791/192173816-bd5fdf17-d21b-411a-8e59-ccb5ac305559.png)

