
# EXERCISE B: API REFERENCE ENTRY

## 1. API Title
Create a New Task in a Project Management Application

## 2. Endpoint Information

- HTTP Method: POST
- Endpoint Path: /api/v1/projects/{project_id}/tasks
- Description: This endpoint allows an authenticated user to create a new task inside a specific project.

## 3. Request Parameters

### Path Parameters

| Name | Data Type | Required | Description |
|---|---|---|---|
| project_id | Integer | Yes | The unique ID of the project where the task will be created. |

### Query Parameters

No query parameters are required.

### Request Body Parameters

| Name | Data Type | Required | Description |
|---|---|---|---|
| title | String | Yes | The title of the task. |
| description | String | No | Additional information about the task. |
| assignee_id | Integer | Yes | The ID of the user assigned to the task. |
| due_date | String (Date) | Yes | The deadline in YYYY-MM-DD format. |
| priority | String | Yes | The task priority: low, medium, or high. |

## 4. Required Request Headers

| Header | Value | Description |
|---|---|---|
| Authorization | Bearer <access_token> | Authenticates the user. |
| Content-Type | application/json | Indicates that the request body is JSON. |
| Accept | application/json | Requests a JSON response. |

## 5. Example Request

HTTP Method: POST

Endpoint:
`/api/v1/projects/101/tasks`

Request Body:

```json
{
  "title": "Prepare project report",
  "description": "Complete the monthly project progress report.",
  "assignee_id": 25,
  "due_date": "2026-12-15",
  "priority": "high"
}
```

## 6. Successful Response

### HTTP Status Code: 201 Created

Description: The task was successfully created.

Example Response Body:

```json
{
  "success": true,
  "message": "Task created successfully.",
  "data": {
    "task_id": 501,
    "project_id": 101,
    "title": "Prepare project report",
    "description": "Complete the monthly project progress report.",
    "assignee_id": 25,
    "due_date": "2026-12-15",
    "priority": "high",
    "status": "pending",
    "created_at": "2026-11-09T10:30:00Z"
  }
}
```

## 7. Possible HTTP Response Codes

| Status Code | Name | Explanation |
|---|---|---|
| 201 | Created | The task was created successfully. |
| 400 | Bad Request | The request contains invalid data. |
| 401 | Unauthorized | Authentication is missing or invalid. |
| 403 | Forbidden | The user does not have permission to create tasks in this project. |
| 404 | Not Found | The specified project or assignee does not exist. |
| 409 | Conflict | The request conflicts with the current project or task rules. |
| 415 | Unsupported Media Type | The request does not use application/json. |
| 422 | Unprocessable Entity | The request data fails validation, such as an invalid priority or date. |
| 500 | Internal Server Error | An unexpected server error occurred. |

## 8. Validation Rules

- The title must not be empty.
- The description is optional.
- The assignee ID must belong to an existing user.
- The due date must use YYYY-MM-DD format.
- The priority must be low, medium, or high.
- The user must be authenticated and authorized to create tasks in the project.

## 9. Conclusion

This API endpoint allows authenticated users to create tasks within a project management application. It supports task titles, descriptions, assignees, due dates, and priority levels. Clear request validation and appropriate HTTP response codes help developers use the endpoint correctly.
