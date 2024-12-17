# Banco-de-dados 
create table cliente (
    id_cliente number(3) primary key,
    nome char(65) not null,
    telefone char(11),
    data_nascimento date,
    observacao char(250)
);

insert into cliente values (1, 'Felipe', '11912341234',  TO_DATE('1999-07-15', 'YYYY-MM-DD'), 'cleinte frequente' );
insert into cliente values (2, 'Tiago', '11943211234',  TO_DATE('2000-06-07', 'YYYY-MM-DD'), 'cleinte frequente' );
insert into cliente values (3, 'Cesar', '11968432654',  TO_DATE('2001-12-23', 'YYYY-MM-DD'), 'alergia a gillette' );
insert into cliente values (4, 'Matheus', '11967589454',  TO_DATE('2004-09-23', 'YYYY-MM-DD'), 'fazer o pézinho' );
    

create table servico (
    id_servico number(3) primary key,
    descricao char(250),
    preco number(10, 2) not null
);

insert into servico values (1, 'cabelo', 50.00 );
insert into servico values (2, 'barba', 30.00 );
insert into servico values (3, 'cabelo e barba', 80.00 );

create table funcionario (
    id_funcionario number(3) primary key,
    nome char(65) not null,
    cargo char(30) not null,
    telefone char(11),
    data_contratacao date not null,
    salario number(10, 2) not null
);

insert into funcionario values(1, 'Carlos Santos', 'Cabeleireiro', '11999887766', TO_DATE('2021-05-10', 'YYYY-MM-DD'), 2000.00);
insert into funcionario values(2, 'Fernanda Souza', 'Recepcionista', '1198705635', TO_DATE('2020-03-23', 'YYYY-MM-DD'), 1500.00);
insert into funcionario values(3, 'Guilherme Augusto', 'Barbeiro', '11946224532', TO_DATE('2019-11-28', 'YYYY-MM-DD'), 2300.00);
insert into funcionario values(4, 'Matheus Silva', 'Gerente', '11985429734', TO_DATE('2017-04-21', 'YYYY-MM-DD'), 5000.00);

create table forma_pagamento (
    id_forma_pagamento number(3) primary key,
    descricao varchar2(50) not null
);

insert into forma_pagamento (id_forma_pagamento, descricao) VALUES (1, 'Dinheiro');
insert into forma_pagamento (id_forma_pagamento, descricao) VALUES (2, 'Cartão de Crédito');
insert into forma_pagamento (id_forma_pagamento, descricao) VALUES (3, 'Cartão de Débito');
insert into forma_pagamento (id_forma_pagamento, descricao) VALUES (4, 'Transferência');
insert into forma_pagamento (id_forma_pagamento, descricao) VALUES (5, 'pix');


create table agendamento (
    id_agendamento number(3) primary key,
    id_cliente number(3),
    id_servico number(3),
    data_hora timestamp not null,
    foreign key (id_cliente) references cliente(id_cliente),
    foreign key (id_servico) references servico(id_servico)
);

insert into agendamento values (1, 1, 1, to_timestamp('2024-10-20 14:00:00', 'YYYY-MM-DD HH24:MI:SS'));
insert into agendamento values (2, 3, 3, to_timestamp('2024-10-20 14:45:00', 'YYYY-MM-DD HH24:MI:SS'));
insert into agendamento values (3, 2, 2, to_timestamp('2024-10-20 15:40:00', 'YYYY-MM-DD HH24:MI:SS'));

create table pagamento (
    id_pagamento number(3) primary key,
    id_cliente number(3),
    id_agendamento number(3),
    id_servico number(3),
    id_forma_pagamento number(3),  
    foreign key (id_cliente) references cliente(id_cliente),
    foreign key (id_agendamento) references agendamento(id_agendamento),
    foreign key (id_forma_pagamento) references forma_pagamento(id_forma_pagamento),
    foreign key (id_servico) references servico(id_servico)
    
    
    );

insert into pagamento values (1, 1, 1, 2, 2);
insert into pagamento values (2, 2, 2, 1, 5);
insert into pagamento values (3, 3, 3, 3, 3);
