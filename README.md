# Prova de Ambiente de Software: Docker

- **Disciplina:** Ambiente de Software
- **Professor:** Rôney Reis
- **Curso:** ADS, IFCE Campus Umirim
- **Aluno:** Mikael Moreira Viana
 
---
 
## Estrutura do projeto
 
```
meu-sistema/
├── app.py
├── requirements.txt
├── Dockerfile
├── README.md
```
 
---
 
## Questão 3:
 
### a) Diferença entre imagem Docker e container Docker
 
Uma imagem Docker é um modelo somente leitura, formado por camadas, que contém tudo o que a aplicação precisa para rodar: sistema base, bibliotecas, dependências, código e as instruções de execução. Ela é estática e funciona como uma "receita" ou "molde".
 
Um container Docker é uma instância em execução de uma imagem. Ele é criado a partir da imagem, possui seu próprio processo e sistema de arquivos isolado e pode ser iniciado, parado e removido. A partir de uma única imagem é possível criar vários containers.
 
Analogia: a imagem é a classe e o container é o objeto; ou a imagem é a planta da casa e o container é a casa construída.
 
### b) Alteração no app.py que não apareceu
 
Isso aconteceu porque a imagem é imutável. Quando ela foi construída (docker build), o app.py foi copiado para dentro dela naquele momento (COPY . .). Alterar o arquivo no computador depois não modifica a imagem existente, e o container criado a partir dela continua com a versão antiga do código.
 
Para executar a versão atualizada, o aluno precisa:
 
1. Reconstruir a imagem com o código novo:
```bash
docker build -t meu-sistema:1.0 .
```
2. Parar e remover o container antigo:
```bash
docker stop sistema-web
docker rm sistema-web
```
3. Criar um novo container com a imagem atualizada:
```bash
docker run -d --name sistema-web -p 8080:5000 meu-sistema:1.0
```
 
---
 
## Questão 2:
 
### a) Construir a imagem meu-sistema com a tag 1.0
 
```bash
docker build -t meu-sistema:1.0 .
```
 
 
### b) Criar e executar o container sistema-web em segundo plano, na porta 8080 do computador
 
```bash
docker run -d --name sistema-web -p 8080:5000 meu-sistema:1.0
```
 

### c) Listar apenas os containers em execução
 
```bash
docker ps
```
 
 
### d) Visualizar os logs do container
 
```bash
docker logs sistema-web
```
 
 
### e) Parar o container
 
```bash
docker stop sistema-web
```
 
 
### f) Remover o container após parado
 
```bash
docker rm sistema-web
```
 
 
---

![alt text](<Captura de tela 2026-11-23 123231.png>)
![alt text](<Captura de tela 2026-11-23 123302.png>)
