# 1) Product and Product Category Relationship

In this database schema, there's a clear relationship between the "Product" and "Product_Category" entities.

## Tables Involved

- **Product**: This table represents individual products with attributes such as name, description, SKU, price, etc.
- **Product_Category**: This table represents different categories that products can belong to. Each category has a unique identifier (`id`), a name, and a description.

## Foreign Key Constraint

In the `Product` table, there's a foreign key constraint defined: `category_id INT NOT NULL`. This constraint indicates that the `category_id` column in the `Product` table references the `id` column in the `Product_Category` table.

## Relationship Type

This relationship is a one-to-many relationship from `Product_Category` to `Product`. This means that one product category can have multiple products associated with it, but each product can belong to only one category.

## Usage

By having the `category_id` column in the `Product` table, each product is associated with a specific category identified by its `id` in the `Product_Category` table. This association allows for categorizing and organizing products effectively.

## Example

For example, if we have a category named "Electronics" with `id` 1 in the `Product_Category` table, and there are several products like smartphones, laptops, and headphones, each of these products in the `Product` table could have their `category_id` set to 1, indicating that they belong to the "Electronics" category.




# 2) How could you ensure that each product in the "Product" table has a valid category assigned to it?

To ensure that each product in the "Product" table has a valid category assigned to it, we can enforce a foreign key constraint with the help of a relational database management system (RDBMS) like MySQL.

## 1. Define Foreign Key Constraint

Make sure the `category_id` column in the "Product" table references the `id` column in the "Product_Category" table.

 ```sql
ALTER TABLE Product
ADD CONSTRAINT fk_product_category
FOREIGN KEY (category_id) REFERENCES Product_Category(id);
```

## 2. Use Foreign Key Constraint Options

- ON DELETE RESTRICT: Prevent deletion of categories that have associated products.
- ON UPDATE CASCADE: Update the category id in the "Product" table if the id of the corresponding category in the "Product_Category" table is updated.

```sql
ALTER TABLE Product
ADD CONSTRAINT fk_product_category
FOREIGN KEY (category_id) REFERENCES Product_Category(id)
ON DELETE RESTRICT
ON UPDATE CASCADE;
```

## 3.  Insert Data Carefully

- When inserting data into the "Product" table, ensure that the category_id column always contains a valid category id from the "Product_Category" table.

## 4. Use Transactions

- If possible, use transactions when inserting or updating data in both the "Product" and "Product_Category" tables. This ensures that either all operations succeed or none of them are applied, maintaining data consistency.
