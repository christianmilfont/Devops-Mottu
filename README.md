# Projeto DevOps - Implementação de Aplicação Java Spring com Docker, MySQL e Azure
## Grupo:
- Christian Milfont Rm555345
- Iago Victor Rm558450
## Descrição do Projeto

Este projeto tem como objetivo implementar uma aplicação Java Spring Boot com o banco de dados MySQL 8.0, utilizando Docker e Docker Compose para containerização e orquestração dos serviços. A aplicação será configurada para rodar na nuvem, usando o **Azure Container Instances (ACI)** para execução do container da aplicação e **Azure Container Registry (ACR)** para armazenar a imagem Docker da aplicação.

## Nossa aplicação no repositório https://github.com/christianmilfont/Java-Mottu está com todos os arquivos necessários para criação! Justamente como utilizamos o Repackage dentro do pom.xml, ele engloba nosso arquivo .sql que criamos dentro de resources da pasta de Java.

## Arquitetura da Solução
<img width="775" height="284" alt="image" src="https://github.com/user-attachments/assets/8ac7c722-d13d-4604-a48c-acf3e14e8f79" />

## Utilizando o formato C4 Architect para formular nossa aquitetura da aplicação

---

### Agora apresentando cada passo desde Context até Code

<img width="686" height="565" alt="image" src="https://github.com/user-attachments/assets/c49e6c9a-817a-4820-bfce-70a06411c0a0" />
   
---

<img width="615" height="496" alt="image" src="https://github.com/user-attachments/assets/8271e3ff-af96-4ed4-bb61-2115b0dbe8e1" />

---

### Lembrando que:

<img width="712" height="373" alt="image" src="https://github.com/user-attachments/assets/f7d66dfd-5999-43d5-8170-54f3f639e199" />

---

<img width="482" height="302" alt="image" src="https://github.com/user-attachments/assets/2fd4de71-b074-4d7a-ae2a-2764dd0c52ee" />

---

<img width="839" height="459" alt="image" src="https://github.com/user-attachments/assets/78868416-0111-4679-b73d-e4f08d126560" />

### A arquitetura da solução é composta por dois componentes principais:

1. **Aplicação Java Spring Boot**:
   - A aplicação Java Spring Boot será empacotada em um container Docker.
   - Ela se conecta a um banco de dados MySQL rodando em um container separado (no local ou na nuvem(AZURE ACR).

2. **Banco de Dados MySQL 8.0**:
   - O banco de dados MySQL 8.0 será executado no **Azure Container Instances (ACI)** 

A solução vai permitir rodar a aplicação na nuvem de forma escalável e de fácil manutenção.

## Tecnologias Utilizadas

- **Java 21** (JDK 21)
- **Spring Boot** (Framework Java para microserviços)
- **MySQL 8.0** (Banco de dados relacional)
- **Docker** (Containerização)
- **Docker Compose** (Orquestração de containers)
- **Flyway** (Migrations de banco de dados)
- **Azure Container Registry (ACR)** (Armazenamento das imagens Docker)
- **Azure Container Instances (ACI)** (Execução de containers na nuvem)

## Benefícios para o Negócio  Utilizando a aplicação na nuvem (Docker ou ACR + ACI)

### 1. **Escalabilidade**:
   - A aplicação pode ser facilmente escalada para atender a maiores volumes de tráfego. A utilização de ACI permite aumentar a capacidade de execução de containers conforme a demanda.

### 2. **Portabilidade**:
   - Com o uso de **Docker**, a aplicação pode ser executada em qualquer ambiente de maneira consistente, seja localmente ou em diferentes ambientes de nuvem (neste caso, **Azure**).

### 3. **Facilidade de Implementação e Manutenção**:
   - A implementação e manutenção são simplificadas, pois o uso de **Docker Compose** facilita a configuração e inicialização de múltiplos containers (aplicação e banco de dados).
   - O **Flyway** automatiza o gerenciamento de migrações de banco de dados.

### 4. **Integração com Azure**:
   - A solução pode ser facilmente integrada ao **Azure** para aproveitar sua infraestrutura escalável e resiliente.
   - **ACR** permite armazenar e versionar as imagens Docker da aplicação.
   - **ACI** oferece uma maneira simples de rodar containers na nuvem sem a necessidade de gerenciar infraestrutura de servidores.

### 5. **Custo Efetivo**:
   - Usar ACI e ACR oferece uma solução econômica, pois você paga apenas pelo tempo de execução dos containers e pela quantidade de armazenamento utilizado no ACR, sem a sobrecarga de gerenciar máquinas virtuais ou servidores.

## Como Rodar a Aplicação (Docker ainda sem automatização do arquivo .sh)

### 1. **Pré-requisitos**

Antes de rodar a aplicação, é necessário ter o **Docker**, **Docker Compose** e **Azure CLI** instalados no seu sistema.

- **Instalar Docker**: [Docker - Instalação](https://docs.docker.com/get-docker/)
- **Instalar Docker Compose**: [Docker Compose - Instalação](https://docs.docker.com/compose/install/)
- **Instalar Azure CLI**: [Azure CLI - Instalação](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)

### Passo a Passo

1. **Clone o Repositório**:

   ```bash
       git clone https://github.com/christianmilfont/Java-Mottu.git
       cd Java-Mottu
   ```
   - Lembrando que é necessário criar o .jar da aplicação!
   ```
   mvn clean package
   ```
## Construir a Imagem da Aplicação:
    ```bash
       docker build -t myapp .
    ```
## Subir os Containers com Docker Compose:
    ```bash
        docker-compose up -d
    ```

## Testes:
Exemplo de POST (inserir um usuário):   
    ```bash
        curl -X POST http://localhost:8080/api/users \
          -H "Content-Type: application/json" \
          -d '{"name": "John", "email": "john@example.com", "role": "USER"}'
    ```
## Verificar os Containers em Execução e parar:
    ```bash
        docker ps
        docker-compose down
    ```
Explicação das mudanças:

URL de conexão:
````sql
Antes: jdbc:mysql://localhost:3306/mottu_challenge

Agora: jdbc:mysql://db:3306/mottu_challenge

````

A URL foi alterada para db:3306, onde db é o nome do serviço MySQL no docker-compose.yml. Isso permite que o Spring Boot se conecte ao MySQL dentro do container ao invés de tentar se conectar ao localhost.

Outras configurações:

O restante das configurações está OK para o seu cenário, especialmente a configuração do Flyway para migrações de banco de dados e as propriedades do JPA/Hibernate.

# Passo a Passo para Implementação no Azure

Agora que a aplicação está funcionando localmente, podemos enviá-la para o Azure Container Registry (ACR) e rodá-la no Azure Container Instances (ACI).

1. **Clone o Repositório**:

   ```bash
       git clone https://github.com/christianmilfont/Java-Mottu.git
       cd projeto-devops
   ```
   - Lembrando que é necessário criar o .jar da aplicação!
   ```
   mvn clean package
   ```
Após isso abra o Git Bash no local da pasta 

Execute:
```
bash deploy_full_aci.sh
```
## Resultado da execução

Dois containers rodando no Azure:

- mottu-db com MySQL

- mottu-app com sua aplicação

--- 

Ao final você verá:

- O IP público da aplicação

- Os logs da aplicação Java tentando conectar no banco


### Checklist da entrega final
- Aplicação rodando no Azure ACI	✅
- Banco MySQL rodando no Azure ACI	✅
- Logs da aplicação acessando o banco	✅
- IP público acessível	✅
- Dockerfile funcionando	✅
- Script automatizado deploy_full_aci.sh
- 
### A aplicação estará acessível via o IP público atribuído ao container ACI.

---

## 📄 application-aci.properties

O arquivo `application-aci.properties` contém as propriedades específicas para o ambiente **ACI (Application Centric Infrastructure)**. Ele centraliza as configurações de runtime que são sensíveis ao ambiente de execução, como:

- URLs de serviços externos
- Configurações de autenticação
- Flags de comportamento da aplicação
- Variáveis de ambiente específicas para execução em containers ou serviços gerenciados

Esse modelo de externalização da configuração garante maior **portabilidade**, **segurança** e **reutilização** do código em múltiplos ambientes (desenvolvimento, homologação, produção, etc).

**Vantagens:**

- Separação clara entre código e configuração
- Facilita a automação do deploy
- Permite alterações sem necessidade de recompilar a aplicação

---

## 🧪 Script de Automação (`deploy.sh`)

O repositório inclui um script `.sh` totalmente automatizado que executa etapas críticas do processo de implantação com segurança e repetibilidade. Esse script pode se chamar `deploy.sh`, `start.sh`, ou conforme o nome adotado no projeto.

### ✅ Por que usar um script `.sh`?

- Elimina a repetição manual de comandos
- Reduz o risco de erro humano
- Permite **execução idempotente** (você pode rodar várias vezes sem efeitos colaterais)
- Pode ser integrado facilmente em pipelines CI/CD (como GitHub Actions, GitLab CI, Azure DevOps, etc)
- Facilita o onboarding de novos desenvolvedores e operadores


