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

#### Authorization Testing Strategy:
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

## Mass Assignment Attacks
> Mass Assignment vulnerabilities are present when an attacker is able to overwrite object properties that they should not be able to.

One of the ways that you can discover mass assignment vulnerabilities by finding interesting parameters in API documentation and then adding those parameters to requests. Look for parameters involved in user account properties, critical functions, and administrative actions.

Testing Account Registration for Mass Assignment
- Try adding other key-values to the JSON POST body, such as:
```
"isadmin": true,
"isadmin":"true",
"admin": 1,
"admin": true, 
```

- Fuzzing for Mass Assignment with Param Miner
  - Right-click on a request that you would like to mine for parameters. Select Extensions > Param Miner > Guess params > Guess JSON parameter. 

####  free tools to see request made to url:

- http://webhook.site/
- http://pingb.in/
- https://requestbin.com/
- https://canarytokens.org/

##  Injection Attacks

if the API is expecting a certain type of input (number, string, boolean value) send:
- A very large number
- A very large string
- A negative number
- A string (instead of a number or boolean value)
- Random characters
- Boolean values
- Meta characters

#### SQL Injection Metacharacters

- SQL metacharacters that can cause some issues:
```SQL
'
''
;%00
--
-- -
""
;
' OR '1
' OR 1 -- -
" OR "" = "
" OR 1 = 1 -- -
' OR '' = '
OR 1=1
```

#### NoSQL Injection

The following are common NoSQL metacharacters you could send in an API request to manipulate the database:
```json
$gt 
{"$gt":""}
{"$gt":-1}
$ne
{"$ne":""}
{"$ne":-1}
 $nin
{"$nin":1}
{"$nin":[1]}
{"$where":  "sleep(1000)"}
```

$gt is a MongoDB NoSQL query operator that selects documents that are greater than the provided value. 

The $ne query operator selects documents where the value is not equal to the provided value. 

The $nin operator is the “not in” operator, used to select documents where the field value is not within the specified array. 

#### OS Injection

Characters such as the following all act as command separators, which enable a program to pair multiple commands together on a single line.

```Shell
|
||
&
&&
'
"
;
'"
```

#### Injection Targets

requests that include user input.examples:
- PUT videos by id
- GET videos by id
- POST change-email
- POST verify-email-token
- POST login
- GET location
- POST check-otp
- POST posts
- POST validate-coupon
- POST orders

#### WAF Evasion

String terminators can be placed in different parts of the request, like the path or POST body, to attempt to bypass any restrictions in place.

Here is a list of potential string terminators you can use:
```
%00
0x00
//
;
%
!
?
[]
%5B%5D
%09
%0a
%0b
%0c
%0e
```

- **Case Switching**:
  - Sometimes API security controls are pretty easy to beat. If a security control is built around the literal spelling and case of the components within a request, then case switching can be an effective technique to bypass the controls.
- Encoding Payloads

Awesome-WAF GitHub repo

https://github.com/0xInfection/Awesome-WAF#known-bypasses








