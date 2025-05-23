# Entidades

---

## Product

Entidade de domínio usada internamente no serviço.

```java
Product {
  String id;
  String name;
  String unit;
  Double price;
}
```

---

## ProductModel

Entidade JPA que representa a tabela `product` no banco de dados.

Campos mapeados com:

- `id_product`: Identificador único do produto.
- `tx_name`
- `tx_unit`
- `double_price`

---

## ProductIn (entrada via API)

```java
ProductIn {
  String name;
  Double price;
  String unit;
}
```

---

## ProductOut (resposta da API)

```java
ProductOut {
  String id;
  String name;
  Double price;
  String unit;
}
```

---

## ProductParser (conversões entre DTOs e entidade)

- `ProductIn` → `Product`.
- `Product` → `ProductOut`.
