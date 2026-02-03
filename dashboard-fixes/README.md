## Wazuh Dashboard Fixes

This section documents issues encountered with the
Wazuh Dashboard during deployment.

### Issues Covered
- Dashboard service failing to start
- Node.js memory exhaustion during initialization

### Resolution Summary
The dashboard is Node.js-based and requires sufficient
memory allocation. Adjusting memory limits resolved
the startup failures.

After remediation, the dashboard operated stably
and remained accessible for alert investigation.

