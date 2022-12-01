-- 1 - Criar UML sobre qualquer tema de teu interesse. Deve conter no mínimo 7 tabelas.
 
-- 2 - Gerar conteúdo de dados .csv ou .json ou .txt referentes às sete tabelas do enunciado anterior. Os dados podem ser sintéticos e devem conter ao menos 15 linhas cada. 
 
-- 3 - Criar schema próprio para o presente trabalho.
 
-- 4 - Criar no MySQL as tabelas que receberão os dados, portanto, mostrar código de criação de cada uma das tabela. 
 
-- 5 - Especificar as chaves primárias e estrangeiras e escolher por um tipo de delete (cascade, set null ou no action). Justificar a escolha na documentação.

-- 6 - Trazer cinco consultas com join.
 
-- 7 - Trazer cinco consultas com order by.
 
-- 8 - Trazer cinco consultas com group by.
 
-- 9 - Trazer três consultas que combinem join e order by (sem repetir as anteriores).
 
-- 10 - Trazer sete consultas que contemplem funções matemáticas (e.g. AVG, SUM...)
 
-- 11 - Criar cinco visões.
 
-- 12 - Criar cinco savepoints.
 
-- 13 - Criar três usuários distintos sendo que um deles só poderá ter acesso às views, um só poderá inserir dados sem ver e o outro apenas poderá ver sem nenhuma outra ação.

create schema CINEMA;
use CINEMA;

-- 1 wizard importado :)
create table CINEMA(
id_cinema INT NOT NULL primary key,
id_nome INT NOT NULL,
id_sessao INT NOT NULL,
id_localizacao INT NOT NULL,
id_ingresso INT NOT NULL,
id_alimentacao INT NOT NULL,
id_filme INT NOT NULL,
id_preco INT NOT NULL
);

-- 2 wizard importado :)
select*from nome_cinema;
drop table nome_cinema;
create table nome_cinema(
id_nome INT NOT NULL auto_increment primary key,
nome varchar(20)
);

-- 3 wizard importado :)
create table sessao_cinema(
id_sessao INT NOT NULL auto_increment primary key,
lugares INT NOT NULL,
pessoas INT NOT NULL
);

-- 4 wizard importado :)
create table localizacao_cinema(
id_localizacao INT NOT NULL auto_increment primary key,
rua varchar(25),
bairro varchar(25),
cidade varchar(25)
);
-- 5 wizard importado :)
create table ingresso_cinema(
id_ingresso INT NOT NULL auto_increment primary key,
valor INT NOT NULL,
tipo varchar(10)
);
-- 6 wizard importado :)
create table alimentacao_cinema(
id_alimentacao INT NOT NULL auto_increment primary key,
preco INT NOT NULL,
quantidade INT NOT NULL
);

-- 7 wizard importado :)
create table filme_cinema(
id_filme INT NOT NULL auto_increment primary key,
nome_filme varchar(20),
genero varchar(20),
idade_minima int not null,
diretor varchar(20)    
);

-- 8 wizard importado :)
create table preco_cinema(
id_preco INT NOT NULL auto_increment primary key,
valor int not null,
numero_ingressos  int not null
);

-- 1
select*from CINEMA;
-- 2
select*from sessao_cinema;
-- 3
select*from nome_cinema;
-- 4
select*from localizacao_cinema;
-- 5
select*from ingresso_cinema;
-- 6
select*from alimentacao_cinema;
-- 7
select*from filme_cinema;
-- 8
select*from preco_cinema;

-- 5)exer
-- usei por conta da facilidade de entendimento, e pois pensei na seguinte ipotese, 
-- por algum motivo um cinema foi fechado então eu daria um delete nele na lista.

delete from nome_cinema
where id_nome = 15;

select*from nome_cinema;

-- 6)exer
-- 1
select sessao_cinema.id_sessao, filme_cinema.nome_filme
from sessao_cinema inner join filme_cinema on sessao_cinema.id_sessao = filme_cinema.id_filme
where lugares like 70;

-- 2

select ingresso_cinema.tipo, preco_cinema.valor
from ingresso_cinema inner join preco_cinema on ingresso_cinema.valor =  preco_cinema.valor
where tipo like 'estudante';

-- 3
select  filme_cinema.nome_filme, sessao_cinema.id_sessao
from sessao_cinema inner join filme_cinema on sessao_cinema.id_sessao = filme_cinema.id_filme
where lugares like 80;

-- 4

select preco_cinema.valor, ingresso_cinema.tipo
from ingresso_cinema inner join preco_cinema on ingresso_cinema.valor =  preco_cinema.valor
where ingresso_cinema.tipo like 'normal';

-- 5

select preco_cinema.valor, ingresso_cinema.tipo
from ingresso_cinema inner join preco_cinema on ingresso_cinema.valor =  preco_cinema.valor;

-- 7)exer
-- 1
select*from preco_cinema
order by valor;
-- 2
select*from ingresso_cinema
order by valor;
-- 3
select*from sessao_cinema
order by lugares;

-- 4
select*from alimentacao_cinema
order by quantidade;

-- 5
select*from filme_cinema
order by idade_minima;

-- 8) exer
-- 1
select idade_minima, count(idade_minima)
from filme_cinema
group by idade_minima;
-- 2
select genero, count(genero)
from filme_cinema
group by genero;
-- 3
select valor, count(valor)
from ingresso_cinema
group by valor;
-- 4
select numero_ingressos, count(numero_ingressos)
from preco_cinema
group by numero_ingressos;
-- 5
select pessoas, count(pessoas)
from sessao_cinema
group by pessoas;

-- 9 exer
-- 1
SELECT * FROM cinema; 
SELECT * FROM nome_cinema; 

select nome_cinema.nome, cinema.id_nome
from nome_cinema
inner join cinema on nome_cinema.id_nome = cinema.id_nome
where cinema.id_nome = 13;

-- 2
select*from preco_cinema;
select*from sessao_cinema;

select alimentacao_cinema.preco, cinema.id_preco, preco
from alimentacao_cinema
right join cinema on alimentacao_cinema.preco = cinema.id_preco
order by  alimentacao_cinema.preco;
-- 3

select alimentacao_cinema.id_alimentacao, cinema.id_alimentacao, quantidade
from alimentacao_cinema
left join cinema on  alimentacao_cinema.id_alimentacao = cinema.id_alimentacao
order by cinema.id_alimentacao;

SELECT * FROM ALIMENTACAO_CINEMA;
SELECT * FROM filme_cinema;

-- 10 EXER

-- 1
select SUM(preco) as sum
from alimentacao_cinema;
-- 2
select min(quantidade) as min
from alimentacao_cinema;
-- 3
select max(lugares) as max
from sessao_cinema;
-- 4
select avg(id_filme) as AVER
from filme_cinema;
-- 5
select sum(id_alimentacao) as sum
from alimentacao_cinema;
-- 6
select min(pessoas) as min
from sessao_cinema;
-- 7
select max(numero_ingressos) as max
from preco_cinema;

-- 11 EXER
-- 1
create view VIEW_FILME_CINEMA
as select*from filme_cinema;
-- 2
create view VIEW_INGRESSO_CINEMA
AS select*FROM INGRESSO_CINEMA;
-- 3
create view VIEW_LOCALIZACAO_CINEMA
AS select*FROM LOCALIZACAO_CINEMA;
-- 4
create view VIEW_PRECO_CINEMA
AS select*from PRECO_CINEMA;
-- 5


-- 12
-- 1
start transaction;
insert into FILME_CINEMA values(16,"bananas","comedia",10,"Mark_Zukenberg");
savepoint SAVE3;

-- 2
select*from nome_cinema;

insert into nome_cinema values(17,"RNALDO_filmes");
savepoint SAVE4;

-- 3
insert into localizacao_cinema values(18,"Lagostas","Vila_nova","sao_joao");
savepoint SAVE5;

-- 4
insert into sessao_cinema values(19,110,77);
savepoint SAVE6;

-- 5
insert into ingresso_cinema values(20,50,"vip");
savepoint SAVE7;

-- 13
create user ROGER12@LOCALHOST
identified by 'banana';

create user ALAN17@LOCALHOST
identified by 'cr7kiwi';

create user LOVERBAD@LOCALHOST
identified by 'garry';

grant all on filme_cinema.* to 'ROGER12'@'LOCALHOST';

grant insert on sessao_cinema.* to 'ALAN17'@'LOCALHOST';

grant select on preco_cinema.* to  'LOVERBAD'@'LOCALHOST';
