# Модули ядра Linux

## Сборка

1. Необходимо перейти в директорию с нужным заданием и выполнить команду для сборки проекта `make`;

2. Файл модуля ядра `xxx.ko` появится в той же директории;

3. Для удаления всех файлов сборки необходимо выполнить команду `make clean`.

## Задания

### Задание 1. Написать модуль ядра, который регистрирует символьное устройство в Linux и предоставляет возможность для чтения и записи через это устройство.

Код представлен в директории [Task1](https://github.com/EltexEmbeddedC/linux-kernel-modules/blob/main/Task1). После сборки модуля установим его в ядро:

```bash
sudo insmod task1.ko
```

Выведем последние 10 сообщений ядра и увидим сообщения об успешной загрузке модуля:

```bash
sudo dmesg | tail -n10
```

![image](https://github.com/user-attachments/assets/e009b840-36a9-4785-b598-1c270746eb08)

Создадим файл устройства в `/dev`, выполнив команду:

```bash
sudo mknod task1 c 511 0
```

Повысим права доступа к файлу:

```bash
sudo chmod +0666 task1
```

![image](https://github.com/user-attachments/assets/7fa66311-072b-40c4-9e04-adde75dec15c)

Выведем его содержимое:

```bash
sudo cat task1
```

Изменим содержимое:

```bash
sudo echo "123456789" > task1
```

Снова выведем содержимое:

```bash
sudo cat task1
```

![image](https://github.com/user-attachments/assets/6249c4a9-aa9d-4821-a763-38408a31d388)

После проведения тестирования удалим файл устройства и выгрузим модуль из ядра:

```bash
sudo rm /dev/task1
sudo rmmod task1
```
