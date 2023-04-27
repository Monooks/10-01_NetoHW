# Домашнее задание к занятию 10.1 "`Keepalived/vrrp`" - `Емельянов Михаил`
**

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

---

### Задание 1

Разверните топологию из лекции и выполните установку и настройку сервиса Keepalived. 

```
vrrp_instance test {

state "name_mode"

interface "name_interface"

virtual_router_id "number id"

priority "number priority"

advert_int "number advert"

authentication {

auth_type "auth type"

auth_pass "password"

}

unicast_peer {

"ip address host"

}

virtual_ipaddress {

"ip address host" dev "interface" label "interface":vip

}

}

```

В качестве решения предоставьте:
- рабочую конфигурацию обеих нод, оформленную как блок кода в вашем md-файле;
- скриншоты статуса сервисов, на которых видно, что одна нода перешла в MASTER, а вторая в BACKUP state.

### ОТВЕТ:
1. Нода № 1:
```
vrrp_instance failover_test {
state MASTER
interface enp0s8
virtual_router_id 10
priority 110
advert_int 4
authentication {
auth_type AH
auth_pass 1111
}
unicast_peer {
192.168.1.10
}
    virtual_ipaddress {
    192.168.1.50 dev enp0s8 label enp0s8:vip
}
}
```
2. Нода № 2:
```
vrrp_instance failover_test {
state BACKUP
interface enp0s8
virtual_router_id 10
priority 10
advert_int 4
authentication {
auth_type AH
auth_pass 1111
}
unicast_peer {
192.168.1.20
}
    virtual_ipaddress {
    192.168.1.50 dev enp0s8 label enp0s8:vip
}
}
```
![Скриншот-1](https://github.com/Monooks/10-01_NetoHW/blob/main/img/10.01_1.1.png)

![Скриншот-2](https://github.com/Monooks/10-01_NetoHW/blob/main/img/10.01_1.2.png)
---
## Дополнительные задания со звёздочкой*

Эти задания дополнительные. Их можно не выполнять. На зачёт это не повлияет. Вы можете их выполнить, если хотите глубже разобраться в материале.
 
### Задание 2*

Проведите тестирование работы ноды, когда один из интерфейсов выключен. Для этого:
- добавьте ещё одну виртуальную машину и включите её в сеть;
- на машине установите Wireshark и запустите процесс прослеживания интерфейса;
- запустите процесс ping на виртуальный хост;
- выключите интерфейс на одной ноде (мастер), остановите Wireshark;
- найдите пакеты ICMP, в которых будет отображён процесс изменения MAC-адреса одной ноды на другой. 

 *Пришлите скриншот до и после выключения интерфейса из Wireshark.*

### ОТВЕТ:
![Скриншот-1](https://github.com/Monooks/10-01_NetoHW/blob/main/img/10.01_2.1.png)

![Скриншот-2](https://github.com/Monooks/10-01_NetoHW/blob/main/img/10.01_2.2.png)