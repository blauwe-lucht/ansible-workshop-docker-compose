# To-do

- [ ] Refine exercise 01 into the blueprint for the other exercises.
- [ ] Decide on the Python interpreter discovery warning (set
  `interpreter_python` in `ansible.cfg` or explain it).
- [ ] Plan the list of exercises and their concepts.
- [ ] Add passwordless sudo for `ansible` on the nodes when an exercise
  introduces `become`.
- [ ] Smoke test on one student laptop (Rancher Desktop, Windows):
  - `docker compose up -d --build`
  - ping from acs in `solutions/01-ping`
  - `ssh -p 2220 ansible@127.0.0.1` and `-p 2221` from Windows
  - `systemctl is-system-running` on a node
