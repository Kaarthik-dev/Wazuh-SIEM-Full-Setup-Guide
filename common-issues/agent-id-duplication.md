## Duplicate Agent ID Issue

### Problem
The agent appeared active locally but showed mismatched
or duplicate identities in the Wazuh dashboard.

### Root Cause
Agent identity is managed on the Wazuh manager.
Local agent renaming does not update manager-side records.

### Resolution
The existing agent entry was removed from the manager
and the agent was re-enrolled with a clean identity.

### Outcome
Agent identity was synchronized correctly across
the manager and dashboard.
