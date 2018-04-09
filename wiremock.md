- disable gzip when recording
  ```json
  {
    "priority": 10,
    "request": {
      "method": "ANY",
      "urlPattern": ".*"
    },
    "response": {
      "proxyBaseUrl" : "https://other.com",
      "additionalProxyRequestHeaders": {
        "Accept-Encoding": "identity"
      }
    }
  }
  ```
- disable gzip in response
  ```json
  {
    "response": {
  		"status": 200,
  		"headers": {
  			"Content-Encoding": "identity"
  		},
  		"jsonBody": {}
    }
  }
  ```
