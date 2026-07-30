# Semaphore IT and IoT Diagnostics

Read-only Ansible diagnostics for alerts triggered by n8n and executed by Semaphore.

The repository intentionally contains no credentials and no corrective actions. Every playbook emits one machine-readable line prefixed with `DIAGNOSTIC_RESULT_JSON=`.

## Playbooks

- `playbooks/windows_service_diagnostic_readonly.yml`: Windows service, dependencies, recovery configuration, process, binary, event logs, host resources, SQL Agent and Telegraf evidence.
- `playbooks/linux_service_diagnostic_readonly.yml`: systemd service, journal warnings, dependencies and host resource summary.
- `playbooks/network_endpoint_diagnostic_readonly.yml`: controller-side DNS, ICMP and TCP port checks.
- `playbooks/iot_http_diagnostic_readonly.yml`: HTTP/HTTPS availability using a HEAD request without reading or changing device state.

## Output Contract

All reports use schema version `1.0` and include:

- `mode`: always `read_only`.
- `profile`: diagnostic profile that generated the report.
- `collected_at_utc`: evidence timestamp.
- `target`: host, service or endpoint identity.
- Collected facts and bounded evidence.
- `query_errors`: evidence that could not be collected, when applicable.
- `safety`: explicit statement of actions not performed.

The Windows profile also returns normalized `findings` with severity, code, message and evidence.

## Safety

These playbooks do not start, stop or restart services; reboot hosts; edit files; modify registry values; install packages; change firewalls; alter device state; or remediate incidents. Successful runs must finish with `changed=0`.
