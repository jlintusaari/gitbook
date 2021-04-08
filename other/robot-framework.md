# Robot Framework

Accessing library instance attributes

```text
Library  MyLib

Test Case
    ${lib}    Get Library Instance    MyLib
    ${lib.attribute}    Set Variable    value
    ${test}    Set Variable    ${lib.attribute}
    Log To Console    ${test}  
```

