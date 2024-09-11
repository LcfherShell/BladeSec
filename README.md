<img src="https://repository-images.githubusercontent.com/855940385/0277f0c7-bd8c-45be-988a-540bdbfc5577" alt="BladeSec" style="max-width: 100%; height: auto;" />

---

# BladeSec - Security Module for NestJS

**BladeSec** is an add-on security module for [NestJS](https://nestjs.com/) that provides enhanced security features for websites. It helps developers safeguard their applications against common web security vulnerabilities and ensure robust security practices are in place.

## Features

- **Rate Limiting**: Prevent brute-force attacks by limiting the number of requests from a single IP.
- **IP Whitelisting/Blacklisting**: Allow or block specific IP addresses from accessing the site.
- **Content Security Policy (CSP)**: Mitigate cross-site scripting (XSS) attacks by enforcing CSP headers.
- **Cross-Origin Resource Sharing (CORS) Configuration**: Securely configure CORS policies for the application.
- **Session Management**: Protect session integrity with secure cookie management and session expiration.
- **Security Headers**: Automatically apply essential security headers (X-XSS-Protection, Strict-Transport-Security, etc.).
- **Request Sanitization**: Ensure inputs are sanitized to prevent injection attacks.
- **Logging and Monitoring**: Track and log suspicious activities for analysis and alerting.

## Installation

To install BladeSec, use npm or yarn:

```bash
npm install bladsec
# or
yarn add bladsec
```

## Usage

Once installed, BladeSec can be easily integrated into your NestJS application by importing the module into your `AppModule` or any other specific module.

```typescript
import { Module } from '@nestjs/common';
import { BladeSecModule } from 'bladsec';

@Module({
  imports: [
    BladeSecModule.forRoot({
      rateLimit: {
        windowMs: 15 * 60 * 1000, // 15 minutes
        maxRequests: 100, // limit each IP to 100 requests per window
      },
      ipWhitelist: ['192.168.0.1'],
      corsOptions: {
        origin: 'https://your-domain.com',
        methods: 'GET,HEAD,PUT,PATCH,POST,DELETE',
      },
      sessionOptions: {
        secret: 'your-session-secret',
        cookie: { secure: true },
      },
    }),
  ],
})
export class AppModule {}
```

### Configuration

BladeSec can be configured to fit your application's specific security needs. Below is an example of how to pass configuration options when initializing the module:

```typescript
BladeSecModule.forRoot({
  rateLimit: {
    windowMs: 15 * 60 * 1000,
    maxRequests: 100,
  },
  corsOptions: {
    origin: 'https://your-domain.com',
    methods: ['GET', 'POST', 'PUT'],
  },
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["'self'"],
      scriptSrc: ["'self'", 'https://trusted.cdn.com'],
    },
  },
  sessionOptions: {
    secret: 'your-session-secret',
    resave: false,
    saveUninitialized: false,
    cookie: { secure: true, httpOnly: true },
  },
});
```

### Rate Limiting

BladeSec offers easy rate limiting, which helps prevent denial-of-service (DoS) and brute force attacks. Configure the rate limiting feature in your security options:

```typescript
rateLimit: {
  windowMs: 15 * 60 * 1000, // 15-minute window
  maxRequests: 100, // limit each IP to 100 requests per window
  message: 'Too many requests, please try again later.',
}
```

### IP Whitelisting and Blacklisting

Control which IPs can access your application by using the whitelisting or blacklisting feature:

```typescript
ipWhitelist: ['192.168.0.1', '127.0.0.1'],
ipBlacklist: ['203.0.113.0'],
```

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for more details.

---

Feel free to adjust or add more details to fit your actual BladeSec module specifics.
