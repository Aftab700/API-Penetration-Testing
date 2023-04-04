# API-Penetration-Testing


## Web API Indicators

lookout for obvious URL naming schemes:

- https://target-name.com/api/v1
- https://api.target-name.com/v1 
- https://target-name.com/docs
- https://dev.target-name.com/rest

Look for API indicators within directory names like:

/api, /api/v1, /v1, /v2, /v3, /rest, /swagger, /swagger.json, /doc, /docs, /graphql, /graphiql, /altair, /playground

Also, subdomains can also be indicators of web APIs:
- api.target-name.com
- uat.target-name.com
- dev.target-name.com
- developer.target-name.com
- test.target-name.com

TruffleHog is a great tool for automatically discovering exposed secrets.
- https://github.com/trufflesecurity/trufflehog

## Active API Reconnaissance

- `nmap -sV --script=http-enum <target> -p 80,443,8000,8080`
- `amass enum -active -d target-name.com |grep api`
- The following example uses an API-specific wordlist to find the directories on an IP address:
  - ` gobuster dir -u target-name.com:8000 -w /home/hapihacker/api/wordlists/common_apis_160 `
- Kiterunner for discovering API endpoints and resources.
  - https://github.com/assetnote/kiterunner
  - ` kr scan HTTP://127.0.0.1 -w ~/api/wordlists/data/kiterunner/routes-large.kite `

## Authentication Attacks

brute-force attacks:
- creating targeted password lists
  - https://github.com/sc0tfree/mentalist
  - https://github.com/Mebus/cupp

Password Spraying
- combining a long list of users with a short list of targeted passwords.

## JWT Attacks

JWT.io is a free web JWT debugger
- https://jwt.io/

Automating JWT attacks with JWT_Tool
- https://github.com/ticarpi/jwt_tool/wiki

## Exploiting API Authorization

- Find Resource IDs and Requests

### Authorization Testing Strategy:
  1. Create a UserA account.
  2. Use the API and discover requests that involve resource IDs as UserA.
  3. Document requests that include resource IDs and should require authorization.
  4. Create a UserB account.
  5. Obtaining a valid UserB token and attempt to access UserA's resources.

- Try changing request method.

## Improper Assets Management
> Testing for Improper Assets Management is all about discovering unsupported and non-production versions of an API

- Non-production versions of an API include any version of the API that was not meant for end-user consumption. Non-production versions could include:
  - api.test.target.com
  - api.uat.target.com
  - beta.api.com
  - /api/private
  - /api/partner
  - /api/test
- Make sure to check out the path, parameters, and headers for any versioning information.














