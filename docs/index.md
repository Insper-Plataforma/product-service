# Product Service

O `product-service` é responsável por **cadastrar, listar, buscar e remover produtos** do sistema. Ele implementa a interface `ProductController` e utiliza JPA para persistência em banco de dados relacional.

---

## Funcionalidades

- **Criar novos produtos com validação**: Permite o cadastro de produtos com validações de campos obrigatórios e formatos.
- **Listar todos os produtos**: Exibe uma lista paginada de todos os produtos cadastrados.
- **Buscar produto por ID**: Permite consultar detalhes de um produto específico pelo seu ID.
- **Remover produto por ID**: Permite a exclusão de um produto específico pelo seu ID, com validação para evitar remoção de produtos inexistentes.

---

## Cache com Redis

Para otimizar a performance de leitura, o `product-service` utiliza **Redis** como sistema de cache:

- Dados de produtos frequentemente consultados são armazenados em Redis.
- Isso reduz a carga no banco de dados relacional e diminui o tempo de resposta.
- As entradas em cache possuem tempo de expiração configurável (TTL) para garantir a atualização periódica das informações.

---

## Observabilidade (Prometheus + Grafana)

O serviço integra métricas e logs ao **Prometheus** e ao **Grafana** para monitoramento e visualização em tempo real:

- **Prometheus**
  - Coleta métricas HTTP (latência, número de requisições, códigos de resposta) e métricas internas do JVM.
  - Configurado para raspar (`scrape`) o endpoint `/actuator/prometheus` exposto pelo Spring Boot.
- **Grafana**
  - Consome os dados do Prometheus e gera dashboards customizados.
  - Permite acompanhar trends de uso, identificar gargalos e disparar alertas quando thresholds são ultrapassados.

Essa camada de observabilidade facilita a detecção de anomalias, otimização de performance e tomada de decisões operacionais.

---

## Integração com Jenkins

Este projeto conta com um arquivo Jenkinsfile (na raiz do repositório) que define uma pipeline de integração contínua para compilar automaticamente o módulo sempre que houver alterações no repositório.

### Para que serve?

- Compilação automatizada: toda alteração no repositório dispara o build do Maven, detectando problemas de compilação antes do merge.

- Imagens Docker consistentes: gera e publica automaticamente imagens multiplataforma, facilitando o deploy em diferentes ambientes (x86_64 e ARM).

- Segurança das credenciais: utiliza credenciais armazenadas no Jenkins (identificador dockerhub-credential), evitando exposição de senhas no código.

Dessa forma, a integração com Jenkins garante que o product-service esteja sempre compilando e empacotado corretamente, com uma imagem Docker pronta para ser implantada nos clusters de produção ou QA.
