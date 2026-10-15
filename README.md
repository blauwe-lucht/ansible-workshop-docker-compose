# Ansible workshop

A lab with one Ansible Control Server (`acs`) and two managed nodes
(`node1`, `node2`), all on Rocky Linux 9.

## Start the lab

```bash
docker compose up -d --build
```

## Log in

All machines run systemd and behave like VMs.
Log in as `ansible` with password `ansible`:

```bash
ssh -p 2220 ansible@localhost   # acs
ssh -p 2221 ansible@localhost   # node1
ssh -p 2222 ansible@localhost   # node2
```

On `acs`, exercises are in `~/exercises` and solutions in `~/solutions`
(read-only). Edit the files on your own machine or inside `acs`.

| Host  | IP          |
|-------|-------------|
| acs   | 172.30.0.10 |
| node1 | 172.30.0.11 |
| node2 | 172.30.0.12 |

On Linux you can also reach the machines directly on their IP,
e.g. `ssh ansible@172.30.0.11`.

## Windows (Rancher Desktop)

- Select the **dockerd (moby)** container engine in Rancher Desktop.
- Clone the repo anywhere, e.g. on `C:\`.
- Log in with `127.0.0.1` instead of `localhost`,
  e.g. `ssh -p 2220 ansible@127.0.0.1`.

## Exercises

| #  | Exercise               | Concepts                                     |
|----|------------------------|----------------------------------------------|
| 01 | [Ping your hosts][ex1] | nodes, `ansible.cfg`, inventory, ad-hoc ping |

[ex1]: exercises/01-ping/README.md

## Stop the lab

```bash
docker compose down      # keeps the SSH key
docker compose down -v   # also removes the SSH key
```
