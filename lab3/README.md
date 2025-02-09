# САНКТ-ПЕТЕРБУРГСКИЙ НАЦИОНАЛЬНЫЙ ИССЛЕДОВАТЕЛЬСКИЙ УНИВЕРСИТЕТ ИНФОРМАЦИОННЫХ ТЕХНОЛОГИЙ, МЕХАНИКИ И ОПТИКИ ФАКУЛЬТЕТ ИНФОКОММУНИКАЦИОННЫХ ТЕХНОЛОГИЙ
## Отчет по лабораторной работе №2 по курсу «Информатика» 
## Тема: Сетевые технологии
**Выполнила: Жмачинская Д.С. К3141**                                                                                                                                               
**Проверила: Болгова Е.В.**                                                                                                                                                
**Санкт-Петербург 2024 г.**                                                                                                                 

## Задание:
Необходимо настроить виртуальную машину А с Ubuntu (желательно, но можно и другую Linux подобную ОС) в VirtualBox. Обеспечить доступ в сеть Интернет. Осуществить проверку этого доступа и приложить скриншот из терминала. Следующим шагом настроить ещё одну виртуальную машину Б. После чего обеспечить сетевой доступ от машины А к машину Б. Приложить скриншот из терминала. Поднять ещё одну виртуальную машину В. Организовать сетевой доступ:

из машины А в машину Б,
из машины А в машину В,
но запретить доступ из машины Б в машину В,
приложить скриншот, на котором видно терминалы всех трёх машин и видно что между машинами есть (или нет) доступа.

## 1. Создаём три виртуальные машины MAAA, MBBB, MCCC
## 2. Создаём виртуальных сетевых адаптеров:
   Переходим *Файл* > *Инструменты* > *Менеджер сетей*
   
![Настройки](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-12%20221936.png)

   Настраиваем два адптера, установавливаем флажок «Включить сервер», чтобы активировать встроенный DHCP-сервер:
   
![Адаптеры](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-12%20222312.png)

## 3. Настраиваем сетевые параметры:
  **Настройка машины MAAA**
  
![Адаптеры](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-13%20012033.png)
![Адаптеры](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-13%20012038.png)
![Адаптеры](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-13%20012043.png)
  
  **Настройка машины MBBB**
  
![Адаптеры](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-13%20012056.png)


  **Настройка машины MCCC**
  
  ![Адаптеры](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-13%20012121.png)

## 4. Проверка работы сети и настройка недоступности машины MBBB в MCCC:

Узнаем ip-адреса каждой машины
```bash
ip -br a
```

Машина **МAAA**

![ip](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-13%20011902.png)


Машина **МBBB**

![ip](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-13%20011735.png)


Машина **МCCC**

![ip](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-13%20010608.png)


### Проверяем доступ машины **МААА** к Интернету
```bash
ping -c 4 google.com
```

![ip](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-13%20010814.png)

### Проверка доступа с машины **МААА** в машину **МВВВ**

```bash
ping -c 4 192.168.56.102
```

![Доступ](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-13%20011026.png)

### Проверка доступа с машины **МААА** в машину **МССC**

```bash
ping -c 4 192.168.56.101
```
![Доступ](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-13%20000600.png)

### Запрещаем доступ с машины **МВВВ** в машину **МССС**

```bash
sudo iptables -A OUTPUT -d 192.168.56.103 -j DROP
```

Проверяем недоступность с машины **МВВВ** в **МССС**

![Доступ](https://github.com/befovis/Informatics/blob/main/images/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202024-11-13%20011152.png)
