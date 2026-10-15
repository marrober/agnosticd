To run the ansible job with the corect settings use :

````bash
cd /home/marrober/data/git-repos/agnosticd
ANSIBLE_LIBRARY=ansible/library 
ANSIBLE_ACTION_PLUGINS=ansible/action_plugins
ANSIBLE_ROLES_PATH=ansible/roles_ocp_workloads 

cat > /tmp/run-tpa.yml <<'EOF'
---
- name: Install Trusted Profile Analyzer
  hosts: localhost
  connection: local
  gather_facts: true
  become: false
  vars:
    ACTION: provision
    ansible_user: "{{ lookup('env', 'USER') }}"
  roles:
    - role: ocp4_workload_trusted_profile_analyzer
EOF

ANSIBLE_ROLES_PATH=ansible/roles_ocp_workloads \
ansible-playbook /tmp/run-tpa.yml -vv
````