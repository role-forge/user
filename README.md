# Ansible Роль: User

Эта роль Ansible создает пользователя, настраивает его права на выполнение конкретных команд, настраивает проль пользователя, копирует ssh ключи.

## Переменные роли

Следующие переменные могут быть установлены для настройки поведения роли:

- `user_name`: Имя пользователя.
  ```yaml
  user_name: example.com

- `user_password`: Пароль пользователя, переменная должна быть зашифрована.
  ```yaml
  user_password: "$6$rounds=656000$Q7JH/7l...mQbTfs5JbA$NQ1dSyedod/NJ0T1tI..."

- `user_sudo`: Переменная типа boolean для включения пользователя в группу sudo.
  ```yaml
  user_sudo: true

- `user_sudoers`: список команд которые пользователь должен выполнять без пароля.
  ```yaml
  user_sudoers: 
    - /bin/example
    - /bin/another-example

- `user_ssh_key`: Список публичных ssh ключей которые должны быть скопированы для пользователя.
  ```yaml
  user_ssh_key:
  - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC56o5lpxITIoDWYU6/Otv/cSQ3d5odBf0jM6PhmW0+cKRU8oNxaDQrbkcWhL...


### Пример плейбука
```yaml
- name: Make user
  hosts: all
  vars:
    user_name: example
    user_sudo: false
    user_password: "example-password"
    user_ssh_key:
      - ssh-rsa examplekey
    user_sudoers:
      - /bin/example
      - /bin/another-example
  roles:
    - role: user
