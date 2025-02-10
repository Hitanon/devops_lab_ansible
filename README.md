# 1. Настройка сети на обеих виртуальных машинах
ip a
sudo nano /etc/netplan/50-cloud-init.yaml
sudo netplan apply
ip addr

# 2. Создание пользователя runner и настройка sudo
sudo useradd -m runner
sudo passwd runner
sudo usermod -a -G sudo runner
sudo nano /etc/sudoers

# 3. Настройка SSH-доступа между машинами
ssh-keygen -t rsa -b 4096
ssh-copy-id runner@10.0.2.16
ssh runner@10.0.2.16

# 4. Установка Ansible на первой VM
sudo apt install ansible
ansible-playbook --version

# 5. Создание файлов для Ansible
mkdir lab-ansible
cd lab-ansible/
touch playbook.yml
touch inventory.ini
nano inventory.ini

# 7. Написание и запуск Playbook для запуска nginx
nano playbook.yml
ansible-playbook playbook.yml -i inventory.ini --check
ansible-playbook playbook.yml -i inventory.ini

# 8. Написание и запуск Playbook для запуска nginx и добавления индексного файла
sudo nano index.html
sudo nano playbook.yml
ansible-playbook playbook.yml -i inventory.ini

# 8. Проверка работы веб-сервера
curl http://10.0.2.16