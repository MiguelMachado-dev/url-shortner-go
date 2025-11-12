# URL Shortener API

A simple URL shortener API built with Go and the Chi router. This is a proof of concept that demonstrates basic URL shortening functionality with in-memory storage.

## Features

- 🔗 Create short URLs from long URLs
- ⚡ Fast redirects using short codes
- 📝 JSON API responses
- 🗃️ In-memory storage (for demo purposes)
- 📊 Structured logging
- 🛡️ Error handling and validation

## Tech Stack

- **Go 1.25.4** - Programming language
- **Chi v5** - HTTP router
- **In-memory map** - Data storage

## Quick Start

### Prerequisites

- Go 1.25.4 or higher installed

### Installation

1. Clone the repository:
```bash
git clone https://github.com/MiguelMachado-dev/url-shortner.git
cd url-shortner
```

2. Install dependencies:
```bash
go mod tidy
```

3. Run the application:
```bash
go run .
```

The server will start on `http://localhost:8080`

## API Endpoints

### Create Short URL

**POST** `/api/shorten`

Creates a short URL from a provided long URL.

#### Request Body
```json
{
  "url": "https://example.com/very/long/url"
}
```

#### Response
```json
{
  "data": "AbCd1234"
}
```

#### Example
```bash
curl -X POST http://localhost:8080/api/shorten \
  -H "Content-Type: application/json" \
  -d '{"url": "https://example.com/very/long/url"}'
```

### Redirect to Original URL

**GET** `/{code}`

Redirects to the original URL associated with the short code.

#### Example
```bash
curl http://localhost:8080/AbCd1234
# Will redirect to the original URL
```

## Error Responses

All errors return JSON in the format:
```json
{
  "error": "error message"
}
```

### Common Errors

- **400 Bad Request** - Invalid URL format
- **422 Unprocessable Entity** - Invalid JSON body
- **404 Not Found** - Short code not found

## Development

### Project Structure

```
.
├── main.go          # Application entry point and server setup
├── api/
│   └── api.go       # HTTP handlers and routing logic
├── go.mod           # Go module file
├── go.sum           # Dependency checksums
└── README.md        # This file
```

### Running Locally

```bash
# Run the application
go run .

# Or build and run
go build -o url-shortner .
./url-shortner
```

## Limitations

This is a proof of concept with the following limitations:

- **In-memory storage**: Data is lost when the server restarts
- **No duplicate checking**: Multiple URLs could get the same short code
- **No rate limiting**: API is open to unlimited requests
- **No analytics**: No tracking of URL usage or statistics
- **No custom URLs**: Cannot specify custom short codes
- **No expiration**: URLs never expire

## Contributing

This is a simple proof of concept. Feel free to fork and extend it with additional features like:

- Database persistence
- Custom short codes
- URL analytics
- Rate limiting
- Authentication

## License

This project is open source and available under the [MIT License](LICENSE).