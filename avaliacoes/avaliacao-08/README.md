# Avaliação-08

*Segue a Avaliação 08 da disciplina Banco de Dados*

* Estudante: Sure Rocha Bezerra 

* Professor: Ricardo Duarte Taveira

* Data de Entrega: 22/11/2023

*Criar o esquema (código SQL) que cria as tabelas e os relacionamentos do modelo anexo.*
  
*Os seguintes atributos devem seguir as seguintes regras:*
  
  *1) id -> é o nome de uma chave primária com auto incremento;*

  *2) atributo_id -> é o nome de uma chave estrangeira;*

     CREATE TABLE TB_IF (id INTEGER PRIMARY KEY AUTOINCREMENT, nome_if TEXT NOT NULL, ano INT NOT NULL, semestre INT NOT NULL);
     CREATE TABLE sqlite_sequence(name,seq);
     CREATE TABLE TB_Campus (nome TEXT NOT NULL, id INTEGER PRIMARY KEY AUTOINCREMENT, if_id, foreign key(if_id) references TB_IF(id));
     CREATE TABLE TB_Curso (nome TEXT NOT NULL, id INTEGER PRIMARY KEY AUTOINCREMENT, campus_id, foreign key(campus_id) references TB_Campus(id));
     CREATE TABLE TB_Laboratorio (id INTEGER PRIMARY KEY AUTOINCREMENT, nome TEXT NOT NULL, responsavel_email TEXT NOT NULL, curso_id, foreign key(curso_id) references TB_Curso(id));
     CREATE TABLE TB_Projeto(nome TEXT NOT NULL, inicio date, termino date, id INTEGER PRIMARY KEY AUTOINCREMENT, laboratorio_id, professor_id, foreign key (laboratorio_id) references TB_Laboratorio(id), foreign key (professor_id) references TB_Professor(id));
     CREATE TABLE TB_Professor(id INTEGER PRIMARY KEY AUTOINCREMENT, nome TEXT NOT NULL, email TEXT NOT NULL, celular TEXT NOT NULL);
     CREATE TABLE TB_Bolsista(id INTEGER PRIMARY KEY AUTOINCREMENT, nome TEXT NOT NULL, email TEXT NOT NULL, celular TEXT NOT NULL);
     CREATE TABLE TB_Frequencia (data date, frequencia_valida ENUM(1, 2), id INTEGER PRIMARY KEY AUTOINCREMENT, projeto_id, bolsista_id, professor_id, horario_planejado_id, foreign key(projeto_id) references TB_Projeto(id), foreign key(bolsista_id) references TB_Bolsista(id), foreign key(professor_id) references TB_Professor(id), foreign key(horario_planejado_id) references TB_Horario_Planejado(id));
     CREATE TABLE TB_Horario_Planejado(id INTEGER PRIMARY KEY AUTOINCREMENT, bolsista_id, ano INT NOT NULL, semestre INT NOT NULL, faixa_horaria_id, dia text check(dia in ('SEGUNDA', 'TERCA', 'QUARTA', 'QUINTA', 'SEXTA')), foreign key(bolsista_id) references TB_Bolsista(id), foreign key(faixa_horaria_id) references TB_FaixaHoraria(id));
     CREATE TABLE FaixaHoraria (turno text check( turno in ('MANHA', 'TARDE', 'NOITE')), faixa_horario text check( faixa_horario in ('A_PRIMEIRO_HORARIO', 'B_SEGUNDO_HORARIO', 'C_TERCEIRO_HORARIO', 'D_QUARTO_HORARIO', 'E_QUINTO_HORARIO')), id INTEGER PRIMARY KEY AUTOINCREMENT);
