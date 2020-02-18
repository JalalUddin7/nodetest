# Event Hubs Data Generator Documentation

## JSON-Faker-Schema

Event Hub Data Generator (EHDG) is heavily based on the work of JSON-Schema-Faker's JavaScript library. JSON-Faker-Schema can generate realistic fake data in JSON format for many areas, including people, address, finance, and company etc. The data generated will be based on the schema provided by the user. JSON-Faker-Schema adheres to the JSON Schema, which is a standard for a valid JSON file. 

A very simple example of valid schema;

```json
{
  "firstName": {
    "type": "string",
    "faker": "name.firstName"
  }
}
```

Given that Event Hubs Data Generator makes use of a library called JSON-Faker-Schema - it would be wise to refer to the documentation provided on their [Github](https://github.com/json-schema-faker/json-schema-faker/) when you're getting started. Their website includes a [playground environment](https://json-schema-faker.js.org/) that is especially useful when testing whether your schema is valid.

### Providers

The concept of providers is an important one in JSON-Faker-Schema - providers are the generator attributes that are packaged together. For instance, generator attributes such as firstName, lastName are packaged into a Provider called Person. Providers can be thought of as logical groupings of attributes. A complete and exhaustive list of providers can be found on the [Faker Github Wiki](https://github.com/Marak/faker.js/wiki).

## How EHDG Works

This tool is web based, and as such, the implementation differs slightly from the documentation in the Github repository for the library we are using. We are using HTML forms (index.html) to pass data into the JavaScript file (index.js) which includes the Faker logic.

In the textbox field 'method' you need to provide a valid schema:

``` json
{
  "firstName": {
    "type": "string",
    "faker": "name.firstName"
  }
}
```

In our index.js file we can pass these values from the form using the Requests library. Here's an example of how it works:

```javascript
var method = req.body.method;
```

Once we have the form values we can then perform our Faker logic:

```javascript
var dataJSON = JSON.parse(method);
        var data = fakerSchema.generate(dataJSON);
        const eventData = {body: data};
        client.send(eventData); 
```

Outputting 'eventData' to console would look like this:

```json
{
  "firstName": "Oswald"
}
```

## 