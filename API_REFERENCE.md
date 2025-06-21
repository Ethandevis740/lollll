# Namal Nexus API Reference

## Base URL
```
Development: http://localhost:3001/api
Production: [Your production URL]/api
```

## Authentication
Currently using demo authentication. For production, implement JWT tokens.

**Demo Credentials:**
- Email: `demo@example.com`
- Password: `password`

---

## Alumni API

### Get All Alumni
```http
GET /api/alumni
```

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `graduationYear` | number | Filter by graduation year |
| `degree` | string | Filter by degree |
| `location` | string | Filter by location |
| `company` | string | Filter by company |
| `search` | string | Text search across name, company, position |
| `page` | number | Page number (default: 1) |
| `limit` | number | Items per page (default: 10) |
| `sortBy` | string | Sort field (default: 'createdAt') |
| `sortOrder` | string | 'asc' or 'desc' (default: 'desc') |

**Example Request:**
```bash
curl "http://localhost:3001/api/alumni?graduationYear=2022&degree=Computer%20Science&page=1&limit=5"
```

**Response:**
```json
{
  "success": true,
  "count": 5,
  "total": 25,
  "page": 1,
  "totalPages": 5,
  "hasNextPage": true,
  "hasPrevPage": false,
  "data": [
    {
      "_id": "64a1b2c3d4e5f6789012345",
      "name": "Ahmed Hassan",
      "email": "ahmed.hassan@namal.edu.pk",
      "graduationYear": 2022,
      "degree": "Computer Science",
      "currentPosition": "Software Engineer",
      "company": "TechCorp",
      "location": "Islamabad, Pakistan",
      "skills": ["JavaScript", "React", "Node.js"],
      "profileCompletion": 85,
      "yearsSinceGraduation": 3,
      "createdAt": "2024-01-15T10:30:00.000Z",
      "updatedAt": "2024-01-15T10:30:00.000Z"
    }
  ]
}
```

### Get Alumni by ID
```http
GET /api/alumni/:id
```

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | string | Alumni ObjectId |

**Response:**
```json
{
  "success": true,
  "data": {
    "_id": "64a1b2c3d4e5f6789012345",
    "name": "Ahmed Hassan",
    "email": "ahmed.hassan@namal.edu.pk",
    "graduationYear": 2022,
    "degree": "Computer Science",
    "currentPosition": "Software Engineer",
    "company": "TechCorp",
    "location": "Islamabad, Pakistan",
    "skills": ["JavaScript", "React", "Node.js"],
    "socialLinks": {
      "linkedin": "https://linkedin.com/in/ahmed-hassan",
      "github": "https://github.com/ahmed-hassan"
    },
    "bio": "Passionate software engineer with 3 years of experience...",
    "profileCompletion": 95,
    "yearsSinceGraduation": 3
  }
}
```

### Create Alumni
```http
POST /api/alumni
```

**Request Body:**
```json
{
  "name": "Sara Ahmed",
  "email": "sara.ahmed@namal.edu.pk",
  "graduationYear": 2023,
  "degree": "Computer Science",
  "currentPosition": "Data Scientist",
  "company": "DataCorp",
  "location": "Lahore, Pakistan",
  "skills": ["Python", "Machine Learning", "Data Analysis"],
  "bio": "Data scientist passionate about AI and machine learning",
  "socialLinks": {
    "linkedin": "https://linkedin.com/in/sara-ahmed",
    "github": "https://github.com/sara-ahmed"
  }
}
```

**Response:**
```json
{
  "success": true,
  "message": "Alumni created successfully",
  "data": {
    "_id": "64a1b2c3d4e5f6789012346",
    "name": "Sara Ahmed",
    "email": "sara.ahmed@namal.edu.pk",
    // ... other fields
    "createdAt": "2024-01-15T11:00:00.000Z",
    "updatedAt": "2024-01-15T11:00:00.000Z"
  }
}
```

### Update Alumni
```http
PUT /api/alumni/:id
```

**Request Body:** (partial update supported)
```json
{
  "currentPosition": "Senior Data Scientist",
  "company": "AI Solutions Inc",
  "skills": ["Python", "Machine Learning", "Deep Learning", "TensorFlow"]
}
```

### Delete Alumni
```http
DELETE /api/alumni/:id
```

**Response:**
```json
{
  "success": true,
  "message": "Alumni deleted successfully"
}
```

### Get Alumni Statistics
```http
GET /api/alumni/stats
```

**Response:**
```json
{
  "success": true,
  "data": {
    "overview": {
      "totalAlumni": 150,
      "avgGraduationYear": 2020.5
    },
    "byDegree": [
      {
        "_id": "Computer Science",
        "count": 45
      },
      {
        "_id": "Business Administration",
        "count": 30
      }
    ],
    "byYear": [
      {
        "_id": 2023,
        "count": 25
      },
      {
        "_id": 2022,
        "count": 30
      }
    ]
  }
}
```

---

## Jobs API

### Get All Jobs
```http
GET /api/jobs
```

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `category` | string | Job category |
| `jobType` | string | Employment type |
| `experienceLevel` | string | Required experience level |
| `location` | string | Job location |
| `search` | string | Text search |
| `page` | number | Page number |
| `limit` | number | Items per page |

**Valid Values:**
- `category`: Technology, Engineering, Business, Marketing, Finance, Healthcare, Education, Design, Sales, Other
- `jobType`: Full-time, Part-time, Contract, Internship, Remote
- `experienceLevel`: Entry Level, Mid Level, Senior Level, Executive

**Response:**
```json
{
  "success": true,
  "count": 10,
  "total": 50,
  "data": [
    {
      "_id": "64a1b2c3d4e5f6789012347",
      "title": "Full Stack Developer",
      "company": "TechCorp",
      "location": "Islamabad, Pakistan",
      "description": "We are looking for an experienced full stack developer...",
      "jobType": "Full-time",
      "experienceLevel": "Mid Level",
      "category": "Technology",
      "salary": {
        "min": 80000,
        "max": 120000,
        "currency": "PKR"
      },
      "postedBy": {
        "_id": "64a1b2c3d4e5f6789012345",
        "name": "Ahmed Hassan",
        "email": "ahmed.hassan@namal.edu.pk",
        "company": "TechCorp"
      },
      "applicationEmail": "hr@techcorp.com",
      "views": 45,
      "applications": 12,
      "daysSincePosted": 5,
      "createdAt": "2024-01-10T09:00:00.000Z"
    }
  ]
}
```

### Get Job by ID
```http
GET /api/jobs/:id
```

### Create Job
```http
POST /api/jobs
```

**Request Body:**
```json
{
  "title": "Software Engineer",
  "company": "Tech Solutions",
  "location": "Remote",
  "description": "We are seeking a talented software engineer to join our growing team...",
  "requirements": [
    "Bachelor's degree in Computer Science or related field",
    "3+ years of experience with JavaScript",
    "Experience with React and Node.js",
    "Strong problem-solving skills"
  ],
  "jobType": "Full-time",
  "experienceLevel": "Mid Level",
  "category": "Technology",
  "postedBy": "64a1b2c3d4e5f6789012345",
  "applicationEmail": "careers@techsolutions.com",
  "applicationUrl": "https://techsolutions.com/careers/software-engineer",
  "salary": {
    "min": 90000,
    "max": 130000,
    "currency": "PKR"
  },
  "skills": ["JavaScript", "React", "Node.js", "MongoDB"],
  "benefits": ["Health Insurance", "Remote Work", "Flexible Hours"],
  "applicationDeadline": "2024-02-15T23:59:59.000Z"
}
```

### Update Job
```http
PUT /api/jobs/:id
```

### Delete Job
```http
DELETE /api/jobs/:id
```

### Get Job Statistics
```http
GET /api/jobs/stats
```

**Response:**
```json
{
  "success": true,
  "data": {
    "byCategory": [
      {
        "_id": "Technology",
        "count": 25,
        "avgViews": 45.5,
        "totalApplications": 150,
        "avgMinSalary": 75000,
        "avgMaxSalary": 110000
      }
    ],
    "byJobType": [
      {
        "_id": "Full-time",
        "count": 40
      }
    ],
    "byExperience": [
      {
        "_id": "Mid Level",
        "count": 20
      }
    ],
    "recentJobs": 15,
    "totalActiveJobs": 50
  }
}
```

---

## Events API

### Get All Events
```http
GET /api/events
```

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `category` | string | Event category |
| `upcoming` | boolean | Show only upcoming events |
| `featured` | boolean | Show only featured events |
| `eventType` | string | Event type |
| `search` | string | Text search |

**Valid Values:**
- `category`: networking, career, social, educational, sports, cultural, other
- `eventType`: in-person, virtual, hybrid

**Response:**
```json
{
  "success": true,
  "count": 5,
  "data": [
    {
      "_id": "64a1b2c3d4e5f6789012348",
      "title": "Alumni Networking Night",
      "description": "Join us for an evening of networking and reconnecting...",
      "date": "2024-02-15T18:00:00.000Z",
      "time": "18:00",
      "location": "Namal University Campus",
      "category": "networking",
      "maxAttendees": 100,
      "currentAttendees": 45,
      "availableSpots": 55,
      "organizer": "Alumni Association",
      "organizerContact": {
        "email": "alumni@namal.edu.pk",
        "phone": "+92-300-1234567"
      },
      "eventType": "in-person",
      "isFeatured": true,
      "isRegistrationOpen": true,
      "eventStatus": "open",
      "createdAt": "2024-01-01T10:00:00.000Z"
    }
  ]
}
```

### Get Event by ID
```http
GET /api/events/:id
```

**Response includes attendee information:**
```json
{
  "success": true,
  "data": {
    "_id": "64a1b2c3d4e5f6789012348",
    "title": "Alumni Networking Night",
    // ... other fields
    "attendees": [
      {
        "_id": "64a1b2c3d4e5f6789012349",
        "alumni": {
          "_id": "64a1b2c3d4e5f6789012345",
          "name": "Ahmed Hassan",
          "email": "ahmed.hassan@namal.edu.pk",
          "profileImage": "https://via.placeholder.com/150"
        },
        "registeredAt": "2024-01-10T14:30:00.000Z",
        "status": "registered"
      }
    ]
  }
}
```

### Create Event
```http
POST /api/events
```

**Request Body:**
```json
{
  "title": "Career Development Workshop",
  "description": "Learn essential skills for career advancement from industry experts...",
  "date": "2024-03-20T14:00:00.000Z",
  "time": "14:00",
  "location": "Virtual Event",
  "category": "career",
  "maxAttendees": 50,
  "organizer": "Career Services",
  "organizerContact": {
    "email": "careers@namal.edu.pk",
    "phone": "+92-300-7654321"
  },
  "registrationDeadline": "2024-03-18T23:59:59.000Z",
  "eventType": "virtual",
  "virtualLink": "https://zoom.us/j/123456789",
  "tags": ["career", "professional development", "workshop"],
  "isFeatured": false
}
```

### Update Event
```http
PUT /api/events/:id
```

### Delete Event
```http
DELETE /api/events/:id
```

### Register for Event
```http
POST /api/events/:id/register
```

**Request Body:**
```json
{
  "alumniId": "64a1b2c3d4e5f6789012345"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Successfully registered for event",
  "data": {
    "eventId": "64a1b2c3d4e5f6789012348",
    "currentAttendees": 46,
    "availableSpots": 54
  }
}
```

### Get Event Statistics
```http
GET /api/events/stats
```

**Response:**
```json
{
  "success": true,
  "data": {
    "byCategory": [
      {
        "_id": "networking",
        "count": 8,
        "avgAttendees": 45.5,
        "totalCapacity": 800,
        "totalAttendees": 364
      }
    ],
    "upcomingEvents": 12,
    "featuredEvents": 3,
    "totalActiveEvents": 25
  }
}
```

---

## Error Responses

### Validation Error
```json
{
  "success": false,
  "message": "Validation failed",
  "errors": [
    "Name is required",
    "Invalid email format"
  ]
}
```

### Not Found Error
```json
{
  "success": false,
  "message": "Alumni not found"
}
```

### Server Error
```json
{
  "success": false,
  "error": "Internal Server Error"
}
```

### Invalid ID Format
```json
{
  "success": false,
  "message": "Invalid alumni ID format"
}
```

---

## Rate Limiting
Currently no rate limiting implemented. For production, consider implementing rate limiting middleware.

## CORS
CORS is enabled for:
- `http://localhost:3000` (React dev server)
- `http://localhost:5173` (Vite dev server)

## Health Check
```http
GET /api/health
```

**Response:**
```json
{
  "success": true,
  "message": "Namal Nexus API is running successfully",
  "timestamp": "2024-01-15T12:00:00.000Z",
  "database": "Connected to MongoDB",
  "endpoints": {
    "alumni": "/api/alumni",
    "jobs": "/api/jobs",
    "events": "/api/events"
  },
  "version": "2.0.0"
}
```

---

## Testing with cURL

### Create Alumni
```bash
curl -X POST http://localhost:3001/api/alumni \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Test User",
    "email": "test@namal.edu.pk",
    "graduationYear": 2023,
    "degree": "Computer Science",
    "currentPosition": "Software Developer",
    "company": "Test Corp",
    "location": "Islamabad, Pakistan"
  }'
```

### Get Alumni with Filters
```bash
curl "http://localhost:3001/api/alumni?degree=Computer%20Science&graduationYear=2023&page=1&limit=5"
```

### Create Job
```bash
curl -X POST http://localhost:3001/api/jobs \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Software Engineer",
    "company": "Tech Corp",
    "location": "Remote",
    "description": "Looking for talented software engineer",
    "jobType": "Full-time",
    "experienceLevel": "Mid Level",
    "category": "Technology",
    "postedBy": "ALUMNI_ID_HERE",
    "applicationEmail": "hr@techcorp.com"
  }'
```

---

## Postman Collection

Import this collection into Postman for easy API testing:

```json
{
  "info": {
    "name": "Namal Nexus API",
    "description": "API collection for Namal Nexus Alumni Portal"
  },
  "variable": [
    {
      "key": "baseUrl",
      "value": "http://localhost:3001/api"
    }
  ],
  "item": [
    {
      "name": "Alumni",
      "item": [
        {
          "name": "Get All Alumni",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/alumni"
          }
        },
        {
          "name": "Create Alumni",
          "request": {
            "method": "POST",
            "url": "{{baseUrl}}/alumni",
            "header": [
              {
                "key": "Content-Type",
                "value": "application/json"
              }
            ],
            "body": {
              "mode": "raw",
              "raw": "{\n  \"name\": \"Test User\",\n  \"email\": \"test@namal.edu.pk\",\n  \"graduationYear\": 2023,\n  \"degree\": \"Computer Science\"\n}"
            }
          }
        }
      ]
    }
  ]
}
```