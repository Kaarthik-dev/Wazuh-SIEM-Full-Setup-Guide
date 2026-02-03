## FIM Alerts Not Triggering

### Problem
File Integrity Monitoring alerts were not generated
after modifying protected files.

### Root Cause
FIM requires an initial baseline of file checksums
before changes can be detected.

### Resolution
The baseline was allowed to initialize before
making file changes.

### Outcome
FIM alerts triggered correctly after baseline
initialization.
