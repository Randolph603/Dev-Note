# ngrok

```
npm i ngrok -g
ngrok authtoken token
ngrok http https://localhost:44327
ngrok http --host-header=rewrite  https://localhost:3000
```


To make a summary, RESTful api can have arguments in several places:

In the request body - As part of a json body, or other MIME type
In the query string - e.g. /api/resource?p1=v1&p2=v2
As part of the URL-path - e.g. /api/resource/v1/v2
And you might see following attributes:

[FromQuery] (Gets values from the query string)
[FromUri] (This is not existing in dot net core, could ignore)
[FromRuote] (same as [Route(...)], Gets values from route data)
[FromForm] (Gets values from the posted form fields, content type of "application/x-www-url-formencoded ")
[FromBody] (Gets values from the request body, content type of "application/json")
[FromHeader] (Gets values from HTTP headers)
What I like to see:
HttpGet:
use path parameter or query parameter or both.

When simple use path. (e.g. get worker by id, [Route("api/worker/{id: int}"]) and
When complex use query. (e.g. api/worker?name=jack&gendar=1) and make request as class
When more complex try from body (e.g. api/worker , request body: {disable: true, createTime: "2021-02-01TZ00:00:00"}).
HttpPost/HttpPut:
use path + body (e.g. api/worker/2, request body:{ name: "jack", place: "Auckland"})

HttpDelete:
use path

About the search endpoint and next step, I like the GraphQL's design that use dynamic response fields which has a better performance. See Azure Search, give the response fields and query as parameter.

(e.g. GET [Organization URI]/api/data/v9.1/accounts?select=name&filter=Account_Emails/any(o:contains(o/subject,'sometext')))