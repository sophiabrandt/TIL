# CURLIE on the commandline

Using the [fish shell](https://fishshell.com) and [curlie](https://curlie.io/) as a more user-friendly alternative to curl.

## Cookies

[Stackoverflow](https://stackoverflow.com/questions/30760213/save-cookies-between-two-curl-requests):

```sh
curlie POST :4000/auth/login email=test@tester.com password='testPassword$5' -c cookie.txt
```

```sh
curlie -d '{"query": "query Me { me { _id email } }"}' -POST :4000/graphql -b cookie.txt
```

## Bearer Tokens

Assuming the bearer token is a json response with the following structure:

```json
{ "accessToken": "ey...." }
```

```sh
set -x AUTH_TOKEN (curlie post https://hostname/auth/signin username='your username' password='your password' | jq -r '.accessToken')
```

```sh
curlie GET localhost:4000/api -H "Authorization: Bearer $AUTH_TOKEN"
curlie POST localhost:4000/api -H "Authorization: Bearer $AUTH_TOKEN" title="Star Trek: Picard" year="2019" rating="7"

```
