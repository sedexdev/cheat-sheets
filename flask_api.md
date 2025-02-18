# Securing a Flask API with JSON Web Tokens (JWT)

## Overview
This guide details a robust way to secure a Flask API using JWT authentication. It ensures that only you can send requests, includes proper rate limiting, and protects against common attack vectors.

---

## 1. Setting Up Flask with JWT Authentication

Install necessary dependencies:
```bash
pip install flask flask-jwt-extended flask-limiter
```

Create a `config.py` file for security settings:
```python
import os

class Config:
    SECRET_KEY = os.environ.get("SECRET_KEY", "your-very-secure-secret")
    JWT_SECRET_KEY = os.environ.get("JWT_SECRET_KEY", "your-jwt-secret")
    JWT_ACCESS_TOKEN_EXPIRES = 3600  # 1 hour expiration
    RATE_LIMIT = "5 per minute"
```

---

## 2. Implementing Authentication

### Generate a JWT Token (Only You Should Have Access)
```python
from flask import Flask, jsonify, request
from flask_jwt_extended import create_access_token, jwt_required, JWTManager
from flask_limiter import Limiter
from flask_limiter.util import get_remote_address
from config import Config

app = Flask(__name__)
app.config.from_object(Config)
jwt = JWTManager(app)
limiter = Limiter(get_remote_address, app=app, default_limits=[Config.RATE_LIMIT])

# Only allow your IP to generate tokens
ALLOWED_IP = "YOUR_STATIC_IP_HERE"

@app.route("/login", methods=["POST"])
@limiter.limit("2 per minute")  # Limit login attempts
def login():
    if request.remote_addr != ALLOWED_IP:
        return jsonify({"msg": "Unauthorized"}), 403
    
    password = request.json.get("password")
    if password == "your-strong-password":
        token = create_access_token(identity="admin")
        return jsonify(access_token=token)
    return jsonify({"msg": "Invalid credentials"}), 401
```

### Protecting API Endpoints with JWT
```python
@app.route("/secure-endpoint", methods=["GET"])
@jwt_required()
@limiter.limit("10 per minute")
def secure_endpoint():
    return jsonify({"msg": "Secure Data"})
```

---

## 3. Security Enhancements

### Restrict API Access to Your IP
```python
from flask import abort

def check_ip():
    if request.remote_addr != ALLOWED_IP:
        abort(403, "Unauthorized IP")
```
Apply it to routes:
```python
@app.before_request
def restrict_access():
    check_ip()
```

### Prevent Common Attacks

#### **Rate Limiting to Prevent Brute Force**
- Implemented using `flask-limiter`.

#### **Protect Against CSRF**
- Since JWTs are stateless, ensure they are only sent in headers (not in cookies or URLs).

#### **Use Strong JWT Secrets**
- Store secrets in environment variables, never in source code.

#### **Disable JWT Token Reuse**
```python
@jwt.token_in_blocklist_loader
def check_if_token_is_revoked(jwt_header, jwt_payload):
    return jwt_payload["jti"] in token_blocklist
```

#### **Use HTTPS**
- Ensure all requests are sent over HTTPS to prevent token interception.

#### **Enable Logging for Unauthorized Access Attempts**
```python
import logging
logging.basicConfig(level=logging.WARNING)

def log_unauthorized_access():
    logging.warning(f"Unauthorized access attempt from {request.remote_addr}")

@app.errorhandler(403)
def forbidden(error):
    log_unauthorized_access()
    return jsonify({"msg": "Forbidden"}), 403
```

---

## Conclusion
This setup ensures that:
- Only you can access the API (restricted by IP and authentication).
- JWT tokens protect sensitive endpoints.
- Rate limiting prevents brute force attacks.
- Common attack vectors are mitigated.

Use this approach to secure your Flask API effectively!

