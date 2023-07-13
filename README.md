# Testing-the-Trello-REST-API-using-Postman
- Trello's REST API testing (CRUD the `Board` and its `Components`)
- Once the test is executed, it will <strong>automatically</strong> perform the CRUD (Create, Read, Update, and Delete) operations step by step in the following order (test schedule included in the section below).

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

