---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction
More-Recipes provides a platform for users to share the awesome and exciting  recipe ideas they have invented or learnt.  Suppose a user comes up with a food recipe,  he/she can post it on More-Recipes and  get feedback in form of reviews and votes from other users who explore that recipe. Users can also keep a list of their favorite recipes on the application.

# Development
The application was developed with [NodeJs](http://nodejs.org) and [Express](http://expressjs.com) is used for routing. The [PostgreSQL](https://www.postgresql.org) database was used with [Sequelize](http://sequelize.readthedocs.io) as the ORM

#Installation
1.  Ensure you have NodeJs and PostgreSQL installed
2.  Clone the repository `https://github.com/Ruqoyah/More-Recipes.git`
3.  Change your directory `cd More-Recipes`
4.  Install all dependencies `npm install`
5.  Start the app `npm start` for development Or
7.  Use [postman] to consume the API

# Authentication
More-Recipes uses (username and password) to login to allow access to the API protected routes. On registering or login, a token is generated.
More-Recipes expect the token to be included in the header or body as `x-access-token: token`. All API requests to the server are stated below

# Api Summary
## Below are the API endpoints and their functions
EndPoint                                                |   Functionality
--------------------------------------------------------|------------------------
POST /api/v1/users/signup                               |   Create a new users.
POST /api/v1/users/signin                               |   Login users.            
GET /api/v1/users/profile                               |   Get user details.
PUT /api/v1/users/profile                               |   Edit profile.
POST /api/v1/users/exist                                |   Check if username or email exist.
POST /api/v1/recipes                                    |   Add recipes
GET /api/v1/user/recipes?page=:page                     |   Get user recipes
GET /api/v1/recipes?search=:keyword                     |   Search recipe
GET /api/v1/recipes?sort=upvotes&order=descending       |   Get most upvote recipes 
GET /api/v1/recipes?page=:page                          |   Get all recipes
PUT /api/v1/recipes/:recipeId                           |   Modify recipes
GET /api/v1/recipes/:recipeId                           |   View recipes
DELETE /api/v1/recipes/:recipeId                        |   Delete recipes
POST /api/v1/recipes/:recipeId/reviews                  |   Post reviews
GET /api/v1/recipes/:recipeId/reviews?page=:page        |   Get recipe reviews
POST /api/v1/recipes/:recipeId/favorite                 |   Add favorite recipes
GET api/v1/users/recipes/favorite?page=:page            |   Get User favorite recipes
POST /api/v1/recipes/:recipeId/upvote                   |   Upvote recipes
POST /api/v1/recipes/:recipeId/downvote                 |   Downvote recipes


# Users

## Sign up User
### Request
  * Endpoint: Post: `/api/v1/users/signup` 
  * Body  `(application/json)` 

### Response
  * Status: `201 created` 
  * Body  `(application/json)` 

> Request:

```json
{
    "username": "ruqoyah",
    "fullName": "rukayat odukoya",
    "email": "ruqoyah@gmail.com",
    "password": "password"
},
```
<aside class="notice">You must set the token at the header or body after sign up to access protected routes (x-access-token: token)</aside>

> Response:

```json

{
    "status": true,
    "message": "You have successfully signed up",
    "data": {
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1MTMwNDE3MzIsImN1cnJlbnRVc2VyIjp7InVzZXJJZCI6MSwidXNlcm5hbWUiOiJydXFveWFoIiwiaXNBZG1pbiI6MH0sImlhdCI6MTUxMjk1NTMzMn0.342PBgJwdv_INYZTbApHzZH1uemUHiKj51JvvuW_MEU"
    }
}

```

## Sign in User
### Request
  * Endpoint: Post: `/api/v1/users/signin` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 

> Request:

```json
{
    "username": "ruqoyah",
    "password": "password"
},
```
<aside class="notice">You must set the token at the header or body after login to access protected routes (x-access-token: token)</aside>

> Response:

```json
{
    "status": true,
    "message": "You have successfully signed in!",
    "data": {
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1MTMwNDE3OTQsImN1cnJlbnRVc2VyIjp7InVzZXJJZCI6MSwidXNlcm5hbWUiOiJydXFveWFoIiwiaXNBZG1pbiI6MH0sImlhdCI6MTUxMjk1NTM5NH0._Y-DujUKn0LYLdk0NbzD7TWRILPXfMPeRwuhFEmGcc0"
    }
}

```

## Get User Details
### Request
  * Endpoint: Get: `/api/v1/users/profile` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 

> Response:

```json
{
    "status": true,
    "data": { 
        "id": 1,
        "username": "ruqoyah",
        "fullName": "rukayat odukoya",
        "email": "ruqoyah@andela.com",
        "picture": null
    }
}


```

## Edit profile
### Request
  * Endpoint: Put: `/api/v1/users/profile` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 

> Request:

```json
{
    "username": "rukkie",
    "picture": "t5rqx9hzbat7f93mgwjn"
},
```

> Response:

```json
{
    "status": true,
    "message": "Profile updated sucessfully!",
    "data": {
        "username": "rukkie",
        "fullName": "rukayat odukoya",
        "email": "ruqoyah@andela.com",
        "picture": "t5rqx9hzbat7f93mgwjn",
        "id": 1
    }
}

```

## Check if username exist
### Request
  * Endpoint: Post: `/api/v1/users/exist` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 

> Request:

```json
{
    "username": "rukkie"
},
```

> Response:

```json

{
    "status": true
}

```

## Check if email exist
### Request
  * Endpoint: Post: `/api/v1/users/exist` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 

> Request:

```json
{
    "email": "ruqoyah@gmail.com"
},
```

> Response:

```json

{
    "status": true
}

```

# Recipe

## Add Recipe
### Request
  * Endpoint: Post: `/api/v1/recipes` 
  * Body  `(application/json)` 

### Response
  * Status: `201 created` 
  * Body  `(application/json)` 
  
> Request:

```json
{
    "recipeName": "sweet pizza",
    "ingredient": "pizza",
    "details": "pizza",
    "picture": "et1xp6qa7a7cznkfpgwn"
},
```

> Response:

```json

{
    "status": true,
    "message": "Recipe added successfully",
    "data": {
        "upvotes": 0,
        "downvotes": 0,
        "views": 0,
        "id": 1,
        "recipeName": "sweet pizza",
        "ingredient": "pizza",
        "details": "pizza",
        "picture": "et1xp6qa7a7cznkfpgwn",
        "userId": 1,
        "updatedAt": "2017-12-11T01:36:28.173Z",
        "createdAt": "2017-12-11T01:36:28.173Z"
    }
}

```

## Get User Recipes
### Request
  * Endpoint: Get: `/api/v1/users/recipes?page=1` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 
  
<aside class="notice">You can always change the `number` in the Endpoint to go to the next page if page is more than one </aside>

> Response:

```json

{
    "status": true,
    "recipes": {
        "count": 2,
        "rows": [
            {
                "id": 1,
                "recipeName": "sweet pizza",
                "ingredient": "pizza",
                "details": "pizza",
                "picture": "et1xp6qa7a7cznkfpgwn",
                "userId": 1,
                "upvotes": 0,
                "downvotes": 0,
                "views": 0,
                "createdAt": "2017-12-11T01:36:28.173Z",
                "updatedAt": "2017-12-11T01:36:28.173Z"
            },
            {
                "id": 2,
                "recipeName": "Rice",
                "ingredient": "oil and so on",
                "details": "cook the rice ",
                "picture": "et1xp6qa7a7cznkfpgwn",
                "userId": 1,
                "upvotes": 0,
                "downvotes": 0,
                "views": 0,
                "createdAt": "2017-12-11T01:59:30.480Z",
                "updatedAt": "2017-12-11T01:59:30.480Z"
            }
        ]
    },
    "pages": 1
}

```

## Get All Recipes
### Request
  * Endpoint: Get: `/api/v1/recipes?page=1` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 
  
<aside class="notice">You can always change the `number` in the Endpoint to go to the next page if page is more than one </aside>

> Response:

```json

{
    "status": true,
    "recipes": {
        "count": 3,
        "rows": [
            {
                "id": 1,
                "recipeName": "sweet pizza",
                "ingredient": "pizza",
                "details": "pizza",
                "picture": "et1xp6qa7a7cznkfpgwn",
                "userId": 1,
                "upvotes": 0,
                "downvotes": 0,
                "views": 0,
                "createdAt": "2017-12-11T01:36:28.173Z",
                "updatedAt": "2017-12-11T01:36:28.173Z",
                "User": {
                    "username": "rukkie"
                }
            },
            {
                "id": 2,
                "recipeName": "Rice",
                "ingredient": "oil and so on",
                "details": "cook the rice ",
                "picture": "et1xp6qa7a7cznkfpgwn",
                "userId": 1,
                "upvotes": 0,
                "downvotes": 0,
                "views": 0,
                "createdAt": "2017-12-11T01:59:30.480Z",
                "updatedAt": "2017-12-11T01:59:30.480Z",
                "User": {
                    "username": "rukkie"
                }
            },
            {
                "id": 3,
                "recipeName": "sweet rice",
                "ingredient": "sweet",
                "details": "cook",
                "picture": "et1xp6qa7a7cznkfpgwn",
                "userId": 2,
                "upvotes": 0,
                "downvotes": 0,
                "views": 0,
                "createdAt": "2017-12-11T02:04:31.728Z",
                "updatedAt": "2017-12-11T02:04:31.728Z",
                "User": {
                    "username": "topey"
                }
            }
        ]
    },
    "pages": 1
}

```

## Search Recipe
### Request
  * Endpoint: Get: `/api/v1/recipes?search=pizza` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 
  
<aside class="notice">You can always change the `pizza` in the Endpoint to any recipe name you wish to search</aside>

> Response:

```json

{
    "status": true,
    "data": [
        {
            "id": 1,
            "recipeName": "sweet pizza",
            "ingredient": "pizza",
            "details": "pizza",
            "picture": "et1xp6qa7a7cznkfpgwn",
            "userId": 1,
            "upvotes": 0,
            "downvotes": 1,
            "views": 0,
            "createdAt": "2017-12-11T01:36:28.173Z",
            "updatedAt": "2017-12-11T02:36:29.761Z"
        }
    ]
}

```

## Get Recipes with the most upvotes
### Request
  * Endpoint: Get: `/api/v1/recipes?sort=upvotes&order=descending` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 

> Response:

```json

{
    "status": true,
    "recipes": [
        {
            "id": 3,
            "recipeName": "sweet rice",
            "ingredient": "sweet",
            "details": "cook",
            "picture": "et1xp6qa7a7cznkfpgwn",
            "userId": 2,
            "upvotes": 1,
            "downvotes": 0,
            "views": 0,
            "createdAt": "2017-12-11T02:04:31.728Z",
            "updatedAt": "2017-12-11T02:04:31.728Z"
        },
        {
            "id": 1,
            "recipeName": "sweet pizza",
            "ingredient": "pizza",
            "details": "pizza",
            "picture": "et1xp6qa7a7cznkfpgwn",
            "userId": 1,
            "upvotes": 0,
            "downvotes": 1,
            "views": 0,
            "createdAt": "2017-12-11T01:36:28.173Z",
            "updatedAt": "2017-12-11T02:36:29.761Z"
        }
    ]
}

```

## Modify Recipe
### Request
  * Endpoint: Put: `/api/v1/recipes/:recipeId` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 
  
> Request:

```json
{
    "recipeName": "Coconut Rice"
},
```

> Response:

```json
{
    "status": true,
    "message": "Recipe modified successfully!",
    "data": {
        "id": 2,
        "recipeName": "Coconut Rice",
        "ingredient": "oil and so on",
        "details": "cook the rice ",
        "picture": "et1xp6qa7a7cznkfpgwn",
        "userId": 1,
        "upvotes": 0,
        "downvotes": 0,
        "views": 1,
        "createdAt": "2018-01-12T11:44:13.423Z",
        "updatedAt": "2018-01-13T02:19:27.600Z"
    }
}

```

## View Recipe
### Request
  * Endpoint: Get: `/api/v1/recipes/:recipeId` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 

> Response:

```json
{   
    "recipe": {
        "id": 2,
        "recipeName": "Coconut Rice",
        "ingredient": "oil and so on",
        "details": "cook the rice ",
        "picture": "et1xp6qa7a7cznkfpgwn",
        "userId": 1,
        "upvotes": 0,
        "downvotes": 0,
        "views": 2,
        "createdAt": "2017-12-11T01:59:30.480Z",
        "updatedAt": "2017-12-11T02:12:13.175Z"
    }
}

```

## Delete Recipe
### Request
  * Endpoint: Delete: `/api/v1/recipes/:recipeId` 
  * Body  `(application/json)` 

### Response
  * Status: `204 no content` 
  * Body  `(application/json)` 

> Response:

```json
{
    "status": true,
    "message": "Recipe deleted successfully!",
    "data": {
        "id": 2
    }
}

```

## Post Review
### Request
  * Endpoint: Post: `/api/v1/recipes/:recipeId/reviews` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 
  
> Request:

```json
{
    "review": "nice recipe"
},
```

> Response:

```json
{
    "status": true,
    "data": {
        "id": 1,
        "recipeId": 1,
        "userId": 1,
        "review": "nice recipe",
        "updatedAt": "2017-12-11T02:14:32.368Z",
        "createdAt": "2017-12-11T02:14:32.368Z",
        "User": {
            "picture": "eaiy6a1o9tpeemybqrrr",
            "username": "rukkiey"
        }
    }
}

```

## Get Recipe Reviews
### Request
  * Endpoint: Get: `/api/v1/recipes/:recipeId/reviews?page=1` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 

<aside class="notice">You can always change the `number` in the Endpoint to go to the next page if page is more than one </aside>

> Response:

```json
{
    "status": true,
    "reviews": {
        "count": 2,
        "rows": [
            {
                "id": 1,
                "recipeId": 1,
                "userId": 1,
                "review": "nice recipe",
                "updatedAt": "2017-12-11T02:14:32.368Z",
                "createdAt": "2017-12-11T02:14:32.368Z",
                "User": {
                    "picture": "eaiy6a1o9tpeemybqrrr",
                    "username": "rukkiey"
                }
            },
            {
                "id": 6,
                "userId": 1,
                "recipeId": 14,
                "review": "nice",
                "createdAt": "2018-01-13T06:07:25.842Z",
                "updatedAt": "2018-01-13T06:07:25.842Z",
                "User": {
                    "picture": "eaiy6a1o9tpeemybqrrr",
                    "username": "rukkieyyyey"
                }
            }
        ]
    },
    "pages": 1
}

```

## Add Favorite Recipe
### Request
  * Endpoint: Post: `/api/v1/recipes/:recipeId/favorite` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 
  

> Response:

```json
{
    "status": true,
    "message": "You successfully favorited this recipe",
    "data": {
        "recipeId": 3
    }
}

```

## Get User Favorite Recipes
### Request
  * Endpoint: Get: `/api/v1/users/recipes/favorite?page=1` 
  * Body  `(application/json)`

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 

<aside class="notice">You can always change the `number` in the Endpoint to go to the next page if page is more than one </aside>
  
> Response:

```json
{
    "status": true,
    "favoriteRecipes": {
        "count": 6,
        "rows": [
            {
                "id": 1,
                "userId": 1,
                "recipeId": 1,
                "createdAt": "2017-12-11T02:20:47.029Z",
                "updatedAt": "2017-12-11T02:20:47.029Z",
                "Recipe": {
                    "recipeName": "sweet pizza",
                    "ingredient": "pizza",
                    "details": "pizza",
                    "upvotes": 0,
                    "downvotes": 0,
                    "picture": "et1xp6qa7a7cznkfpgwn",
                    "views": 0,
                    "createdAt": "2017-12-11T01:36:28.173Z",
                    "User": {
                        "username": "rukkie"
                    }
                }
            },
            {
                "id": 2,
                "userId": 1,
                "recipeId": 3,
                "createdAt": "2017-12-11T02:23:37.682Z",
                "updatedAt": "2017-12-11T02:23:37.682Z",
                "Recipe": {
                    "recipeName": "sweet rice",
                    "ingredient": "sweet",
                    "details": "cook",
                    "upvotes": 0,
                    "downvotes": 0,
                    "picture": "et1xp6qa7a7cznkfpgwn",
                    "views": 0,
                    "createdAt": "2017-12-11T02:04:31.728Z",
                    "User": {
                        "username": "topey"
                    }
                }
            }
        ]
    },
    "pages": 1
}

```

## Upvote Recipe
### Request
  * Endpoint: Post: `/api/v1/recipes/:recipeId/upvote` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 
  
> Response:

```json
{
    "status": true,
    "message": "upvote successful",
    "data": {
        "id": 3,
        "recipeName": "Fdghjl",
        "ingredient": "fghj",
        "details": "fghj",
        "picture": "b0norcjiw3eysf4xzwao",
        "userId": 3,
        "upvotes": 1,
        "downvotes": 0,
        "views": 7,
        "createdAt": "2018-01-11T12:13:05.554Z",
        "updatedAt": "2018-01-13T06:14:02.837Z",
        "User": {
            "username": "rukky"
        }
    }
}

```

## Downvote Recipe
### Request
  * Endpoint: Post: `/api/v1/recipes/:recipeId/downvote` 
  * Body  `(application/json)` 
  
### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 
  
> Response:

```json
{
    "status": true,
    "message": "vote updated successfully",
    "data": {
        "id": 3,
        "recipeName": "Fdghjl",
        "ingredient": "fghj",
        "details": "fghj",
        "picture": "b0norcjiw3eysf4xzwao",
        "userId": 3,
        "upvotes": 0,
        "downvotes": 1,
        "views": 7,
        "createdAt": "2018-01-11T12:13:05.554Z",
        "updatedAt": "2018-01-13T06:14:02.837Z",
        "User": {
            "username": "rukky"
        }
    }
}

```
