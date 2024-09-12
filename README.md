## User Interface
### Student Tabs

- Event Tab
  - Show a list of events depends on user permission
  - A form to create a new event
- RSO Tab
  - Show a list of available RSOs depends on university
  - Show all RSO that user is currently a member of
  - A form to create a new RSO

### Admin Tabs

- Event Tab
  - Show a list of events depends on user permission
  - Event Form to create a new event
- University Tab
  - A form to create a new university


## Requirements

- [Node](https://nodejs.org/) & [NPM](https://www.npmjs.com/)
- [MySQL](https://www.mysql.com//) Database
- [Docker](https://www.docker.com/) (for development)


## Environment Variables

Create a .env file in the root folder for node server:

- `GOOGLE_KEY` - Google Map API key
- `GEOCODE_URL` - Google Map API URL
- `DB_HOST` - URL of the MySQL server
- `DB_PORT` - Port number that the MySQL server is running on
- `DB_DATABASE` - Name of the database 
- `DB_USERNAME` - Username to connect to the database server
- `DB_PASS` - Password to connect to the database server

Create a .env file in the client folder for react app:

- `REACT_APP_GOOGLE_API_KEY` - Google Map API key

## Development Setup

1. Run `npm install` to install dependencies for server
2. Run `npm run client-install` to install dependencies for client
3. Run `npm run db:rebuild` to setup the database in a Docker container
4. Run `npm run dev` to run server and client concurrently


Server: [http://localhost:5000](http://localhost:5000) 

Client: [http://localhost:3000](http://localhost:3000) 

http://localhost:3000/student/register: create a new student

http://localhost:3000/super-admin/register: create a new super admin


## Endpoints

#### Student Routes

| Method | Endpoint                | Access Control | Description                                  |
| ------ | ----------------------- | -------------- | -------------------------------------------- |
| POST   | `/api/student/login`    | Public         | Return a JWT for that Student.               |
| POST   | `/api/student/register` | Public         | Register a new student.                      |
| GET    | `/api/student/current`  | Public         | Return a student information.                |

#### Super Admin Routes

| Method | Endpoint                      | Access Control         | Description                          |
| ------ | ------------------------------| -----------------------| ------------------------------------ |
| POST   | `/api/super-admin/login`      | Public                 | Return a JWT for that Super Admin.   |
| POST   | `/api/super-admin/register`   | Public                 | Register a new Super Admin.          |
| GET    | `/api/student/current`        | Super Admin            | Return a Super Admin information.    |


#### Event Routes

| Method | Endpoint                  | Access Control        | Description                                        |
| ------ | -----------------------   | -------------------   | -------------------------------------------------- |
| GET    | `/api/event/all`          | Student, Super Admin  | Return all events available for that user.         |
| GET    | `/api/event/:eid`         | Student, Super Admin  | Return full detail of a event                      |
| POST   | `/api/event/create`       | Admin, Super Admin    | Create a new event.                                |

#### RSO Routes

| Method | Endpoint                  | Access Control        | Description                                        |
| ------ | -----------------------   | -------------------   | -------------------------------------------------- |
| POST   | `/api/student/rso/create` | Student               | Create a new RSO.                                  |
| POST   | `/api/student/rso/join`   | Student               | Join an existing RSO                               |
| DELETE | `/api/student/rso/leave`  | Student               | Leave a RSO.                                       |

#### University Routes

| Method | Endpoint                  | Access Control        | Description                                        |
| ------ | -----------------------   | -------------------   | -------------------------------------------------- |
| POST   | `/api/university/create`  | Super Admin           | Create a new university.                           |
| GET    | `/api/university/names`   | Public                | Return a list of available universities            |
| GET    | `/api/university/:uid`    | Public                | Return information of a university                 |
