# Exercise 01: Ping your hosts

## Goal

Let Ansible reach both managed nodes.

## Concepts

- **Control node**: the machine where Ansible runs. In this workshop that is
  `acs`.
- **Managed nodes**: the machines Ansible configures over SSH: `node1` and
  `node2`.
- **Inventory** (`inventory.ini`): the list of managed nodes, one host per
  line.
- **`ansible.cfg`**: settings Ansible reads from the current directory. Here it
  points to the inventory.
- **Ad-hoc command**: a single Ansible action from the command line:
  `ansible <hosts> -m <module>`.
- **`ping` module**: logs in on a host and checks Ansible can run there. It
  answers `pong`.

## Start

```bash
ssh -p 2220 ansible@localhost
cd exercises/01-ping
ansible all -m ping
```

`node1` answers with `"ping": "pong"`.

## Assignment

Only `node1` is in the inventory. Add `node2` so both hosts answer.

## Expected result

```text
node1 | SUCCESS => { ... "ping": "pong" }
node2 | SUCCESS => { ... "ping": "pong" }
```

## Check

Compare your work with the solution:

```bash
diff -r -x README.md ~/exercises/01-ping ~/solutions/01-ping
```
