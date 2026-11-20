# Домашнее задание к занятию 5 «Тестирование roles» - Розаев А.Ю.

## Подготовка к выполнению

1. Установлен molecule и его драйвера: `pip3 install "molecule-plugins[docker,podman]" docker ansible-core`.

![0_1](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_0_1.png)

2. Выполнен `docker pull aragast/netology:latest` —  образ с podman, tox и несколькими пайтонами (3.7 и 3.9) внутри.

![0_2](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_0_2.png)

---

## Основная часть

Цель — настроить тестирование ролей. 

Задача — сделать сценарии тестирования для vector. 

Ожидаемый результат — все сценарии успешно проходят тестирование ролей.

### Molecule

1. Внутри корневой директории clickhouse-role запущен  `molecule test -s ubuntu_xenial`.

![1_1](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_1_1.png)

2. В каталоге vector-role создан сценарий тестирования по умолчанию при помощи `molecule init scenario`, сконфигурирован файл `molecule/default/molecule.yml`.

![1_2](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_1_2_1.png)

![1_2](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_1_2_2.png)

3. Добавлены дистрибутивы (oraclelinux:8, ubuntu:22.04) для инстансов и протестирована роль, исправлены найденные ошибки.

![1_3](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_1_3.png)

4. Добавлены несколько assert в verify.yml-файл для проверки работоспособности vector-role (проверка, что конфиг валидный, проверка успешности запуска и др.).
5. Запущено тестирование роли повторно - прошло успешно.

![1_5](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_1_5.png)

5. Добавлен [тег](https://github.com/expgt/net-fops-hw-16-5/tree/1.1.0) на коммит с рабочим сценарием в соответствии с семантическим версионированием.

### Tox

1. В директорию с vector-role добавлены файлы из [директории](./example).
2. Запущен `docker run --privileged=True -v <path_to_repo>:/opt/vector-role -w /opt/vector-role -it aragast/netology:latest /bin/bash`, где path_to_repo — путь до корня репозитория с vector-role.

![2_2](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_2_2.png)

3. Внутри контейнера выполнена команда `tox`.

![2_3](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_2_3.png)

4. Создан облегчённый сценарий для `molecule` с драйвером `molecule_podman`. Проверена его на исполнимость.

![2_4_1](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_2_4_1.png)

![2_4_2](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_2_4_2.png)

5. Прописана правильная команда в `tox.ini`, чтобы запускался облегчённый сценарий.

![2_5](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_2_5.png)

6. Запущена команда `tox`. Всё отработало успешно.

![2_6](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_2_6.png)

7. Добавлен [тег](https://github.com/expgt/net-fops-hw-16-5/tree/1.2.0) на коммит с рабочим сценарием в соответствии с семантическим версионированием.

---

## Необязательная часть

1. Выполнены такие же манипуляции для создания роли LightHouse.

![3_1_1](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_3_1_1.png)

![3_1_2](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_3_1_2.png)

![3_1_3](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_3_1_3.png)

![3_1_4](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_3_1_4.png)

![3_1_5](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_3_1_5.png)

2. Создан сценарий, который умеет поднимать весь стек при помощи всех ролей.

![3_2](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_3_2.png)

3. Проверена работоспособность стека. Создан отдельный [verify.yml](https://github.com/expgt/net-fops-hw-16-5/blob/main/playbook/roles/lighthouse-role/molecule/full_stack/verify.yml), который проверяет работоспособность интеграции всех инструментов между ними.

![3_3](https://github.com/expgt/net-fops-hw-16-5/blob/main/16_5_3_3.png)

4. Добавлен [тег](https://github.com/expgt/net-fops-hw-16-5/tree/1.3.0) на коммит с рабочим сценарием в соответствии с семантическим версионированием.
