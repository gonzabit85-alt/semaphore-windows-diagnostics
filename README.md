# Semaphore Windows Diagnostics

Read-only Ansible diagnostics for Windows service alerts triggered by n8n.

This repository intentionally contains no credentials and no corrective actions.

## Playbooks

- `playbooks/windows_service_diagnostic_readonly.yml`: inspects a Windows service and recent event logs through WinRM.

## Safety

The playbook does not start, stop, restart, reboot, edit files, modify registry values, install packages, or change configuration.
