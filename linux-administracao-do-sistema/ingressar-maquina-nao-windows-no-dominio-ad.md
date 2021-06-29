# Ingressar máquina não Windows no Domínio AD

#### PBIS - Ferramenta  que abstrai o processo de ingresso de máquinas Linux e Unix em Samba4/AD

{% embed url="https://github.com/BeyondTrust/pbis-open" %}

#### Ansible Playbook para SSSD

```text
---
- name: Install SSSD for active directory
  ansible.builtin.package:
    name: 'openssh-server'
    state: present
  with_items:
    - realmd
    - sssd
    - oddjob
    - oddjob-mkhomedir
    - adcli
    - samba-common-tools
- name: Check if Server is on domain
  shell: "realm list"
  register: already_member
  changed_when: false
- name: join system to domain
  expect:
    command: "realm join {{ active_directory_realm }} --user={{ active_directory_user }}"
    responses:
      Password*: "{{ active_directory_password }}"
  when: already_member.stdout is not defined or already_member.stdout == ""
- name: Restore krb5 custom config
  template:
    src: "{{ item.src }}"
    dest: "{{ item.dest }}"
    owner: root
    group: root
    mode: 0644
  with_items:
    - src: krb5.conf.j2
      dest: /etc/krb5.conf
    - src: sssd.conf.j2
      dest: /etc/sssd/sssd.conf
- name: Add domain admins into sudoers
  ansible.builtin.lineinfile:
    path: /etc/sudoers
    state: present
    line: '"%domain admins" ALL=(ALL) ALL'
    validate: /usr/sbin/visudo -cf %s
```



