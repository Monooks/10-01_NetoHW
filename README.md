# �������� ������� � ������� 10.1 "`Keepalived/vrrp`" - `��������� ������`
**

### ���������� �� ���������� ��������� �������

1. �������� fork [����������� c �������� �������](https://github.com/netology-code/sys-pattern-homework) � ���� � Github � ������������ ��� �� �������� ��� ������ �������, ��������, https://github.com/���-������-�����������/gitlab-hw ��� https://github.com/���-������-�����������/8-03-hw).
2. ��������� ������������ ����� ����������� � ���� �� �� � ������� ������� `git clone`.
3. ��������� �������� ������� � ��������� � ���� �������� ���� ���� README.md:
   - ������� ������ �������� ������� � ���� ������� � ���;
   - � ������ ������� �������� ������� � ��������� ����: �����/���/���������/������;
   - ��� ����������� ���������� ���������� �������������� ����������� [���� �������� �������� � ������ � ��������](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - ��� ���������� ����������� ����������� ����� �������� md. ������� �� ���� ����� ���������� � [���������� �� MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. ����� ���������� ������ ��� �������� �������� �������� ������ (`git commit -m "comment"`) � ��������� ��� �� Github (`git push origin`).
5. ��� �������� ��������� ������� �������������� � ������ �������� ���������� � ��������� ������ �� ������� � ���� md-����� � ����� Github.
6. ����� ������� ��������� � ���� ������� ������ �/��� � ������� �������� �� �������� � ������ ��������.

---

### ������� 1

���������� ��������� �� ������ � ��������� ��������� � ��������� ������� Keepalived. 

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

� �������� ������� ������������:
- ������� ������������ ����� ���, ����������� ��� ���� ���� � ����� md-�����;
- ��������� ������� ��������, �� ������� �����, ��� ���� ���� ������� � MASTER, � ������ � BACKUP state.

### �����:
1. ���� � 1:
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
2. ���� � 2:
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
![��������-1](https://github.com/Monooks/10-01_NetoHW/blob/main/img/10.01_1.1.png)

![��������-2](https://github.com/Monooks/10-01_NetoHW/blob/main/img/10.01_1.2.png)
---
## �������������� ������� �� ���������*

��� ������� ��������������. �� ����� �� ���������. �� ����� ��� �� ��������. �� ������ �� ���������, ���� ������ ������ ����������� � ���������.
 
### ������� 2*

��������� ������������ ������ ����, ����� ���� �� ����������� ��������. ��� �����:
- �������� ��� ���� ����������� ������ � �������� � � ����;
- �� ������ ���������� Wireshark � ��������� ������� ������������� ����������;
- ��������� ������� ping �� ����������� ����;
- ��������� ��������� �� ����� ���� (������), ���������� Wireshark;
- ������� ������ ICMP, � ������� ����� �������� ������� ��������� MAC-������ ����� ���� �� ������. 

 *�������� �������� �� � ����� ���������� ���������� �� Wireshark.*

### �����:
![��������-1](https://github.com/Monooks/10-01_NetoHW/blob/main/img/10.01_2.1.png)

![��������-2](https://github.com/Monooks/10-01_NetoHW/blob/main/img/10.01_2.2.png)