## Manager–Agent Version Mismatch

### Problem
Agent enrollment failed even though configuration
appeared correct.

### Root Cause
The installed agent version was higher than the
manager version, which is unsupported.

### Resolution
The agent was reinstalled with a version matching
the manager.

### Outcome
The agent enrolled successfully and began
sending events.
