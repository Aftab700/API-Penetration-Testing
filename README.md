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


