---
title: "OQL Select Clause"
url: /refguide8/oql-select-clause/
---

The SELECT clause specifies which entity attributes or other specified data must be retrieved. The `SELECT` clause consists of the term `SELECT` and one or more expressions. These expressions must be separated by a comma. Each expression defines a column in the result.
Each expression can have an alias, which will be the name of the column in the result.

The syntax is as following:

```sql
SELECT [ DISTINCT ]
    {
            *
        | { entity_name | from_alias }.*
        | { expression [ [ AS ] column_alias ] } [ ,...n ]
    }
```

`DISTINCT` – specifies that double rows must not be shown in the result.

`*` (asterisk) – specifies that all attributes from all entities in the FROM clause should be returned.

`entity_name.*`, `from_alias.*` – specifies that all attributes of the specified entity or expression of the FROM clause should be returned. `entity_name` can be optionally put in double quotes. If the entity name is a reserved OQL word (like `Order` or `Group`), double quotes are mandatory.

{{% alert color="info" %}}

```sql {linenos=false}
SELECT Sales.Customer.* FROM Sales.Customer
```

```sql {linenos=false}
SELECT Person.* FROM Sales.Customer AS Person
```

```sql {linenos=false}
SELECT "Sales.Order".* FROM "Sales.Order"
```

{{% /alert %}}

`expression`

Is either a constant, a function or any combination of attribute names, constants, and functions connected by operator(s) or a subquery. When you add more expressions, place a comma between each expression.

{{% alert color="info" %}}

```sql {linenos=false}
SELECT Name AS CustomerName, LastName AS CustomerLastName, Birthday, Category FROM Sales.Customer
```

{{% /alert %}}

See [this page](/refguide8/oql-expressions/) for more information.

`column_alias` – is an alternative name to replace the column name in the result. When the attribute Name is retrieved, the result column is 'Name'. With an alias, you can specify another result column name, like 'Customer Name'. An alias can contain spaces.

{{% alert color="info" %}}

```sql {linenos=false}
SELECT Sales.Customer.Name AS CustomerName FROM Sales.Customer
```

```sql {linenos=false}
SELECT Sales.Customer.Name AS 'Customer Name' FROM Sales.Customer
```

{{% /alert %}}
