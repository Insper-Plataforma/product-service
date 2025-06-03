# Arquitetura

## Estrutura de Pastas

```bash
src/main/java/store/product/
├── Product.java # Entidade de domínio
├── ProductModel.java # Entidade JPA
├── ProductRepository.java # Repositório JPA
├── ProductService.java # Lógica de negócio
├── ProductParser.java # Conversões entre DTOs e entidade
├── ProductResource.java # Implementação REST (controller)
└── ProductApplication.java # Classe principal
└── resources/
│ ├── application.yaml # Configurações de ambiente
│ └── db/migration/ # Scripts Flyway
```
