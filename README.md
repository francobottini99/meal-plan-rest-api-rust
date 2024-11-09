Aquí tienes la traducción del texto:

---

# REST API in Rust

This project involves the development of a *Rest API* for a meal planning system using the *Rocket* framework. The "*backend*" manages a database that stores ingredients, recipes, and meal plans.

> [!NOTE]
> Due to time constraints, simplifications were made to the database, user messages, and logs. Please note that this is a learning-oriented application.

### Authors:
- **Bottini, Franco Nicolas**
- **Robledo, Valentín**

## How to Clone This Repository?

```console
git clone https://github.com/francobottini99/APIRESTRUST-2023.git
```

## How to Use?

First, to test the program, you will need to start a *MySql Server* service. The database schema can be found in the **[database](./database/)** directory of the project.

Then, configure the **[database.env](./server/database.env)** file with the *mysql* address to establish a connection with the database.

Once the database is configured, you can run the server by going to the main directory of the project **[server](./server/)** and using the following commands:

```console
cargo build
```

```console
cargo run
```

Once the server is running, you can use the *endpoints*. In our case, we used the *Postman* software.

## Endpoints

### Ingredients

- <span style="color: green">POST</span> `/api/add/ingredient`: Add an ingredient.
- <span style="color: dodgerblue">GET</span> `/api/get/ingredient`: Get ingredients.
- <span style="color: gold">PUT</span> `/api/update/ingredient`: Update ingredients.
- <span style="color: red">DELETE</span> `/api/delete/ingredient/<id>`: Delete an ingredient by ID.

### Recipes

- <span style="color: green">POST</span> `/api/add/recipe`: Add a recipe.
- <span style="color: dodgerblue">GET</span> `/api/get/recipe`: Get recipes.
- <span style="color: gold">PUT</span> `/api/update/recipe`: Update recipe.
- <span style="color: red">DELETE</span> `/api/delete/recipe/<id>`: Delete a recipe by ID.

### Meal Plans

- <span style="color: green">POST</span> `/api/add/mealplan`: Add a meal plan.
- <span style="color: dodgerblue">GET</span> `/api/get/mealplan`: Get meal plans.
- <span style="color: gold">PUT</span> `/api/update/mealplan`: Update a meal plan.
- <span style="color: red">DELETE</span> `/api/delete/mealplan/<id>`: Delete a meal plan by ID.

### What Does Each *Request* Receive?

### Ingredients

> [!NOTE]
> Simplification for the nutritional values of the ingredients: values are entered per 100 grams.

```json
{
    "id_ingredient": 0,
    "name": "String",
    "proteins": double,
    "carbs": double,
    "fats": double
}
```

### Recipes

> [!NOTE]
> The *id* of each ingredient is provided with the quantity and unit describing that quantity.

```json
{
    "id_recipe": 0,
    "name": "String",
    "category": "String",
    "instructions": "String",
    "ingredients": [
    {
      "id_ingredient": 0,
      "amount": double,
      "unit": "String"
    },
    {
      "id_ingredient": 0,
      "amount": double,
      "unit": "String"
    }
    {
        "..."
    }
  ]
}
```

### Meal Plan

> [!NOTE]
> The *id* of each recipe is provided, specifying the day of the week and which meal of the day it belongs to (breakfast, lunch, dinner).

```json
{
    "id_mealplan": 0,
    "name": "String",
    "category": "String",
    "recipes": [
    {
      "id_recipe": 0,
      "day": "String",
      "meal_type": "String"
    },
    {
      "id_recipe": 0,
      "day": "String",
      "meal_type": "String"
    }
  ]
}
```

## Project Architecture

The design follows a three-layer architecture. It consists of a presentation layer (API), business layer, and data access layer.

### *API Layer* or *Presentation Layer*

The Presentation Layer is the interface that exposes the endpoints to the client. This layer is responsible for receiving requests, validating input data, and serializing and deserializing data to JSON format for the client.

### *Business Layer*

The Business Layer handles the application logic. Here, business rules, processing logic, and complex operations are implemented that should not be directly in the presentation layer. This layer acts as a bridge between the API layer and the data access layer, ensuring the application functions according to the rules.

### *Data Access Layer*

The Data Access Layer interacts directly with the database. It is responsible for performing read and write operations in the database according to the requests from the business layer. This layer handles SQL queries and data manipulation, ensuring that information is stored and retrieved efficiently and securely.

## Database

![Database Schema](imgs/tp3_database_schema.png)

## Basic Examples

### *POST ADD* and *GET* Ingredients

```console
/api/add/ingredient
```
```json
{
    "id_ingredient": 0,
    "name": "Egg",
    "proteins": 14.6,
    "carbs": 0.72,
    "fats": 9.6
}
```
---
```console
/api/get/ingredient
```
![Get Ingredients](imgs/get_ingredients.png)

### *POST ADD* and *GET* Recipes

```console
/api/add/recipe
```
```json
{
    "id_recipe": 0,
    "name": "Scrambled Eggs",
    "category": "Breakfast",
    "instructions": "Beat the egg for 1 minute and cook it in a pan.",
    "ingredients": [
    {
      "id_ingredient": 5,
      "amount": 1,
      "unit": "Unit (one egg)"
    }
  ]
}
```
---
```console
/api/get/recipe
```
![Get Recipe](imgs/get_recipes.png)

### *POST ADD* and *GET* Meal Plan

```console
/api/add/mealplan
```
```json
{
    "id_mealplan": 0,
    "name": "Weekly Plan",
    "category": "Caloric Deficit",
    "recipes": [
    {
      "id_recipe": 9,
      "day": "Monday",
      "meal_type": "Snack"
    },
    {
      "id_recipe": 10,
      "day": "Monday",
      "meal_type": "Breakfast"
    }
  ]
}
```
---
```console
/api/get/mealplan
```

![Get Meal Plans](imgs/get_mealplans.png)
