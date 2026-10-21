# DirectAdmin PHP2Shell Ansible Mitigation

Temporary mitigation for PHP2Shell (CVE-2026-109618 and CVE-2026-109619) on DirectAdmin servers using PHP-FPM.

The playbook applies two PHP security settings:

```ini
session.upload_progress.enabled = Off
session.use_strict_mode = 1
```

Settings are applied through a separate PHP INI file and enforced through the DirectAdmin PHP-FPM configuration.

Existing custom configurations are preserved. Supports deployment, verification and rollback.

## Usage

Adjust `hosts` in the playbook to match your Ansible inventory.

**Apply mitigation:**
```bash
ansible-playbook fix_php_exploit.yml -e mitigation_action=apply
```

**Verify settings:**
```bash
ansible-playbook fix_php_exploit.yml -e mitigation_action=verify
```

**Rollback:**
```bash
ansible-playbook fix_php_exploit.yml -e mitigation_action=rollback
```

Rollback removes only the configuration added by this playbook.

## Note

This is a temporary workaround, not a replacement for the official PHP security patches. Apply the patches as soon as they become available.
Test on one server before deploying across your environment.

## More info

https://sansec.io/research/php2shell
https://www.php.net/archive/2026.php#2026-10-20-1
