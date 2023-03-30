> **Warning**
> **The FoodFinder API is no longer supported.** The database deployment and maintenance period for this project has ended.

# FoodFinder API
This file contains the documentation for [FoodFinder](https://github.com/vsupapo/FoodFinder)'s API.

### Contents
- [Overview](#Overview)
  - [Authentication](#Authentication)
  - [Endpoints](#Endpoints)
  - [Response Codes](#Response-Codes)
- [Resources](#Resources)
  - [Getting all restaurants](#Getting-all-restaurants)
  - [Getting restaurant by ID](#Getting-restaurant-by-ID)
  - [Getting restaurant by keyword](#Getting-restaurant-by-keyword)
  - [Creating a new restaurant](#Creating-a-new-restaurant)
  - [Updating a restaurant](#Updating-a-new-restaurant)
  - [Deleting a restaurant](#Deleting-a-restaurant)

## Overview
The FoodFinder API provides information about restaurants, including restaurant location, cuisine, price range and rating. Our API is organized around REST and returns JSON-formatted responses along with standard HTTP response codes. 

All requests are made to endpoints beginning with:  
`https://foodfinder.com`

All requests must use `https` to be secure. Do **NOT** use `http`.

### Authentication
No authentication is required to access resources for this API.

### Endpoints
| HTTP Method     | Endpoint                                               |  Description                                    |
| -------------   |--------------------------------------------------------|-------------------------------------------------|
| `GET`           | `/restaurants`                                         | Gets a list of all restaurants. |
| `GET`           | `/restaurants/{id}`                                    | Gets a specific restaurant by ID. |
| `GET`           | `/restaurants?restaurant_name={restaurant_name}`       | Gets a list of all restaurants with a specific name. |
| `GET`           | `/restaurants?city={city}`                             | Gets a list of all restaurants in a specific city. |
| `GET`           | `/restaurants?cuisine={cuisine}`                       | Gets a list of all restaurants that serve a specific cuisine. |
| `GET`           | `/restaurants?price={price}`                           | Gets a list of all restaurants in a specific price range. |
| `GET`           | `/restaurants?rating={rating}`                         | Gets a list of all restaurants with a specific rating. |
| `POST`          | `/restaurants`                                         | Creates a new restaurant. |
| `PUT`           | `/restaurants/{id}`                                    | Updates an existing restaurant by ID. |
| `DELETE`        | `/restaurants/{id}`                                    | Deletes a specific restaurant by ID. |

### Response Codes
Possible response codes include:

| Code                      | Description                                                                               |
| ------------------------- |---------------------------------------------------------------------------------------------------------|
| 200 OK	                  | The request succeeded. |
| 400 Bad Request	          | The request was not processed by the server due to client error. |
| 402 Request Failed	      | The parameters were valid but the request failed. |
| 404 Not Found	            | The requested resource cannot be found. |
| 410 Gone                  |	The requested resource is no longer available. |
| 500 Internal Server Error	| The server encountered an unexpected error while fulfilling the request. |

## Resources

### Getting all restaurants
Returns the details of all restaurants.

#### Endpoint:  
```
GET https://foodfinder.com/restaurants
```

#### Example cURL request:  
```
curl -I -X GET https://foodfinder.com/restaurants
```

#### Example response:  
The response contains a list of Restaurant objects within a data envelope. The following is an example response from the `/restaurants` endpoint:
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": [{
      "id": 1,
      "restaurant_name": "Cookie Time",
      "street": "456 West Avenue",
      "city": "San Jose",
      "state": "CA",
      "cuisine": "Dessert",
      "price": "4-9"
    }, {
      "id": 2,
      ...
  }]
}
```

The following table describes the fields of each Restaurant object in the response:
| Field           | Type        | Description                                     |
| ----------------|-------------|-------------------------------------------------|
| `id`	            | Integer	    | A unique number identifier for the restaurant. |
| `restaurant_name`	| String	    | The name of the restaurant. |
| `street`          |	String	    | The city where the restaurant is located. |
| `city`	          | String	    | The state where the restaurant is located. |
| `state`           |	String	    | The state where the restaurant is located. |
| `cuisine`	        | String	    | The type of cuisine served by the restaurant. |
| `price`	          | Integer	    | The price range of the restaurant as a number from 1 to 4. |
| `rating`	        | Integer	    | The average rating of the restaurant as a number from 1 to 5. |

### Getting restaurant by ID
Returns the restaurant details for a specific restaurant ID.

#### Endpoint:  
```
GET https://foodfinder.com/restaurants/{id}
```

#### Path Parameters:
| Field       | Description                                                 |
| ----------- |-------------------------------------------------------------|
| `id`	      | The ID value for the Restaurant object to search for. |

#### Example cURL request:  
The following is an example request where `id` is "1".
```
curl -I -X GET https://foodfinder.com/restaurants/1
```

#### Example response:  
The response contains a single Restaurant object within a data envelope. The following is a sample response from the `/restaurants/{id}` endpoint:
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": {
      "id": 1,
      "restaurant_name": "Cookie Time",
      "street": "456 West Avenue",
      "city": "San Jose",
      "state": "CA",
      "cuisine": "Dessert",
      "price": "4-9"
    }
}
```

The following table describes the fields of each Restaurant object in the response:
| Field           | Type        | Description                                     |
| ----------------|-------------|-------------------------------------------------|
| `id`	            | Integer	    | A unique number identifier for the restaurant. |
| `restaurant_name`	| String	    | The name of the restaurant. |
| `street`          |	String	    | The city where the restaurant is located. |
| `city`	          | String	    | The state where the restaurant is located. |
| `state`           |	String	    | The state where the restaurant is located. |
| `cuisine`	        | String	    | The type of cuisine served by the restaurant. |
| `price`	          | Integer	    | The price range of the restaurant as a number from 1 to 4. |
| `rating`	        | Integer	    | The average rating of the restaurant as a number from 1 to 5. |

### Getting restaurants by keyword
Returns the details of all restaurants with a specific value for:
- `restaurant_name`
- `city`
- `cuisine`
- `price range`
- `rating`

#### Endpoints:  
```
GET https://foodfinder.com/restaurants?restaurant_name={restaurant_name}
```
```
GET https://foodfinder.com/restaurants?city={city}
```
```
GET https://foodfinder.com/restaurants?cuisine={cuisine}
```
```
GET https://foodfinder.com/restaurants?price={price}
```
```
GET https://foodfinder.com/restaurants?rating={rating}
```

#### Query String Parameters:
| Field               | Type        | Required? | Description                                       |
| --------------------|-------------|-----------|---------------------------------------------------|
| `restaurant_name`   | String      | Optional  | The name of the restaurant. |
| `city`              | Optional    | String    | The city where the restaurant is located. |
| `cuisine`           | Optional    | String    | The type of cuisine served by the restaurant. |
| `price`             | Optional    | Integer   | The price range of the restaurant as a number from 1 to 4. |
| `rating`            | Optional    | Integer   | The average rating of the restaurant as a number from 1 to 5. |

#### Example cURL request:  
The following is an example request where `restaurant_name` is "Cream".
```
curl -I -X GET https://foodfinder.com/restaurants?restaurant_name=Cream
```

#### Example response:  
The response contains a list of Restaurant objects within a data envelope. The following is a sample response from the `/restaurants?restaurant_name={restaurant_name}` endpoint:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": [{
      "id": 2,
      "restaurant_name": "Cream",
      "street": "789 East Avenue",
      "city": "San Jose",
      "state": "CA",
      "cuisine": "Dessert",
      "price": "1-3"
    }, {
      "id": 2,
      ...
    }]
}
```

The following table describes the fields of each Restaurant object in the response:

| Field           | Type        | Description                                     |
| ----------------|-------------|-------------------------------------------------|
| `id`	            | Integer	    | A unique number identifier for the restaurant. |
| `restaurant_name`	| String	    | The name of the restaurant. |
| `street`          |	String	    | The city where the restaurant is located. |
| `city`	          | String	    | The state where the restaurant is located. |
| `state`           |	String	    | The state where the restaurant is located. |
| `cuisine`	        | String	    | The type of cuisine served by the restaurant. |
| `price`	          | Integer	    | The price range of the restaurant as a number from 1 to 4. |
| `rating`	        | Integer	    | The average rating of the restaurant as a number from 1 to 5. |

### Creating a new restaurant
Creates a Restaurant object using the provided Restaurant object details. 

#### Endpoint:
```
POST https://foodfinder.com/restaurants
```

#### Object Parameters:  
The values for the following fields can be defined when creating a new Restaurant object:

| Field           | Type        | Description                                     |
| ----------------|-------------|-------------------------------------------------|
| `restaurant_name`	| String	    | The name of the restaurant. |
| `street`          |	String	    | The city where the restaurant is located. |
| `city`	          | String	    | The state where the restaurant is located. |
| `state`           |	String	    | The state where the restaurant is located. |
| `cuisine`	        | String	    | The type of cuisine served by the restaurant. |
| `price`	          | Integer	    | The price range of the restaurant as a number from 1 to 4. |
| `rating`	        | Integer	    | The average rating of the restaurant as a number from 1 to 5. |

#### Example cURL request:  

```
curl -I -X POST -H 'Content-Type: application/json'
-d '{"restaurant_name":"Pizza Palace","street":"123 South Street",
"city":"San Jose", "state":"CA", "cuisine":"Italian", 
"price":"4-9"}' http://www.foodfinder.com/restaurants
```

#### Example response:  
The response contains a single Restaurant object within a data envelope. The following is an example response from the `/restaurants` endpoint:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": {
      "id": 225,
      "restaurant_name": "Pizza Palace",
      "street": "123 South Street",
      "city": "San Jose",
      "state": "CA",
      "cuisine": "Italian",
      "price": "4-9"
    }
}
```

The following table describes the fields of each Restaurant object in the response:

| Field           | Type        | Description                                     |
| ----------------|-------------|-------------------------------------------------|
| `id`	            | Integer	    | A unique number identifier for the restaurant. |
| `restaurant_name`	| String	    | The name of the restaurant. |
| `street`          |	String	    | The city where the restaurant is located. |
| `city`	          | String	    | The state where the restaurant is located. |
| `state`           |	String	    | The state where the restaurant is located. |
| `cuisine`	        | String	    | The type of cuisine served by the restaurant. |
| `price`	          | Integer	    | The price range of the restaurant as a number from 1 to 4. |
| `rating`	        | Integer	    | The average rating of the restaurant as a number from 1 to 5. |

### Updating a restaurant
Updates a Restaurant object with a specific ID using the provided Restaurant object details. 

#### Endpoint:  
```
PUT https://foodfinder.com/restaurants/{id}
```

#### Path Parameters:  
| Field       | Description                                                 |
| ----------- |-------------------------------------------------------------|
| `id`	      | The ID value for the Restaurant object to be updated. |

#### Object Parameters:  
The values for the following fields can be changed when updating a Restaurant object:

| Field           | Type        | Description                                     |
| ----------------|-------------|-------------------------------------------------|
| `restaurant_name`	| String	    | The name of the restaurant. |
| `street`          |	String	    | The city where the restaurant is located. |
| `city`	          | String	    | The state where the restaurant is located. |
| `state`           |	String	    | The state where the restaurant is located. |
| `cuisine`	        | String	    | The type of cuisine served by the restaurant. |
| `price`	          | Integer	    | The price range of the restaurant as a number from 1 to 4. |
| `rating`	        | Integer	    | The average rating of the restaurant as a number from 1 to 5. |

#### Example cURL request:  
The following is an example request where `id` is "255" and the updated `price` is "2-5".

```
curl -I -X PUT -H 'Content-Type: application/json'
-d '{"price":"2-5"}' http://www.foodfinder.com/restaurants/225
```

#### Example response:  
The response contains a single Restaurant object within a data envelope. The following is a sample response from the `/restaurants/{id}` endpoint:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": {
      "id": 225,
      "restaurant_name": "Pizza Palace",
      "street": "123 South Street",
      "city": "San Jose",
      "state": "CA",
      "cuisine": "Italian",
      "price": "2-5"
    }
}
```

The following table describes the fields of each Restaurant object in the response:

| Field           | Type        | Description                                     |
| ----------------|-------------|-------------------------------------------------|
| `id`	            | Integer	    | A unique number identifier for the restaurant. |
| `restaurant_name`	| String	    | The name of the restaurant. |
| `street`          |	String	    | The city where the restaurant is located. |
| `city`	          | String	    | The state where the restaurant is located. |
| `state`           |	String	    | The state where the restaurant is located. |
| `cuisine`	        | String	    | The type of cuisine served by the restaurant. |
| `price`	          | Integer	    | The price range of the restaurant as a number from 1 to 4. |
| `rating`	        | Integer	    | The average rating of the restaurant as a number from 1 to 5. |

### Deleting a restaurant
Deletes a Restaurant object with a specific restaurant ID. 

#### Endpoint:  
```
DELETE https://foodfinder.com/restaurants/{id}
```

#### Path Parameters:  
| Field       | Description                                                 |
| ----------- |-------------------------------------------------------------|
| `id`	      | The ID value for the Restaurant object to be deleted. |

#### Example cURL request:  
The following is an example request where `id` is "225".

```
curl -I -X DELETE http://www.foodfinder.com/restaurants/225
```

#### Example response:  
The response contains a single Restaurant object within a data envelope. The following is a sample response from the `/restaurants/{id}` endpoint:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "status": success
  "message": "Successfully deleted restaurant with id: 225."
}
```

The following table describes the fields in the body of the response:

| Field           | Type        | Description                                     |
| ----------------|-------------|-------------------------------------------------|
| `status`	  | String      | The status of the request set to "success" upon fulfillment or "unsuccessful" upon failure. |
| `message`	  | String      | A message providing more details on request status. |
