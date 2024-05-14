#### Atividade complementar - PARTE 2 de prática de laboratório de banco de dados.

>[!Important]
> Nessa atividade, continuaremos com chave estrangeira. Iremos realizar consulta simples usando chave estrangeira conforme os exemplos abaixo.

  > Revisando os conceitos sobre chave estrangeira

1. Vimos o passo a passo sobre como criar um banco de dados conforme o código abaixo:

```sql
CREATE DATABASE escola;
```
2. Após criar o banco, selecionar o banco para ser usado e trabalhado no servidor

```sql
USE escola;
```
3. Criar as tabelas e inserir dados

```sql
CREATE TABLE alunos (
    id_aluno INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50)
);

INSERT INTO alunos (nome) VALUES
('João'),
('Maria');
```

4. Observe que iremos criar mais uma tabela para aplicarmos a ideia de chave estrangeira

```sql
   CREATE TABLE cursos (
    id_curso INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50)
);

INSERT INTO cursos (nome) VALUES
('Matemática'),
('História');

```

5. Agora que criamos nossas tabelas do nosso banco, iremos criar mais uma chamada matriculas porém, com nossas chaves estrangeiras. Observe:

```sql
CREATE TABLE matriculas (
    id_matricula INT AUTO_INCREMENT PRIMARY KEY,
    id_aluno INT,
    id_curso INT,
    FOREIGN KEY (id_aluno) REFERENCES alunos(id_aluno),
    FOREIGN KEY (id_curso) REFERENCES cursos(id_curso)
);

INSERT INTO matriculas (id_aluno, id_curso) VALUES
(1, 1),
(2, 2);
```

6. Vamos criar mais uma outra tabela chamada de "notas" também com chave estrngeira para correlacionar as tabelas do nosso banco:

```sql
CREATE TABLE notas (
    id_nota INT AUTO_INCREMENT PRIMARY KEY,
    id_matricula INT,
    nota FLOAT,
    FOREIGN KEY (id_matricula) REFERENCES matriculas(id_matricula)
);

INSERT INTO notas (id_matricula, nota) VALUES
(1, 8.5),
(2, 7.0);
```
`Observe que temos duas tabelas com chaves estrangeiras. Nessa última, criamos apenas uma chve estrangeira`

7. Agora iremos realizar uma consulta correlacionando todas as tabelas. Veja:

```sql
SELECT alunos.nome AS aluno, cursos.nome AS curso, notas.nota
FROM alunos
JOIN matriculas ON alunos.id_aluno = matriculas.id_aluno
JOIN cursos ON matriculas.id_curso = cursos.id_curso
JOIN notas ON matriculas.id_matricula = notas.id_matricula;
```
`JOIN ON -  É uma cláusula usada em consultas SQL para combinar linhas de duas ou mais tabelas com base em uma condição específica.`

  > Usamos JOIN para combinar as tabelas alunos, matriculas, cursos e notas. O ON especifica a condição para a junção entre essas tabelas.

Observe:

  > Aqui vamos juntar alunos com matrículas.
```sql
JOIN matriculas ON alunos.id_aluno = matriculas.id_aluno
```
  > Aqui vamos juntar matrículas com cursos
```sql
JOIN cursos ON matriculas.id_curso = cursos.id_curso
```

  > Aqui vamos juntar matrículas com notas.
```sql
JOIN notas ON matriculas.id_matricula = notas.id_matricula
```

8. Baseado no passo a passo acima, crie o seu banco com as sus tabelas e suas respectivas chaves estrangeiras e realize suas consultas. Compile o passo a psso do seu banco em um arquivo pdf único e envie para `cleciosousa@ufpi.edu.br`. Essa atividade é individual e contará pontuação Extra para as avaliações finais.

