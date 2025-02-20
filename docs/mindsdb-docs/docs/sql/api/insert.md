# `#!sql INSERT INTO` Statement

## Description

The `#!sql INSERT INTO` statement inserts data into a table. The data comes from a subselect query. It is commonly used to input prediction results into a database table.

## Syntax

Here is the syntax:

```sql
INSERT INTO [integration_name].[table_name]
    (SELECT ...);
```

Please note that the destination table (`[integration_name].[table_name]`) must exist and contain all the columns where the data is to be inserted.

And the steps followed by the syntax:

- It executes a subselect query to get the output dataset.
- It uses the `#!sql INSERT INTO` statement to insert the output of the `#!sql (SELECT ...)` query into the `[integration_name].[table_name]` table.

On execution, we get:

```sql
Query OK, 0 row(s) updated - x.xxxs
```

## Example

We want to save the prediction results into the `#!sql int1.tbl1` table.

Here is the schema structure used throughout this example:

```bash
int1
└── tbl1
mindsdb
└── predictor_name
int2
└── tbl2
```

Where:

| Name             | Description                                                                                  |
| ---------------- | -------------------------------------------------------------------------------------------- |
| `int1`           | Integration where the table that stores prediction results resides.                          |
| `tbl1`           | Table that stores prediction results.                                                        |
| `predictor_name` | Name of the model.                                                                           |
| `int2`           | Integration where the data source table used in the inner `#!sql SELECT` statement resides.  |
| `tbl2`           | Data source table used in the inner `#!sql SELECT` statement.                                |

Let's execute the query.

```sql
INSERT INTO int1.tbl1 (
    SELECT *
    FROM int2.tbl2 AS ta
    JOIN mindsdb.predictor_name AS tb
    WHERE ta.date > '2015-12-31'
);
```

On execution, we get:

```sql
Query OK, 0 row(s) updated - x.xxxs
```
