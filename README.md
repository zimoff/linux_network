### "Сети в Linux"

---

1. **Сети и маршрутизация:**  
   - Настроить две виртуальные машины (ws1 и ws2) с указанием сетевых параметров через конфигурационный файл `netplan`.  
   - Добавить статические маршруты вручную между машинами с помощью команды `ip r add`.  
   - Сохранить маршруты в конфигурации, чтобы они работали после перезагрузки.  
   - Проверить соединение между машинами с помощью команды `ping`.  

**Инструменты:**  
- **netplan** для настройки сетевых интерфейсов.  
- **ip** для работы с маршрутизацией.  
- **ping** для проверки соединения.  

---

2. **Сетевой экран:**  
   - Создать файлы фаервола для двух машин (ws1 и ws2) с использованием `iptables`.  
     - Для ws1 использовать стратегию, где сначала задаются запрещающие правила, а затем разрешающие.  
     - Для ws2 использовать стратегию, где сначала задаются разрешающие правила, а затем запрещающие.  
   - Настроить доступ для портов 22 (SSH) и 80 (HTTP).  
   - Запретить и разрешить *echo reply* (чтобы машина перестала и начала "пинговаться").  
   - Проверить работу фаервола с помощью команд `ping` и `nmap`.  

**Инструменты:**  
- **iptables** для создания и управления фаерволом.  
- **ping** для проверки доступности.  
- **nmap** для сканирования сети.  

---

3. **Маршрутизация сети:**  
   - Поднять сеть из пяти машин, включая три рабочие станции (ws11, ws21, ws22) и два маршрутизатора (r1, r2).  
   - Настроить IP-адреса для всех узлов через конфигурационный файл `netplan`.  
   - Включить IP-переадресацию на маршрутизаторах с помощью команды `sysctl -w net.ipv4.ip_forward=1`.  
   - Настроить маршруты по умолчанию для рабочих станций, добавив шлюз в конфигурацию `netplan`.  
   - Добавить статические маршруты на маршрутизаторы для обеспечения связи между всеми узлами.  
   - Проверить маршрутизацию между узлами с помощью команд `ping`, `tcpdump` и `traceroute`.  

**Инструменты:**  
- **netplan** для настройки сетевых интерфейсов.  
- **sysctl** для включения IP-переадресации.  
- **ping**, **tcpdump**, **traceroute** для проверки маршрутизации.  

---

4. **DHCP:**  
   - Настроить DHCP-сервер на маршрутизаторе r2 для автоматической выдачи IP-адресов рабочим станциям.  
     - Указать адрес маршрутизатора по умолчанию, диапазон выдаваемых IP-адресов и DNS-сервер.  
   - Настроить DHCP-сервер на маршрутизаторе r1 для статической выдачи IP-адресов по MAC-адресу.  
   - Проверить, что рабочие станции успешно получают IP-адреса через DHCP.  
   - Обновить IP-адреса рабочих станций вручную и проверить их изменения.  

**Инструменты:**  
- **isc-dhcp-server** для настройки DHCP-сервера.  
- **netplan** для настройки статических и динамических IP-адресов.  

---

5. **NAT:**  
   - Настроить веб-сервер Apache на одной из рабочих станций (ws22) для обработки запросов как из внутренней, так и из внешней сети.  
   - Добавить правила SNAT на маршрутизаторе r2 для маскировки исходящего трафика из внутренней сети.  
   - Добавить правила DNAT на маршрутизаторе r2 для перенаправления запросов на веб-сервер Apache.  
   - Проверить соединения с помощью команды `telnet` для SNAT и DNAT.  

**Инструменты:**  
- **iptables** для настройки SNAT и DNAT.  
- **Apache** для настройки веб-сервера.  
- **telnet** для проверки соединений.  

---

6. **SSH Tunnels:**  
   - Настроить веб-сервер Apache на ws22 так, чтобы он был доступен только через localhost.  
   - Настроить локальное TCP-перенаправление (Local TCP Forwarding) с ws21, чтобы обеспечить доступ к серверу на ws22.  
   - Настроить удалённое TCP-перенаправление (Remote TCP Forwarding) с ws11, чтобы обеспечить доступ к серверу на ws22.  
   - Проверить работу SSH-туннелей с помощью команды `telnet`.  

**Инструменты:**  
- **SSH** для настройки туннелей.  
- **Apache** для настройки веб-сервера.  
- **telnet** для проверки соединений через туннели.
