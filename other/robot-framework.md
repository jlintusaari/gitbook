# Robot Framework

rfdebug tricks

```text
Import Library  MyLib


${lib}    Get Library Instance    MyLib

# Run a method or get attribute
${lib.method()}
${lib.attribute}
    
# Run sequentially
Catenate  ${lib.method1()}  ${lib.method2()}
    
# Set attribute or variable
${lib.attribute}    Set Variable    value
${var}              Set Variable    ${lib.attribute}
```

