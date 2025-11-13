---
layout: default
title: InvokeRestMethod
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/utility/invokerestmethod/
---

# InvokeRestMethod

Executes HTTP REST API calls to interact with web services and APIs.

## Syntax

```jyro
InvokeRestMethod(url, method, headers, body)
```

## Parameters

- **url** (string, required): The URL to call
- **method** (string, optional): HTTP method - defaults to "GET"
- **headers** (object, optional): Request headers as key-value pairs
- **body** (any, optional): Request body - automatically JSON-serialized

## Returns

- **object**: Response object with the following properties:
  - **statusCode** (number): HTTP status code (e.g., 200, 404)
  - **statusDescription** (string): Status description (e.g., "OK", "Not Found")
  - **isSuccessStatusCode** (boolean): True if status code is 2xx
  - **content** (any): Response body - automatically parsed if JSON
  - **contentType** (string): Response content type
  - **headers** (object): Response headers as key-value pairs

## Description

The InvokeRestMethod function enables Jyro scripts to make HTTP requests to REST APIs. This is an opt-in feature that must be explicitly enabled via `.WithRestApi()` when building the Jyro execution context. The function automatically handles JSON serialization for request bodies and deserialization for JSON responses.

## Enabling REST API Support

REST API functionality must be explicitly enabled for security reasons:

```csharp
var result = JyroBuilder.Create()
    .WithScript(scriptSource)
    .WithData(data)
    .WithRestApi()  // Enable REST API functionality
    .Run();
```

## Examples

### Simple GET Request

```jyro
var response = InvokeRestMethod("https://api.example.com/users/1", "GET")
Data.user = response.content
Data.success = response.isSuccessStatusCode
```

### POST with JSON Body

```jyro
var newUser = {
    "name": "John Doe",
    "email": "john@example.com",
    "age": 30
}

var headers = {
    "Content-Type": "application/json",
    "Authorization": "Bearer token123"
}

var response = InvokeRestMethod(
    "https://api.example.com/users",
    "POST",
    headers,
    newUser
)

if response.isSuccessStatusCode then
    Data.newUserId = response.content.id
end
```

### Error Handling

```jyro
var response = InvokeRestMethod("https://api.example.com/data", "GET")

if response.statusCode == 200 then
    Data.result = response.content
else if response.statusCode == 404 then
    Data.error = "Resource not found"
else if response.statusCode == 401 then
    Data.error = "Unauthorized - check credentials"
else
    Data.error = "Request failed: " + response.statusDescription
end
```

### PUT and DELETE Requests

```jyro
# Update existing resource
var updateData = {
    "status": "completed",
    "completedAt": Now()
}

var putResponse = InvokeRestMethod(
    "https://api.example.com/tasks/" + Data.taskId,
    "PUT",
    { "Content-Type": "application/json" },
    updateData
)

# Delete resource
var deleteResponse = InvokeRestMethod(
    "https://api.example.com/items/" + Data.itemId,
    "DELETE",
    { "Authorization": "Bearer " + Data.token }
)
```

### Working with Response Headers

```jyro
var response = InvokeRestMethod("https://api.example.com/data", "GET")

# Access specific headers
Data.rateLimit = response.headers["X-RateLimit-Remaining"]
Data.etag = response.headers["ETag"]

# Check content type
if response.contentType == "application/json" then
    Data.result = response.content
end
```

## Security Configuration

REST API functionality includes comprehensive security controls that should be configured based on your use case:

### Default Configuration

```csharp
// Uses safe defaults
var result = JyroBuilder.Create()
    .WithScript(script)
    .WithData(data)
    .WithRestApi()
    .Run();
```

**Default Limits:**
- Max request body: 1 MB
- Max response size: 10 MB
- Concurrent requests: 5
- Request timeout: 30 seconds
- Allowed methods: GET, POST, PUT, PATCH, DELETE
- URL filtering: None (all URLs allowed)

### Custom Security Configuration

```csharp
var restOptions = new RestApiOptions
{
    // Only allow specific domains
    AllowedUrlPatterns = new List<Regex>
    {
        new Regex(@"^https://api\.example\.com/", RegexOptions.IgnoreCase)
    },

    // Block sensitive endpoints
    DeniedUrlPatterns = new List<Regex>
    {
        new Regex(@"/admin/", RegexOptions.IgnoreCase)
    },

    // Limit sizes
    MaxRequestBodySize = 512_000,    // 500 KB
    MaxResponseSize = 5_242_880,     // 5 MB

    // Restrict methods
    AllowedHttpMethods = new HashSet<string> { "GET", "POST" },

    // Set timeout
    RequestTimeout = TimeSpan.FromSeconds(15)
};

var result = JyroBuilder.Create()
    .WithScript(script)
    .WithData(data)
    .WithRestApi(restOptions)
    .Run();
```

### Pre-configured Security Profiles

#### Local Development

```csharp
// Allows only localhost and local network addresses
var result = JyroBuilder.Create()
    .WithScript(script)
    .WithData(data)
    .WithRestApi(RestApiOptions.CreateForLocalDevelopment())
    .Run();
```

#### Production with SSRF Protection

```csharp
// Blocks all private/internal network access
var result = JyroBuilder.Create()
    .WithScript(script)
    .WithData(data)
    .WithRestApi(RestApiOptions.CreateWithPrivateNetworkBlocking())
    .Run();
```

## REST API Security for Untrusted Scripts

When enabling REST API functionality for untrusted client scripts, several critical security considerations must be addressed to prevent malicious actors from exploiting the system. The REST API feature provides powerful capabilities that, if left unconstrained, could be weaponized to compromise security, exfiltrate data, or attack internal infrastructure.

### Server-Side Request Forgery (SSRF) Risks

The primary security concern when allowing untrusted scripts to make HTTP requests is Server-Side Request Forgery (SSRF). In an SSRF attack, malicious scripts leverage the host server's network access to reach internal services, cloud metadata endpoints, or other protected resources that would be inaccessible to the attacker directly. The host server often has privileged network access to internal systems, databases, and configuration services that external clients cannot reach. If untrusted scripts can control the destination URL without restrictions, they can effectively use the host as a proxy to access these protected resources.

Cloud environments are particularly vulnerable to SSRF attacks through metadata services. Major cloud providers expose instance metadata at well-known addresses such as `169.254.169.254` (AWS, Azure, GCP) and `metadata.google.internal`. These endpoints provide sensitive information including temporary security credentials, API keys, instance configuration, and user data. An attacker who can make the host server request these endpoints can extract credentials that grant broad access to the cloud account. Similarly, internal network services running on localhost or private IP ranges (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) are common targets, as they often lack authentication when accessed from trusted internal sources.

### URL Filtering and Access Control

To mitigate SSRF risks, strict URL filtering must be implemented through both allowlist and denylist mechanisms. The denylist should always take precedence over the allowlist, ensuring that explicitly forbidden URLs cannot be accessed even if they match an allowed pattern. Private network ranges, localhost addresses, link-local addresses (169.254.0.0/16), and cloud metadata endpoints must be systematically blocked. The denylist should be comprehensive and include IPv4, IPv6, and hostname variations of protected endpoints.

An allowlist approach provides the strongest security posture for production environments. When implemented, only URLs matching explicitly permitted patterns should be accessible, with all other requests denied by default. This prevents attackers from discovering and exploiting endpoints that were not anticipated during configuration. The allowlist should use precise regular expressions that match the exact domains and paths required for legitimate functionality, avoiding overly broad patterns that could be bypassed.

DNS rebinding attacks represent an advanced SSRF technique that can circumvent URL filtering. In these attacks, a malicious domain initially resolves to a safe public IP address to pass URL validation, then quickly changes its DNS record to point to an internal IP address. When the host server makes the actual HTTP request, it connects to the internal resource despite the URL appearing legitimate during validation. Protection against DNS rebinding requires validating the resolved IP address immediately before connection establishment, not just during initial URL parsing.

### HTTP Method and Header Restrictions

Limiting the available HTTP methods reduces the attack surface by preventing destructive operations. For read-only use cases, restricting access to GET requests prevents untrusted scripts from modifying data through POST, PUT, PATCH, or DELETE operations. Even when write operations are necessary, dangerous methods like CONNECT or TRACE should never be permitted, as they can be exploited for tunneling or information disclosure.

Request headers must be carefully controlled to prevent header injection attacks and credential leakage. Untrusted scripts should not be allowed to override security-critical headers such as `Host`, `Origin`, `Referer`, or authentication headers unless specifically required. If authentication is necessary, credentials should be injected by the host application rather than being provided by untrusted scripts. This prevents scripts from accessing credentials or impersonating other users. Custom headers should be validated to ensure they do not contain newline characters or other control sequences that could enable header injection attacks.

### Resource Limits and Denial of Service Prevention

Resource limits are essential to prevent denial of service attacks through resource exhaustion. Request body size limits prevent attackers from consuming excessive memory or bandwidth by uploading large payloads. Similarly, response size limits protect against memory exhaustion when receiving large responses, either from legitimate services returning unexpectedly large datasets or from malicious endpoints designed to overwhelm the host.

Concurrent request limits prevent scripts from opening excessive simultaneous connections that could exhaust network resources, file descriptors, or connection pools. Without such limits, a malicious script could launch hundreds or thousands of concurrent requests, degrading service performance or causing complete service outages. The timeout configuration must balance preventing indefinite blocking with allowing reasonable completion time for legitimate requests. Timeouts should be set conservatively, considering both the execution time limits of the overall script and the expected response times of accessed APIs.

### Data Exfiltration Risks

When untrusted scripts can make arbitrary HTTP requests, data exfiltration becomes a significant concern. Malicious scripts could extract sensitive data from the execution context and transmit it to attacker-controlled endpoints. The script has access to the Data object and any variables in scope, potentially including confidential business data, personally identifiable information, or system configuration details. This data can be encoded into URL parameters, request bodies, or custom headers and sent to external services.

To mitigate exfiltration risks, the allowlist approach should restrict outbound communication to only necessary and trusted domains. Logging and monitoring of all REST API calls should be implemented, including the destination URL, method, and response status. Anomalous patterns such as requests to unusual domains, high request volumes, or transfers of unusually large data payloads should trigger alerts. The principle of least privilege should guide what data is made available to scripts; sensitive information should be excluded from the execution context whenever possible.

### Content Type and Response Handling

Automatic content type handling introduces additional security considerations. The function automatically parses JSON responses into Jyro objects, which is convenient but could be exploited if the response contains malicious data structures. Extremely nested JSON objects or arrays could cause excessive memory usage or stack overflow during parsing. Response parsing should enforce reasonable depth limits and reject structures that exceed memory or complexity thresholds.

Non-JSON content types should be handled carefully, especially when scripts process binary data or HTML responses. If scripts can access raw response content, they might be able to extract sensitive information from error pages, debug output, or administrative interfaces that return HTML. Content type validation should ensure responses match expected formats, and unexpected content types should be logged or rejected based on security policy.

### Audit Logging and Monitoring

Comprehensive audit logging is critical for detecting and responding to security incidents. Every REST API invocation should be logged with sufficient detail to support forensic investigation, including timestamp, script identifier, destination URL, HTTP method, request size, response status, response size, and execution duration. These logs enable detection of suspicious patterns such as port scanning (sequential requests to different ports), credential stuffing (repeated authentication attempts), or data exfiltration (large response volumes to unusual domains).

Real-time monitoring should identify anomalous behavior and trigger alerts or automated responses. Rate limiting can be enforced at multiple levels: per-script, per-user, or globally across the system. Geographic restrictions might be appropriate for some use cases, blocking requests to IP addresses or domains in specific countries. Integration with security information and event management (SIEM) systems enables correlation of REST API activity with other security events across the infrastructure.

### Defense in Depth Strategy

A defense-in-depth approach layers multiple security controls to ensure that if one control fails, others remain effective. URL filtering should be combined with network-level controls such as firewall rules or network segmentation that prevent the host server from accessing sensitive internal resources. Even if a URL filtering bypass is discovered, network controls provide a secondary barrier.

The principle of least privilege should be applied to the host server's network access, service account permissions, and available system resources. The server should only have network connectivity to services required for legitimate operations. Service accounts should have minimal permissions, reducing the impact if credentials are compromised through SSRF or other attacks. Container isolation or sandboxing technologies can provide additional isolation between script execution and the underlying system.

Security policies should be regularly reviewed and updated as new attack vectors are discovered or application requirements change. Penetration testing and security audits should specifically target REST API functionality, attempting to bypass URL filters, exfiltrate data, or access internal services. Automated security scanning should be integrated into the development pipeline to detect misconfigurations or vulnerabilities before they reach production.

### Secure Configuration Examples

For production environments serving untrusted scripts, the following configuration template provides a strong security baseline:

```csharp
var productionRestOptions = new RestApiOptions
{
    // Strict allowlist - only specific trusted APIs
    AllowedUrlPatterns = new List<Regex>
    {
        new Regex(@"^https://api\.trustedpartner\.com/v1/public/",
                  RegexOptions.IgnoreCase | RegexOptions.Compiled)
    },

    // Comprehensive denylist - block all internal access
    DeniedUrlPatterns = new List<Regex>
    {
        // Localhost in all forms
        new Regex(@"^https?://localhost", RegexOptions.IgnoreCase),
        new Regex(@"^https?://127\.", RegexOptions.IgnoreCase),
        new Regex(@"^https?://\[::1\]", RegexOptions.IgnoreCase),

        // Private networks (RFC 1918)
        new Regex(@"^https?://10\.", RegexOptions.IgnoreCase),
        new Regex(@"^https?://172\.(1[6-9]|2[0-9]|3[01])\.", RegexOptions.IgnoreCase),
        new Regex(@"^https?://192\.168\.", RegexOptions.IgnoreCase),

        // Link-local addresses
        new Regex(@"^https?://169\.254\.", RegexOptions.IgnoreCase),

        // Cloud metadata services
        new Regex(@"^https?://169\.254\.169\.254", RegexOptions.IgnoreCase),
        new Regex(@"^https?://metadata\.google\.internal", RegexOptions.IgnoreCase),

        // Additional internal domains
        new Regex(@"\.internal$", RegexOptions.IgnoreCase),
        new Regex(@"\.local$", RegexOptions.IgnoreCase)
    },

    // Conservative resource limits
    MaxRequestBodySize = 100_000,        // 100 KB
    MaxResponseSize = 1_000_000,         // 1 MB
    MaxConcurrentRequests = 2,           // Minimal concurrency
    RequestTimeout = TimeSpan.FromSeconds(10),

    // Read-only access
    AllowedHttpMethods = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
    {
        "GET"
    },

    // Disable automatic redirects to prevent redirect-based bypasses
    AllowRedirects = false
};
```

This configuration enforces multiple layers of protection: strict allowlist limiting access to specific trusted endpoints, comprehensive denylist blocking all internal network access, conservative resource limits preventing abuse, read-only HTTP access, and disabled redirects preventing bypass techniques. Each control addresses specific attack vectors while maintaining functionality for legitimate use cases.

### Recommendations for Untrusted Script Environments

When deploying Jyro with REST API functionality in environments that execute untrusted scripts, the following practices should be implemented:

1. **Never enable REST API without explicit security configuration.** The default permissive settings are suitable only for trusted, controlled environments.

2. **Implement the most restrictive allowlist possible** that still meets functional requirements. Regularly review and audit the allowlist to ensure it remains minimal.

3. **Deploy comprehensive monitoring and alerting** for all REST API activity, with automated responses to suspicious patterns.

4. **Use network-level controls** as a secondary defense layer, ensuring the host server cannot access internal infrastructure even if URL filtering is bypassed.

5. **Regularly update deny patterns** to include newly discovered attack vectors, cloud provider changes, and internal infrastructure modifications.

6. **Implement rate limiting at multiple levels** to prevent abuse and resource exhaustion.

7. **Conduct regular security assessments** specifically targeting REST API functionality, including penetration testing and code review.

8. **Minimize data exposure** by limiting what information is available in the script execution context.

9. **Log and archive all REST API activity** for security monitoring, forensic investigation, and compliance requirements.

10. **Educate developers and administrators** about SSRF risks, proper configuration practices, and security monitoring procedures.

By implementing these security controls and following defense-in-depth principles, the risks associated with enabling REST API functionality for untrusted scripts can be substantially mitigated while preserving the valuable capabilities that REST API integration provides.

## Error Handling

REST API calls can fail for various reasons. The function handles errors gracefully and provides detailed error information:

### Runtime Exceptions

The following conditions will throw `JyroRuntimeException`:

- **Invalid URL format**: Malformed URLs that cannot be parsed
- **Unsupported protocol**: Non-HTTP/HTTPS protocols (e.g., FTP, file://)
- **Security policy violation**: URLs blocked by allow/deny lists
- **Method not allowed**: HTTP methods blocked by security policy
- **Size limit exceeded**: Request or response exceeds configured limits
- **Timeout**: Request exceeds timeout duration
- **Concurrent limit**: Maximum concurrent requests exceeded
- **Network errors**: Connection failures, DNS resolution errors

### HTTP Errors

HTTP error status codes (4xx, 5xx) do not throw exceptions. Instead, they are returned in the response object with `isSuccessStatusCode = false`. This allows scripts to handle different error conditions appropriately:

```jyro
var response = InvokeRestMethod("https://api.example.com/data", "GET")

# HTTP errors don't throw - check status
if response.statusCode >= 400 and response.statusCode < 500 then
    Data.error = "Client error: " + response.statusDescription
else if response.statusCode >= 500 then
    Data.error = "Server error: " + response.statusDescription
end
```

## Limitations

- Only HTTP and HTTPS protocols are supported
- Response bodies are read entirely into memory
- Multipart/form-data uploads are not supported
- Client certificates are not supported
- Custom SSL validation is not supported
- Automatic cookie handling is not implemented

## See Also

- [String Functions](/jyro/functions/stdlib/string/) - For working with response data
- [Object Functions](/jyro/functions/stdlib/utility/) - For working with JSON responses
- [Error Handling](/jyro/error-handling/) - For handling REST API errors
