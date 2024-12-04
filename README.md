# Лабораторная работа 4.
## Задание:  
Запустить в контейнере приложение “aafire”. Обратите внимание, что оно бесконечное и контейнер не будет автоматически отключаться.  
Приложить скриншот в процессе работы контейнера.  

Далее в рамках лабораторной работы необходимо самостоятельно настроить сеть между двумя контейнерами, также как в предыдущей работе вы настраивали связь между двумя виртуальными машинами.  

Для проверки сети между контейнерами вам потребуется утилита ping. Поскольку контейнеры очень маленькие и в них нет ничего лишнего (по сравнению с виртуальными машинами) - ping там не установлен. В вашем образе нужно будет установить пакет с этой утилитой, помимо aafire.  

Далее запустите два контейнера с aafire и оставьте их в работающем состоянии.  
Откройте ещё одно окно терминала и создайте сеть при помощи команды 
```
docker network create myNetwork
```
После этого нужно будет подключить контейнеры к вашей сети. Названия контейнеров можно увидеть при выводе списка действующих контейнеров у вас на машине.
```
docker network connect myNetwork mycontainer1
docker network connect myNetwork mycontainer2
```
Теперь при помощи следующей команды вы можете увидеть настройки созданной вами сети.
```
docker network inspect myNetwork
```
Далее вам нужно самостоятельно протестировать соединение между контейнерами утилитой ping и приложить скриншот.

# Реализация:

## Создание Dockerfile

Создадим файл `Dockerfile` со следующим содержимым:

```dockerfile
dockerfile 
FROM ubuntu:latest 
 
# Установка необходимых пакетов 
RUN apt-get update && \ 
    apt-get install -y libaa-bin iputils-ping && \ 
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/* 
 
# Запуск aafire с терминалом 
CMD ["sh", "-c", "exec aafire </dev/tty && tail -f /dev/null"]
```
**Объяснение:** 
- Используем официальный образ Ubuntu. 
- Устанавливаем необходимые пакеты: libaa-bin (для aafire`) и `iputils-ping. 
- Команда CMD запускает aafire с привязкой к терминалу. 

 
## Сборка Docker-образа

В терминале, находясь в директории с `Dockerfile`, выполним команду:

```bash 
sudo docker build -t aafire_image:latest . 
```

**Объяснение:**

- `-t aafire_image:latest` задаёт имя и тег образа.
- Точка `.` указывает на текущую директорию как контекст сборки.


## Запуск двух контейнеров с `aafire`

Запустим два контейнера в интерактивном режиме.

```bash
sudo docker run -itd --name mycontainer1 aafire_image:latest 
sudo docker run -itd --name mycontainer2 aafire_image:latest 
```

**Объяснение:** 
- -itd запускает контейнеры в интерактивном и фоновом режимах. 
- Контейнеры будут отображать aafire. 


## Создание сети `myNetwork`

Создадим пользовательскую сеть Docker:

```bash
sudo docker network create myNetwork
```


## Подключение контейнеров к сети `myNetwork`

Подключим оба контейнера к созданной сети.

```bash 
sudo docker network connect myNetwork mycontainer1 
sudo docker network connect myNetwork mycontainer2 
```


## Проверка соединения между контейнерами.

Выполняем `ping` из первого контейнера во второй.

```bash
sudo docker exec -it mycontainer1 ping mycontainer2 
```

**Объяснение:**

- `docker exec` позволяет выполнять команды внутри запущенного контейнера.
- Мы пингуем `mycontainer2` по имени контейнера.

**Ожидаемый результат:**

![image](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-12-04%20195914.png)


## Очистка ресурсов Docker

Чтобы  остановить и удалить созданные контейнеры, образы и сеть: 

```bash
sudo docker stop mycontainer1 mycontainer2 
sudo docker rm mycontainer1 mycontainer2 
sudo docker rmi aafire_image:latest 
sudo docker network rm myNetwork 
```

Для очистки неиспользуемых объектов: 

```bash
sudo docker system prune -a --volumes 
```

**Объяснение:**

- `docker system prune -a --volumes` удаляет все неиспользуемые ресурсы.


## Шаг 9: Отключение и включение Docker

### Отключение Docker

```bash
sudo systemctl stop docker
```

### Включение Docker

```bash
sudo systemctl start docker
```





