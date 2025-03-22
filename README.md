# Ansible Playbooks

Цей репозиторій містить колекцію Ansible-плейбуків для автоматизації розгортання та налаштування серверів.

## Вимоги

- Ansible >= 2.9
- Python >= 3.6
- Налаштований SSH-доступ до цільових серверів

## Структура репозиторію

```
Ansible/
│── inventory/       # Файли інвентаризації
│── roles/           # Ролі для різних конфігурацій
│── playbooks/       # Основні плейбуки
│── vars/            # Глобальні змінні
│── templates/       # Jinja2-шаблони конфігурацій
│── files/           # Статичні файли
│── ansible.cfg      # Налаштування Ansible
│── requirements.yml # Залежності
```

## Використання

1. Клонувати репозиторій:
   ```sh
   git clone https://github.com/sevii-ia/Ansible.git
   cd Ansible
   ```

2. Встановити необхідні залежності:
   ```sh
   ansible-galaxy install -r requirements.yml
   ```

3. Запустити плейбук:
   ```sh
   ansible-playbook -i inventory/hosts playbooks/setup.yml
   ```
