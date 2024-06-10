# Tema-NoSQL
{
  "homepage": "www.google.com",
  "language": "Português do Brasil",
  "location": "São Paulo",
  "theme": "Clássico",
  "showFavorites": true,
  "zoom": 100
}
////exercicio 2**
{
"funcionarios": [
{
"id": 1,
"nome": "João Grilo",
"endereco": "Rua Suassuna, 30, João Pessoa, PB",
"emails": [
"grilo@mail.com",
"joaoq@mk.com"
],
"cargo": "Contador",
"jornada": 40,
"salario": 3000.00
},
{
"id": 2,
"nome": "Ada Byron",
"endereco": "Rua Lovelace, 67, London",
"emails": [
"ada@mail.com",
"abyrondtech.com"
],
"cargo": "Developer",
"jornada": 20,
"salario": 15000.00
},
{
"id": 3,
"nome": "Gerundino",
"endereco": "Rua Substantivo, 78 Bairro Predicado, Mesoclise-AC",
"emails": [
"gerundino@gmail.com"
],
"cargo": "Linguista",
"jornada": 44,
"salario": 8000.00
},
{
"id": 4,
"nome": "Chicó",
"endereco": "Rua Eurico, 50, João Pessoa, PB, Apl 28 Bloco C",
"emails": [],
"cargo": "Developer",
"jornada": 20,
"salario": 15000.00
}
],
"localidades": [
{
"id": 1,
"cidade": "João Pessoa",
"estado": "PB",
"pais": "Brasil"
},
{
"id": 2,
"cidade": "London",
"estado": null,
"pais": "Reino Unido"
},
{
"id": 3,
"cidade": "Mesoclise",
"estado": "AC",
"pais": "Brasil"
}
]
}


exercicio 3***

CREATE TABLE Funcionarios (
id INTEGER PRIMARY KEY,
nome TEXT,
endereco TEXT,
email TEXT,
cargo TEXT,
jornada INTEGER,
salario REAL
);

CREATE TABLE Localidades (
id INTEGER PRIMARY KEY,
cidade TEXT,
estado TEXT,
pais TEXT
);

ALTER TABLE Funcionarios
ADD COLUMN localidade_id INTEGER;
ALTER TABLE Funcionarios
ADD FOREIGN KEY (localidade_id) REFERENCES Localidades(id);

Banco de dados de Jogos:
CREATE TABLE Fabricantes (
id INTEGER PRIMARY KEY,
nome TEXT,
pais TEXT,
site TEXT
);

CREATE TABLE Jogos (
id INTEGER PRIMARY KEY,
nome TEXT,
genero TEXT,
ano_lancamento INTEGER,
fabricante_id INTEGER,
FOREIGN KEY (fabricante_id) REFERENCES Fabricantes(id)
);

CREATE TABLE Personagens (
id INTEGER PRIMARY KEY,
nome TEXT,
raca TEXT,
classe TEXT,
jogo_id INTEGER,
FOREIGN KEY (jogo_id) REFERENCES Jogos(id)
);
CREATE VIEW vw_Funcionarios AS
SELECT
f.id,
f.nome,
f.endereco,
f.email,
f.cargo,
f.jornada,
f.salario,
l.cidade,
l.estado,
l.pais
FROM Funcionarios f
JOIN Localidades l ON f.localidade_id = l.id;

CREATE VIEW vw_Jogos AS
SELECT
j.id,
j.nome AS nome_jogo,
j.genero,
j.ano_lancamento,
f.nome AS fabricante,
f.pais AS pais_fabricante,
f.site AS site_fabricante,
p.nome AS nome_personagem,
p.raca,
p.classe
FROM Jogos j
JOIN Fabricantes f ON j.fabricante_id = f.id
LEFT JOIN Personagens p ON j.id = p.jogo_id;
INSERT INTO Localidades (cidade, estado, pais) VALUES
('São Paulo', 'São Paulo', 'Brasil'),
('Nova Iorque', 'Nova Iorque', 'Estados Unidos'),
('Londres', 'Inglaterra', 'Reino Unido');

INSERT INTO Funcionarios (nome, endereco, email, cargo, jornada, salario, localidade_id) VALUES
('João Silva', 'Rua A, 123', 'joao.silva@empresa.com', 'Gerente', 40, 8000.00, 1),
('Maria Oliveira', 'Avenida B, 456', 'maria.oliveira@empresa.com', 'Analista', 35, 5000.00, 1),
('Pedro Santos', 'Rua C, 789', 'pedro.santos@empresa.com', 'Desenvolvedor', 38, 6500.00, 2),
('Ana Souza', 'Avenida D, 321', 'ana.souza@empresa.com', 'Coordenador', 42, 7200.00, 3);

INSERT INTO Fabricantes (nome, pais, site) VALUES
('Nintendo', 'Japão', 'www.nintendo.com'),
('Sony', 'Japão', 'www.playstation.com'),
('Microsoft', 'Estados Unidos', 'www.xbox.com'),
('Ubisoft', 'França', 'www.ubisoft.com');

INSERT INTO Jogos (nome, genero, ano_lancamento, fabricante_id) VALUES
('The Legend of Zelda: Breath of the Wild', 'Ação-Aventura', 2017, 1),
('God of War', 'Ação', 2018, 2),
('Halo Infinite', 'Tiro em Primeira Pessoa', 2021, 3),
('Assassin''s Creed Valhalla', 'Ação-Aventura', 2020, 4);

INSERT INTO Personagens (nome, raca, classe, jogo_id) VALUES
('Link', 'Hyliano', 'Cavaleiro', 1),
('Kratos', 'Deus Grego', 'Guerreiro', 2),
('Master Chief', 'Humano', 'Soldado', 3),
('Eivor', 'Nórdico', 'Assassino', 4);
SELECT * FROM vw_Jogos;
