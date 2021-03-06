# syncerror

eventMaturity | [2 - Tested](../../specification/STU1/#event-maturity-model)

## Workflow

A synchronization error has been detected. Inform subscribed clients. 

Unlike most of FHIRcast events, `syncerror` is an infrastructural event and does not follow the `FHIR-resource`-`[open|close]` syntax and is directly referenced in the [underlying specification](../../specification/STU1/#event-notification-errors).

## Context

Key | Optionality | Fhir operation to generate context | Description
----- | -------- | ---- | ---- 
`operationoutcome` | OPTIONAL | `OperationOutcome` | FHIR resource describing an outcome of an unsuccessful system action. The OperationOutcome SHALL use a code of `processing`. The OperationOutcome's `details.coding.code` SHALL contain the id of the event that this error is related to as a `code` with the `system` value of "https://fhircast.hl7.org/events/syncerror/eventid" and the name of the relevant event with a `system` value of "https://fhircast.hl7.org/events/syncerror/eventname" . Other `coding` values can be included with different `system` values so as to include extra information about the `syncerror`.



### Examples

<mark>

```json
{
  "timestamp": "2018-01-08T01:37:05.14",
  "id": "q9v3jubddqt63n1",
  "event": {
    "hub.topic": "7544fe65-ea26-44b5-835d-14287e46390b",
    "hub.event": "syncerror",
    "context": [
      {
        "key": "operationoutcome",
        "resource": {
          "resourceType": "OperationOutcome",
          "issue": [
            {
              "severity": "warning",
              "code": "processing",
              "diagnostics": "AppId3456 failed to follow context",
              "details": {
                "coding": [
                  {
                    "system": "https://fhircast.hl7.org/events/syncerror/eventid",
                    "code": "fdb2f928-5546-4f52-87a0-0648e9ded065"
                  },
                  {
                    "system": "https://fhircast.hl7.org/events/syncerror/eventname",
                    "code": "patient-open"
                  },
                  {
                    "system": "http://example.com/events/syncerror/your-error-code-system",
                    "code": "FHIRcast sync error"
                  }
                ]
              }
            }
          ]
        }
      }
    ]
  }
}
```

</mark>

## Change Log

Version | Description
---- | ----
1.0 | Initial Release
2.0 | Require id of event syncerror is about, in `OperationOutcome.details.coding.code`
