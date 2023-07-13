# Testing-the-Trello-REST-API-using-Postman
- Trello's REST API testing (CRUD the `Board` and its `Components`)
- Once the test is executed, it will <strong>automatically</strong> perform the CRUD (Create, Read, Update, and Delete) operations step by step in the following order ([test schedule](https://github.com/thianrawichS/Testing-the-Trello-REST-API-using-Postman#test-execution-schedule) included in the section below).

## Purpose
``` Functionality Testing ```
- Ensure that the basic CRUD operations for boards and their components (e.g. list, card, checklist, and checkitem) are functioning correctly.
  - Creating, reading, updating, and deleting work as expected.

``` Basic Performance Testing ```
- Ensure that the reponse times of each operation is less than 3 seconds.



## Test Case / Execution list
### Test Case
| Category  | Request          | Dependency        | Priority |
|-----------|------------------|-------------------|----------|
| Board     | Create Board     | none              | High     |
| Board     | Update Board     | Create Board      | Medium   |
| Board     | Read Board       | Create Board      | Low      |
| Board     | Delete Board     | Create Board      | High     |
| List      | Create List      | Create Board      | High     |
| List      | Update List      | Create List       | Medium   |
| List      | Read List        | Create List       | Low      |
| List      | Delete List      | Create List       | High     |
| Card      | Create Card      | Create List       | High     |
| Card      | Update Card      | Create Card       | Medium   |
| Card      | Read Card        | Create Card       | Low      |
| Card      | Delete Card      | Create Card       | High     |
| Checklist | Create Checklist | Create Card       | High     |
| Checklist | Update Checklist | Create Checklist  | Medium   |
| Checklist | Read Checklist   | Create Checklist  | Low      |
| Checklist | Delete Checklist | Create Checklist  | High     |
| Checkitem | Create Checkitem | Create Checklist  | High     |
| Checkitem | Read Checkitem   | Create Checkitem  | Low      |
| Checkitem | Delete Checkitem | Create Checkitem  | High     |

### Test Execution Schedule
| Step | Description       |
|------|-------------------|
| 1    | Create Board      |
| 2    | Create List       |
| 3    | Create Card       |
| 4    | Create Checklist  |
| 5    | Create Checkitem  |
| 6    | Update Board      |
| 7    | Update List       |
| 8    | Update Card       |
| 9    | Update Checklist  |
| 10   | Read Board        |
| 11   | Read List         |
| 12   | Read Card         |
| 13   | Read Checklist    |
| 14   | Read Checkitem    |
| 15   | Delete Checkitem  |
| 16   | Delete Checklist  |
| 17   | Delete Card       |
| 18   | Delete List       |
| 19   | Delete Board      |

## Test Procedure
- To perform the same test, import the attached `Trello API.postman_collection.json` in the postman.
- Create Environments
- Add the Variable to Environments
  - <b><i>api_key</i></b> : Trello api key
  - <b><i>token</i></b> : Trello authorization token

Both can get at [trello.com/power-ups/admin](https://trello.com/power-ups/admin)
- Other Variable will create once you run the collection (created by script in the "Pre-request Script" section)

## Sample Testing Preview
### Create board
  ```
  request: POST
  url: 'https://api.trello.com/1/boards/?name={{boardName}}&key={{api_key}}&token={{token}}'
  ```
  #### Query Parameters
  | Key | Value |
  |-----|-------|
  | name| {{boardName}}|
  | key | {{api_key}} |
  | token | {{token}} |
  #### Pre-request Script
  ```jsx
  // set boardName's value to "testingBoard"
  pm.environment.set("boardName", "testingBoard")
  ```
  #### Test Script
  ```jsx
  var jsonData = pm.response.json();

  // set board id
  pm.environment.set("boardId", jsonData.id);

  // test
  pm.test("Create board successfully (Status 200)", () => {
      pm.expect(pm.response.code).to.eql(200)
  });
  
  pm.test("Board name is correct", () => {
      pm.expect(jsonData.name).to.eql(pm.environment.get("boardName"))
  });
  ```

***

### Get/Read a board

  ```
  request: GET
  url: 'https://api.trello.com/1/boards/{{boardId}}?key={{api_key}}&token={{token}}'
  ```
  #### Query Parameters
  | Key | Value |
  |-----|-------|
  |key| {{api_key}}|
  |token|{{token}}|
  #### Test Script
  ```jsx
  pm.test("Get a board successfully", () => {
    pm.response.to.have.status(200)
  });
  ```

***

### Update board
  ```
  request: PUT
  url: 'https://api.trello.com/1/boards/{{boardId}}?key={{api_key}}&token={{token}}&name={{newBoardName}}&desc={{boardDescription}}'
  ```
  #### Query Parameters
  | Key | Value |
  |-----|-------|
  |key| {{api_key}}|
  |token|{{token}}|
  |name|{{newBoardName}}|
  |desc|{{boardDescription}}|
  #### Pre-request Script
  ```jsx
  // set newBoardName's value to "updatedTestingBoard"
  pm.environment.set("newBoardName", "updatedTestingBoard");

  // set boardDescription
  pm.environment.set("boardDescription", "This is a board description");
  ```
  #### Test Script
  ```jsx
  var jsonData = pm.response.json();

  // test
  pm.test("Update board successfully", () => {
    pm.response.to.have.status(200)
  });

  pm.test("Board name changed correctly", () => {
      pm.expect(jsonData.name).to.eql(pm.environment.get("newBoardName"))
  });
  
  pm.test("Board description has been added", () => {
      pm.expect(jsonData.desc).to.exist
  });
  ```

  ***

### Delete board
  ```
  request: DELETE
  url: 'https://api.trello.com/1/boards/{{boardId}}?key={{api_key}}&token={{token}}'
  ```
  #### Query Parameters
  | Key | Value |
  |-----|-------|
  |key| {{api_key}}|
  |token|{{token}}|
  #### Test Script
  ```jsx
  pm.test("Delete board successfully (Status 200)", () => {
    pm.expect(pm.response.code).to.eql(200)
  })
  ```
  ***
  #### Next step
  - Once you finished create all 4 requests, next thing is to run a collection (Select a Collections > Run collection)
    <img src="https://github.com/thianrawichS/Testing-the-Trello-REST-API-using-Postman/blob/main/Screenshot%201.png" alt="run-collection">
  - You can choose to run manually or schedule runs(run collection at a specified time)

  `Run/Test Summary` <br>
  <br>
  <img src="https://github.com/thianrawichS/Testing-the-Trello-REST-API-using-Postman/blob/main/Screenshot%202.png" alt="summary1"><br>
  <img src="https://github.com/thianrawichS/Testing-the-Trello-REST-API-using-Postman/blob/main/Screenshot%203.png" alt="summary2">
    
  
