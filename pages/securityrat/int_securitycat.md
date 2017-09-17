---
title: SecurityCAT
#keywords: sample
summary: "Integrating SecurityRAT with SecurityCAT."
sidebar: home_sidebar
permalink: int_securitycat.html
#simple_map: true
#map_name: usermap
#box_number: 1
folder: product2
---


## SecurityCAT

SecurityCAT (Compliance Automation Tool) is an extension for SecurityRAT meant for automatic testing of requirements. 
Given that the implementation depends on the particular used requirements, everybody should implement his own respective version of SecurityCAT.
SecurityRAT just defines an API it can speak to and which can be used for starting a scan, fetching the results and stopping a scan. 

## API specification

### Create a test 

Request:
```
POST /scanapi/tests
```

Reponse 202/Accepted containing the URL for fetching the result in the ```Location``` header is expected. 

### Fetch test results
Request:
```
GET /scanapi/tests/{test_id}
```

Response contains an array of requirements being tested together with the current status of the test. 
```
200/OK
 
[{
    requirement: req_shortName
    testResults: [{
        status: ERROR/IN_PROGRESS/PASSED/FAILED
        confidenceLevel: 90
        message: String
        tool: tool_name
    }]
}]
```

* ```status``` describes the state of the test:
  * ```ERROR```: Test could not be completed
  * ```IN_PROGRESS```: Test is being executed
  * ```PASSED```: Test was completed and the requirement is fulfilled.
  * ```FAILED```: Test was completed and the requirement is not fulfilled.
* ```confidenceLevel``` indicates the value in percent about reliability of the test
* ```message``` contains detailed description of the test, markdown is supported
* ```tool``` indicates the name of tool / microservice which actually performed the test

### Stop the test
Request:
```
DELETE /scanapi/tests/{test_id}
```

Response 200 is expected. 


{% include links.html %}