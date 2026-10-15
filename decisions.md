# Decisions

- **Rocky Linux 9 base image** for all containers (`rockylinux/rockylinux`,
  published by the Rocky project): closest free match to the students' RHEL 9
  environment. UBI 9 lacks openssh-server in its free repos.
- **All machines run systemd** (`9-ubi-init` image) so they behave like VMs
  and can run services. systemd needs a writable cgroup tree: `cgroup: host`
  plus a read-write `/sys/fs/cgroup` mount, which is less than `privileged`.
- **Static IPs** on subnet `172.30.0.0/24` so machines have fixed addresses like
  VMs. Other subnets may clash with existing Docker networks or VPNs.
- **SSH login from the host** as `ansible`/`ansible` on `127.0.0.1:2220`
  (acs), `:2221` and `:2222` (nodes): simplest for students, and it matches
  how they reach a control node at work; the ports are only reachable from the local
  machine. Port mapping also works on Docker Desktop, where container IPs are
  not reachable from the host.
- **Ansible from pip in a venv** (`/opt/ansible`, Python 3.12, version pinned
  in `acs/Dockerfile`): RHEL's `ansible-core` package is too old.
- **Ansible environment in `/etc/profile.d/`** on acs: login sessions under
  systemd don't inherit Docker `ENV` variables.
- **SSH key in a shared named volume** (`ssh-keys`): `acs` generates the key
  at first boot, nodes install the public key at boot. The key survives container
  recreation.
- **Host keys accepted automatically** via `acs/ssh_config`: nodes get new host
  keys on rebuild, and exercise `ansible.cfg` files stay free of SSH settings.
- **User `ansible` with UID 1000** on all containers: matches the host user, so
  students can edit the bind-mounted exercises with their own editor.
- **`solutions/` mounted read-only** in `acs`: students can compare but not
  change solutions.
- **Students use Rancher Desktop on Windows** with the dockerd (moby) engine:
  it provides `docker compose`.
- **`ANSIBLE_CONFIG=.` on acs**: Windows bind mounts look world-writable, and
  Ansible skips `./ansible.cfg` in a world-writable directory. An explicit
  `ANSIBLE_CONFIG` bypasses that check, so students can clone on Windows.
- **LF line endings via `.gitattributes`**: Git for Windows checks out CRLF by
  default, which breaks the shell scripts in the containers.
- **Exercise instructions in English**, matching Ansible docs and module names.
- **Exercise structure**: each exercise starts from a working setup and asks
  one small change. The solution is the full exercise directory after that
  change. An exercise only uses concepts from itself and earlier exercises.
- **Markdown follows markdownlint default rules**, including 80-character
  lines; warnings are fixed, not suppressed.
