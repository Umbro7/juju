**БАЗОВЫЕ**



**tshark -r file.pcap -q -z io,phs**



**показывает статистику протоколов (что вообще есть в трафике)**



**tshark -r file.pcap**



**вывод всех пакетов подряд**



**tshark -r file.pcap -T fields -e ip.src -e ip.dst | sort | uniq**



**список уникальных IP (кто с кем общался)**





**IP / СОЕДИНЕНИЯ**

**tshark -r file.pcap -q -z conv,ip**



**все соединения IP ↔ IP**



**tshark -r file.pcap -q -z conv,tcp**





**TCP соединения**



**tshark -r file.pcap -q -z conv,udp**





**UDP соединения**



**tshark -r file.pcap -Y "ip.addr == X.X.X.X"**



**фильтр по конкретному IP**







**DNS**

**tshark -r file.pcap -Y "dns"**



**весь DNS трафик**



**tshark -r file.pcap -Y "dns" -T fields -e dns.qry.name**



**только домены**



**... | sort | uniq**



**уникальные домены**



**dns.qry.name.len > 50**



**длинные домены (возможный туннель)**



**-Y "dns.a"**





**IP-ответы DNS**





**HTTP**

**tshark -r file.pcap -Y "http.request"**





**HTTP запросы**



**-e http.host -e http.request.uri**





**URL (куда шли)**



**http.request.method == POST**





**POST (часто данные/пароли)**



**-e http.user\_agent**



&#x20;**какой клиент/бот**



**http contains password**



&#x20;**поиск паролей**





***TLS***

**tshark -r file.pcap -Y "tls"**





**HTTPS трафик**



**-e tls.handshake.extensions\_server\_name**



**домен (SNI)**



**-Y "x509sat.printableString"**



**данные сертификата**





**STREAMS**

**-e tcp.stream**



**список соединений (ID)**



**tcp.stream == 5**



**конкретное соединение**



**-z follow,tcp,ascii,5**



**восстановить переписку (очень важно)**





**ЭКСФИЛЬТРАЦИЯ**

**tcp.len > 1000**



**большие пакеты (утечка данных)**



**-e http.file\_data**



**данные POST**



**strings file.pcap | grep base64**



**поиск закодированных данных**





**STRINGS**

**strings file.pcap**



**все читаемые строки**



**grep -i password**



**поиск паролей**



**grep -i flag**



**поиск флага**



**grep http**



&#x20;**поиск ссылок**





**BINWALK**

**binwalk file.pcap**



&#x20;**ищет встроенные файлы**



**binwalk -e file.pcap**



&#x20;**извлекает их**





