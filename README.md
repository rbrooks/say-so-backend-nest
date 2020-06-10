# SaySo Backend: NestJS

Hobby project to learn the [NestJS](https://nestjs.com/) Node.js framework and TypeORM.

## Installation

Clone:

```:bash
$ git clone git@github.com:iq9/say-so-backend-nest.git
```

Make a copy of the JSON Web Token secret, and change it accordingly:

```:bash
$ cp src/config.ts.example src/config.ts
```

Do the same with the database config:

```:bash
$ cp ormconfig.json.example ormconfig.json
```

Change ormconfig.json accordingly:

```:json
{
    "type": "mysql",
    "host": "localhost",
    "port": 3306,
    "username": "appuser",
    "password": "password",
    "database": "sayso",
    "entities": ["src/**/**.entity{.ts,.js}"],
    "synchronize": true
}
```

**IMPORTANT:** The `mysql` NPM package doesn't support MySQL 8.0.4 and newer yet. You can coerce it by:

```:sql
ALTER USER 'appuser'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

For more info, see the discussion on this PR (still open as of 6/9/2020): https://github.com/mysqljs/mysql/pull/1962

Install dependencies:

```:bash
$ npm install
```

Run the Server:

```:bash
$ npm start
```

It should create DB tables. You may have to create the DB manaually first.

```:bash
CREATE DATABASE sayso;
```

REST API should now be accessible over HTTP at `http://localhost:3000/api/articles`

## Scripts

- `npm start` - Start Service
- `npm run start:watch` - Start Service, then watch code for changes.
- `npm run test` - Run Test Suite - Uses Jest. Not much here yet.
- `npm run start:prod` - Start App on Production

## API Docs

Swagger API Docs are browseable at: http://localhost:3000/docs/

![api-say-so-blog2](https://user-images.githubusercontent.com/214047/84197948-c9fbc180-aa70-11ea-94d0-8cf40ce19b44.png)

![api-say-so-blog](https://user-images.githubusercontent.com/214047/84197947-c9632b00-aa70-11ea-8488-31856c83e7f0.png)

## Authentication

Uses JSON Web Tokens (JWT) for Authentication. The token is passed with each Request using the `Authorization` header with `Token` scheme. The JWT authentication middleware handles the validation and authentication of the token.
