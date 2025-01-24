# mock-pulsifi-json-server

#### Prerequisite
* Create a folder
```
mkdir mock-pulsifi-json-server
cd mock-pulsifi-json-server
```

#### Step 1: Create a node js project
```
npm init -y
```

#### Step 2: Install json server dependency
```
npm i json-server
```

#### Step 3: Create server.js
```js
const jsonServer = require('json-server')

const server = jsonServer.create()

const router = jsonServer.router('db.json')
const middlewares = jsonServer.defaults()
 
server.use(middlewares)
server.use('/api', router)
server.listen(process.env.PORT || 5001, () => {
  console.log('JSON Server is running')
})


```


#### Step 4: Create db.json
<details>
<summary>db.json</summary>

```js
{
  "employees": [
    {
      "id": "1",
      "firstName": "John",
      "lastName": "Slug",
      "email": "john.slug@example.com",
      "department": "Engineering",
      "role": {
        "name": "Manager",
        "permissions": [
          "view_employees",
          "edit_profile"
        ]
      },
      "startDate": "2024-01-17T00:00:00.000Z",
      "status": "inactive"
    },
  ],
  "roles": [
    {
      "id": "1",
      "name": "Admin",
      "permissions": [
        "manage_users",
        "manage_roles",
        "view_all",
        "edit_all",
        "manage_employees",
        "view_employees"
      ]
    },
  ],
  "permissions": [
    {
      "id": "1",
      "name": "manage_users",
      "description": "Can manage all user accounts"
    },
  ],
  "users": [
    {
      "id": "1",
      "email": "admin@example.com",
      "password": "admin123",
      "firstName": "Admin",
      "lastName": "User",
      "role": {
        "name": "Admin",
        "permissions": [
          "manage_users",
          "manage_roles",
          "view_all",
          "edit_all",
          "manage_employees",
          "view_employees"
        ]
      }
    },
    {
      "id": "2",
      "email": "manager@example.com",
      "password": "manager123",
      "firstName": "Manager",
      "lastName": "User",
      "role": {
        "name": "Manager",
        "permissions": [
          "view_team",
          "edit_team",
          "view_all",
          "manage_employees",
          "view_employees"
        ]
      }
    },
    {
      "id": "3",
      "email": "employee@example.com",
      "password": "employee123",
      "firstName": "John",
      "lastName": "Doe",
      "role": {
        "name": "Employee",
        "permissions": [
          "view_public",
          "edit_profile",
          "view_employees"
        ]
      }
    }
  ],
 "validation": {
    "step1": {
      "success": {
        "status": "success",
        "message": "Personal information validated successfully"
      },
      "error": {
        "status": "error",
        "message": "Email already exists",
        "field": "email"
      }
    },
    "step2": {
      "success": {
        "status": "success",
        "message": "Role assignment validated successfully"
      },
      "error": {
        "status": "error",
        "message": "Invalid department and role combination",
        "fields": [
          "department",
          "role"
        ]
      }
    },
    "step3": {
      "success": {
        "status": "success",
        "message": "System access credentials validated successfully"
      },
      "error": {
        "status": "error",
        "message": "Password does not meet strength requirements",
        "field": "password",
        "requirements": {
          "minLength": 8,
          "uppercase": true,
          "lowercase": true,
          "number": true,
          "special": true
        }
      }
    }
  }
}
```
</details>


#### Step 5: Run the Node JS Project
```
node server.js
```

#### Step 6: Test - List Users API 
```
http://localhost:5001/api/articles
```


