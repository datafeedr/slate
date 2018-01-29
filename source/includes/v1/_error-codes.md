# Error Codes

Possible error codes and their respective messages and HTTP status codes:

Error Code | Error Message | HTTP Status
---|---|---
101 | Invalid request method | 400
102 | Content length not specified | 400
103 | No content | 400
104 | Content too long | 400
105 | Invalid mime type | 400
106 | JSON parse error | 400
107 | Invalid request compression | 400
111 | Required parameter missing | 400
112 | Invalid parameter type | 400
113 | Invalid timestamp | 400
114 | Unknown action | 400
115 | Request expired | 400
201 | Access denied | 403
202 | Invalid access id | 403
203 | Invalid signature | 403
204 | Wrong authorization | 403
205 | Invalid access key | 403
301 | Request limit exceeded | 400
302 | Response too long | 400
303 | Total limit exceeded | 400
304 | Limit too big | 400
401 | Query syntax error | 400
402 | Query was empty | 400
403 | Invalid integer | 400
404 | Invalid date | 400
405 | Invalid currency | 400
406 | Invalid source id | 400
407 | Invalid merchant id | 400
410 | Invalid field | 400
411 | Wrong field type | 400
412 | Bad argument | 400
413 | Field is not sortable | 400
420 | Impossible field combination | 400
421 | Query not computable | 400
422 | Condition is always false | 400
432 | Amazon query error | 400
433 | Zanox query error | 400
701 | Amazon API error | 500
751 | Zanox API error | 500
752 | PerformanceHorizon API error | 500
901 | Service unavailable | 503
903 | Query timed out | 504
990 | Unspecified error | 500
999 | Internal error | 500