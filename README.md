# Postman API Collections

A comprehensive collection of Postman API testing suites for various services and authentication flows.

## 📚 Collections Overview

This repository contains professionally crafted Postman collections that provide complete testing suites, documentation, and examples for:

### 🚇 [BART API Collection](https://documenter.getpostman.com/view/48949346/2sB3QFSCzL)

The Bay Area Rapid Transit (BART) API provides comprehensive access to BART service and station data.

**Features:**
- 🚉 **Station Data**: Access to all BART stations, schedules, and route information
- 📢 **Advisory Information API**: Real-time service advisories (BSA), elevator status messages
- 🚊 **System Data**: Current train count and system-wide information
- ⏱️ **Real-Time Updates**: Information updated every minute from BART's live system
- 🌐 **Complete Coverage**: All data available on the BART website accessible via API

**What You Can Do:**
- Get real-time departure information for any station
- Check current service advisories and disruptions
- Access elevator and escalator status updates
- Retrieve route maps and station details
- Monitor system-wide train counts and performance

**Use Cases:**
- Transit mobile applications
- Real-time service monitoring
- Integration with travel planning systems
- Accessibility applications (elevator status)
- Data analysis and reporting

---

### 🔐 [OAuth 2.0 Authentication Collection](https://documenter.getpostman.com/view/48949346/2sB3QFSCux)

A comprehensive guide to OAuth 2.0 authorization flows using real-world APIs (Spotify and PagerDuty).

**Authentication Flows Covered:**
- 🔑 **Client Credentials Flow**: Server-to-server authentication
- 🎫 **Authorization Code Flow**: Traditional web application flow
- ⚡ **Implicit Grant Flow**: Single-page applications (deprecated but documented)
- 🛡️ **Authentication with Token in Header**: Bearer token usage
- 🔒 **Authorization Code with PKCE**: Enhanced security for mobile/native apps

![OAuth 2.0 Roles](https://i.imgur.com/u59bK3B.png)

**Real-World Examples:**
- **Spotify API**: Music streaming service integration
- **PagerDuty API**: Incident management and alerting

**What You'll Learn:**
- How to implement each OAuth 2.0 flow correctly
- Security best practices for different application types
- Token management and refresh strategies
- Common pitfalls and how to avoid them
- Real API integration examples

**Use Cases:**
- Web application authentication
- Mobile app security implementation
- API integration development
- Security architecture planning
- OAuth 2.0 learning and training

---

## 🚀 Quick Start

### 1. **Import Collections**

Click on the collection links above and use the **"Run in Postman"** button to import directly into your Postman workspace.

Alternatively:
1. Download the collection JSON files from this repository
2. Open Postman
3. Click **Import** → **Upload Files**
4. Select the downloaded collection files

### 2. **Set Up Environment**

Import the environment files from the `environments/` directory and configure:

#### BART API Environment Variables:
```
bart_api_base_url = http://api.bart.gov/api
bart_api_key = MW9S-E7SL-26DU-VV8V  # Public demo key
```

#### OAuth 2.0 Environment Variables:
```
spotify_client_id = your_spotify_client_id
spotify_client_secret = your_spotify_client_secret
pagerduty_client_id = your_pagerduty_client_id
pagerduty_client_secret = your_pagerduty_client_secret
redirect_uri = your_configured_redirect_uri
```

### 3. **Test the APIs**

- **BART API**: Start with basic station information requests
- **OAuth 2.0**: Begin with the Client Credentials flow for simplicity

---

## 📁 Repository Structure

```
postman-api-collections/
├── README.md                    # This comprehensive guide
├── collections/                 # Postman collection JSON files
│   ├── bart-api.json           # BART API collection
│   └── oauth2-flows.json       # OAuth 2.0 collection
├── environments/               # Environment configuration files
│   ├── bart-api-env.json       # BART API environment
│   └── oauth2-env.json         # OAuth 2.0 environment
├── documentation/              # Additional documentation
│   ├── bart-api-guide.md       # BART API detailed guide
│   ├── oauth2-guide.md         # OAuth 2.0 implementation guide
│   └── troubleshooting.md      # Common issues and solutions
└── assets/                     # Images and diagrams
    ├── oauth-flow-diagram.png  # OAuth 2.0 flow visualizations
    └── bart-system-map.png     # BART system reference
```

---

## 🔧 Detailed Setup Guides

### BART API Setup

1. **API Key**: The BART API uses a public demo key included in the collection
2. **Base URL**: `http://api.bart.gov/api`
3. **Rate Limits**: No strict limits for the demo key
4. **Response Format**: XML (converted to JSON in collection tests)

**Example Request:**
```http
GET http://api.bart.gov/api/stn.aspx?cmd=stns&key=MW9S-E7SL-26DU-VV8V
```

### OAuth 2.0 Setup

1. **Register Applications**:
   - [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/)
   - [PagerDuty Developer Account](https://developer.pagerduty.com/)

2. **Configure Redirect URIs**:
   - For testing: `https://oauth.pstmn.io/v1/callback`
   - For production: Your application's callback URL

3. **Security Notes**:
   - Never commit real client secrets to repositories
   - Use environment variables for sensitive data
   - Implement proper token storage and refresh mechanisms

---

## 🧪 Testing Workflows

### BART API Testing Sequence

1. **System Information** → Get overall system status
2. **Station List** → Retrieve all stations
3. **Station Details** → Get specific station information
4. **Real-time Departures** → Check current departures
5. **Service Advisories** → Check for any service disruptions

### OAuth 2.0 Testing Sequence

1. **Client Credentials** → Simplest flow for server-to-server
2. **Authorization Code** → Most common web application flow
3. **PKCE Enhancement** → Secure mobile/native app flow
4. **Token Usage** → Using acquired tokens for API calls
5. **Token Refresh** → Maintaining session with refresh tokens

---

## 📊 Collection Features

### ✅ Automated Testing
- Pre-request scripts for dynamic data generation
- Test scripts for response validation
- Environment variable management
- Error handling and retry logic

### ✅ Documentation
- Detailed request descriptions
- Response schema documentation
- Example use cases
- Implementation notes

### ✅ Real-World Examples
- Production-ready code samples
- Best practices implementation
- Common integration patterns
- Security considerations

---

## 🔍 Advanced Usage

### Custom Scripts

Both collections include advanced Postman scripting:

```javascript
// Example: Dynamic timestamp generation
pm.environment.set("timestamp", new Date().getTime());

// Example: Token extraction and storage
const response = pm.response.json();
pm.environment.set("access_token", response.access_token);

// Example: Automated retry logic
if (pm.response.code === 429) {
    setTimeout(() => {}, 1000); // Wait and retry
}
```

### Integration Examples

```javascript
// Using BART API in web application
fetch('http://api.bart.gov/api/etd.aspx?cmd=etd&orig=MONT&key=MW9S-E7SL-26DU-VV8V')
  .then(response => response.text())
  .then(data => {
    // Process XML response
    console.log(data);
  });

// Using OAuth 2.0 tokens
fetch('https://api.spotify.com/v1/me', {
  headers: {
    'Authorization': `Bearer ${access_token}`
  }
})
.then(response => response.json())
.then(user => console.log(user));
```

---

## 🚨 Troubleshooting

### Common Issues

#### BART API
- **XML Responses**: BART API returns XML; use collection's built-in XML to JSON conversion
- **Rate Limiting**: Use delays between requests for bulk operations
- **Station Codes**: Use 4-letter codes (MONT, EMBR, etc.) not station names

#### OAuth 2.0
- **Invalid Redirect URI**: Ensure exact match with registered URI
- **Expired Tokens**: Implement refresh token logic
- **Scope Issues**: Request appropriate scopes for your use case
- **CORS Errors**: Use proper redirect URIs for web applications

### Support Resources

- 📖 **BART API Documentation**: [Official BART API Docs](http://api.bart.gov/docs/overview/index.aspx)
- 🔐 **OAuth 2.0 Specification**: [RFC 6749](https://tools.ietf.org/html/rfc6749)
- 🎵 **Spotify API Reference**: [Spotify Web API](https://developer.spotify.com/documentation/web-api/)
- 📟 **PagerDuty API Reference**: [PagerDuty API](https://developer.pagerduty.com/docs/rest-api-v2/)

---

## 🤝 Contributing

### Adding New Collections

1. **Fork** this repository
2. **Create** new collection in Postman
3. **Export** as JSON and add to `collections/` directory
4. **Create** corresponding environment file
5. **Update** README with collection details
6. **Submit** pull request

### Collection Standards

- ✅ Include comprehensive test scripts
- ✅ Add detailed documentation for each request
- ✅ Provide example responses
- ✅ Include error handling
- ✅ Use environment variables for configuration
- ✅ Follow REST API best practices

---

## 📄 License

This repository is available under the MIT License. See LICENSE file for details.

Individual APIs (BART, Spotify, PagerDuty) have their own terms of service and usage policies.

---

## 🌟 Acknowledgments

- **BART** for providing comprehensive public transit API
- **Spotify** for excellent API documentation and OAuth examples
- **PagerDuty** for robust incident management API
- **Postman** for the powerful API testing platform

---

## 📞 Contact

For questions, suggestions, or issues:
- 🐛 **Issues**: Use GitHub Issues for bug reports
- 💡 **Feature Requests**: Submit via GitHub Issues with enhancement label
- 📧 **General Questions**: Contact repository maintainer

---

*Last updated: October 2025*