# API Specification: [FEATURE_NAME]

## API Overview
*High-level description of API endpoints and their purpose*

### Base Configuration
- **Base URL**: `/api/v1`
- **Content Type**: `application/json`
- **Authentication**: [Method, e.g., Bearer token, API key]
- **Rate Limiting**: [Limits, e.g., 1000 requests/hour per user]

## Type Definitions

### Request/Response Interfaces
```typescript
// Core entity types
interface [EntityName] {
  id: string;
  [field]: [type];
  [field]: [type];
  created_at: string;
  updated_at: string;
}

// Request types
interface Create[EntityName]Request {
  [field]: [type];
  [field]: [type];
}

interface Update[EntityName]Request {
  [field]?: [type]; // Optional for partial updates
  [field]?: [type];
}

// Response types
interface [EntityName]Response {
  id: string;
  [field]: [type];
  [field]: [type];
  created_at: string;
  updated_at: string;
}

interface [EntityName]ListResponse {
  data: [EntityName]Response[];
  pagination: PaginationMeta;
  total: number;
}

// Common types
interface PaginationMeta {
  page: number;
  per_page: number;
  total_pages: number;
  has_next: boolean;
  has_prev: boolean;
}

interface ErrorResponse {
  error: {
    code: string;
    message: string;
    details?: Record<string, string>;
  };
}
```

## Endpoint Specifications

### [Resource] Endpoints

#### Create [Resource]
```
POST /api/v1/[resources]
```

**Purpose**: [What this endpoint does]

**Authentication**: [Required/Optional]

**Request Schema**:
```typescript
interface Request {
  [field]: [type]; // [Description, validation rules]
  [field]: [type]; // [Description, validation rules]
}
```

**Request Example**:
```json
{
  "[field]": "[example_value]",
  "[field]": "[example_value]"
}
```

**Success Response** (201 Created):
```typescript
interface Response {
  id: string;
  [field]: [type];
  [field]: [type];
  created_at: string;
  updated_at: string;
}
```

**Response Example**:
```json
{
  "id": "123e4567-e89b-12d3-a456-426614174000",
  "[field]": "[value]",
  "[field]": "[value]",
  "created_at": "2024-01-15T10:30:00Z",
  "updated_at": "2024-01-15T10:30:00Z"
}
```

**Error Responses**:
- `400 Bad Request`: Invalid request data
- `401 Unauthorized`: Authentication required
- `409 Conflict`: [Resource already exists or business rule violation]
- `422 Unprocessable Entity`: Validation errors

#### Get [Resource]
```
GET /api/v1/[resources]/{id}
```

**Purpose**: [What this endpoint does]

**Authentication**: [Required/Optional]

**Path Parameters**:
- `id` (string, required): [Resource identifier]

**Success Response** (200 OK):
```typescript
interface Response {
  id: string;
  [field]: [type];
  [field]: [type];
  created_at: string;
  updated_at: string;
}
```

**Error Responses**:
- `401 Unauthorized`: Authentication required
- `403 Forbidden`: Access denied
- `404 Not Found`: Resource not found

#### List [Resources]
```
GET /api/v1/[resources]
```

**Purpose**: [What this endpoint does]

**Authentication**: [Required/Optional]

**Query Parameters**:
- `page` (integer, optional): Page number (default: 1)
- `per_page` (integer, optional): Items per page (default: 20, max: 100)
- `filter[field]` (string, optional): [Filter description]
- `sort` (string, optional): Sort field (default: created_at)
- `order` (string, optional): Sort order (asc/desc, default: desc)

**Success Response** (200 OK):
```typescript
interface Response {
  data: [EntityName]Response[];
  pagination: PaginationMeta;
  total: number;
}
```

**Error Responses**:
- `401 Unauthorized`: Authentication required
- `400 Bad Request`: Invalid query parameters

#### Update [Resource]
```
PUT /api/v1/[resources]/{id}
```

**Purpose**: [What this endpoint does]

**Authentication**: [Required/Optional]

**Path Parameters**:
- `id` (string, required): [Resource identifier]

**Request Schema**:
```typescript
interface Request {
  [field]?: [type]; // [Optional for partial updates]
  [field]?: [type]; // [Validation rules]
}
```

**Success Response** (200 OK):
```typescript
interface Response {
  id: string;
  [field]: [type];
  [field]: [type];
  created_at: string;
  updated_at: string;
}
```

**Error Responses**:
- `400 Bad Request`: Invalid request data
- `401 Unauthorized`: Authentication required
- `403 Forbidden`: Access denied
- `404 Not Found`: Resource not found
- `422 Unprocessable Entity`: Validation errors

#### Delete [Resource]
```
DELETE /api/v1/[resources]/{id}
```

**Purpose**: [What this endpoint does]

**Authentication**: [Required/Optional]

**Path Parameters**:
- `id` (string, required): [Resource identifier]

**Success Response** (204 No Content):
No response body

**Error Responses**:
- `401 Unauthorized`: Authentication required
- `403 Forbidden`: Access denied
- `404 Not Found`: Resource not found
- `409 Conflict`: [Cannot delete due to dependencies]

## Authentication & Authorization

### Authentication Methods
- **Bearer Token**: `Authorization: Bearer {token}`
- **API Key**: `X-API-Key: {key}` (if applicable)

### Authorization Levels
- **Public**: No authentication required
- **User**: Authenticated user access
- **Admin**: Administrative privileges required

### Permission Matrix
| Endpoint | Public | User | Admin |
|----------|--------|------|-------|
| GET /[resources] | ❌ | ✅ | ✅ |
| GET /[resources]/{id} | ❌ | ✅ (own) | ✅ |
| POST /[resources] | ❌ | ✅ | ✅ |
| PUT /[resources]/{id} | ❌ | ✅ (own) | ✅ |
| DELETE /[resources]/{id} | ❌ | ❌ | ✅ |

## Error Handling

### Error Response Format
```typescript
interface ErrorResponse {
  error: {
    code: string;           // Machine-readable error code
    message: string;        // Human-readable error message
    details?: Record<string, string>; // Field-specific errors
  };
}
```

### Error Codes
- `INVALID_REQUEST`: Malformed request
- `VALIDATION_FAILED`: Field validation errors
- `RESOURCE_NOT_FOUND`: Requested resource does not exist
- `DUPLICATE_RESOURCE`: Resource already exists
- `UNAUTHORIZED`: Authentication required
- `FORBIDDEN`: Access denied
- `RATE_LIMITED`: Request rate limit exceeded
- `INTERNAL_ERROR`: Server error

### Validation Error Example
```json
{
  "error": {
    "code": "VALIDATION_FAILED",
    "message": "Request validation failed",
    "details": {
      "email": "Email format is invalid",
      "name": "Name is required"
    }
  }
}
```

## Rate Limiting

### Limits
- **Authenticated users**: 1000 requests/hour
- **Unauthenticated**: 100 requests/hour
- **Burst limit**: 10 requests/second

### Headers
```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1642680000
```

## Testing Strategy

### Contract Tests
Each endpoint requires failing contract tests that validate:
- Request/response schema compliance
- HTTP status codes
- Error response formats
- Authentication/authorization behavior

### Test File Mapping
- `POST /api/v1/[resources]` → `tests/contract/test_[resources]_post.py`
- `GET /api/v1/[resources]/{id}` → `tests/contract/test_[resources]_get.py`
- `GET /api/v1/[resources]` → `tests/contract/test_[resources]_list.py`
- `PUT /api/v1/[resources]/{id}` → `tests/contract/test_[resources]_put.py`
- `DELETE /api/v1/[resources]/{id}` → `tests/contract/test_[resources]_delete.py`

## Observability

### Logging Points
- Request/response logging with correlation IDs
- Authentication/authorization events
- Validation failures
- Performance metrics (response times)

### Metrics
- Request count by endpoint
- Response time distribution
- Error rate by endpoint and type
- Authentication success/failure rates

---

Based on PINDEX Constitution v1.0.0