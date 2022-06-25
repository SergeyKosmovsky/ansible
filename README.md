# Домашнее задание к занятию "08.01 Введение в Ansible" 
## Подготовка к выполнению 
1. Установите ansible версии 2.10 или выше.  
2. Создайте свой собственный публичный репозиторий на github с произвольным именем.  
3. Скачайте playbook из репозитория с домашним заданием и перенесите его в свой репозиторий.  

## Основная часть  
1. Попробуйте запустить playbook на окружении из test.yml, зафиксируйте какое значение имеет факт some_fact для указанного хоста при выполнении playbook'a.  

![ДЗ-1](https://user-images.githubusercontent.com/93204208/175765512-a96b4879-490f-4639-92c0-55a2ac402cd3.PNG)


2. Найдите файл с переменными (group_vars) в котором задаётся найденное в первом пункте значение и поменяйте его на 'all default fact'.  

![ДЗ-2](https://user-images.githubusercontent.com/93204208/175765523-c398f995-85e9-46c6-bbb9-e2b826114ce5.PNG)


3. Воспользуйтесь подготовленным (используется docker) или создайте собственное окружение для проведения дальнейших испытаний.  

docker run --name ubuntu -d pycontribs/ubuntu sleep 31536000  
docker run --name centos7 -d pycontribs/centos:7 sleep 31536000  


4. Проведите запуск playbook на окружении из prod.yml. Зафиксируйте полученные значения some_fact для каждого из managed host.  

![ДЗ-4](https://user-images.githubusercontent.com/93204208/175776507-1c17960d-1cd1-4ad1-bdb1-924c7e2809f9.PNG)



5. Добавьте факты в group_vars каждой из групп хостов так, чтобы для some_fact получились следующие значения: для deb - 'deb default fact', для el - 'el default fact'.

6. Повторите запуск playbook на окружении prod.yml. Убедитесь, что выдаются корректные значения для всех хостов.

![ДЗ-5-6](https://user-images.githubusercontent.com/93204208/175776657-c95f1b33-7048-4b74-aeda-636afbafccaf.PNG)


7. При помощи ansible-vault зашифруйте факты в group_vars/deb и group_vars/el с паролем netology.

![ДЗ-7](https://user-images.githubusercontent.com/93204208/175776754-978da2c8-0185-46b1-9a56-e2b5ec4f6f78.PNG)


8. Запустите playbook на окружении prod.yml. При запуске ansible должен запросить у вас пароль. Убедитесь в работоспособности.

![ДЗ-8](https://user-images.githubusercontent.com/93204208/175776838-2fccd951-d24e-48dc-a9fd-820a365c91e7.PNG)


9. Посмотрите при помощи ansible-doc список плагинов для подключения. Выберите подходящий для работы на control node.  

local


10. В prod.yml добавьте новую группу хостов с именем local, в ней разместите localhost с необходимым типом подключения.

11. Запустите playbook на окружении prod.yml. При запуске ansible должен запросить у вас пароль. Убедитесь что факты some_fact для каждого из хостов определены из верных group_vars.

![ДЗ-11](https://user-images.githubusercontent.com/93204208/175777461-e020c345-c8d7-4962-aca6-f84718a5da62.PNG)


12. Заполните README.md ответами на вопросы. Сделайте git push в ветку master. В ответе отправьте ссылку на ваш открытый репозиторий с изменённым playbook и заполненным README.md.



# Самоконтроль выполнения задания

1. Где расположен файл с some_fact из второго пункта задания?  
group_vars/all/examp.yml  

2. Какая команда нужна для запуска вашего playbook на окружении test.yml?  
ansible-playbook -i inventory/test.yml site.yml  

3. Какой командой можно зашифровать файл?  
ansible-vault encrypt group_vars/el/examp.yml  

4. Какой командой можно расшифровать файл?  
ansible-vault decrypt group_vars/el/examp.yml  

5. Можно ли посмотреть содержимое зашифрованного файла без команды расшифровки файла? Если можно, то как?  
ansible-vault view group_vars/el/examp.yml  

6. Как выглядит команда запуска playbook, если переменные зашифрованы?  
ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass  

7. Как называется модуль подключения к host на windows?  
winrm  

8. Приведите полный текст команды для поиска информации в документации ansible для модуля подключений ssh  
ansible-doc -t connection ssh  

9. Какой параметр из модуля подключения ssh необходим для того, чтобы определить пользователя, под которым необходимо совершать подключение?  
remote_user  
