---
title: "Модели сетевого взаимодействия"
authors:
  - igsekor
contributors:
  - furtivite
keywords:
  - OSI
  - DOD
  - TCP/IP
  - IPX/SPX
tags:
  - article
---

## Кратко

На заре создания компьютерных сетей были разработаны модели взаимодействия сетевых устройств, которые описывали программную и аппаратную реализации. Среди разработанных моделей наибольшее распространение получили:

- Сетевая модель OSI (Open Systems Interconnection).
- Модель DOD (Семейство TCP/IP).
- Модель SPX/IPX.

Сетевая модель — это описание принципов работы протоколов сетевого взаимодействия, спецификация которых закреплена в стандартах связи и используется для передачи _данных в цифровом виде_.

## Сетевая модель OSI

Для того чтобы корректно описать совместную работу сетевых устройств необходимо рассмотреть разные аспекты организации связи между ними. Модель OSI разбивает систему построения связи между сетевыми устройствами на уровни:

1. Физический.
2. Канальный.
3. Сетевой.
4. Транспортный.
5. Сеансовый.
6. Представления.
7. Прикладной.

Первые три уровня описывают среду передачи данных.

### Физический уровень

Физический уровень (physical layer) отвечает за аппаратную реализацию передачи битов информации, то есть обеспечивает работу физических устройств: сетевых адаптеров, концентраторов, повторителей, медиаконвертеров (устройств для преобразования сигнала при переходе из сети с одной средой передачи данных в сеть с другой средой).

На физическом уровне рассматривают среды передачи данных: последовательный или параллельный порт, коаксиальный кабель, витая пара, радиоканал, оптоволокно, спутниковый интернет и т.д. Для передачи данных на физическом уровне существуют свои протоколы, то есть правила, по которым должен быть преобразован и передан сигнал с данными. Вы наверняка встречались с такими протоколами: IEEE 802.15 (Bluetooth), 802.11 Wi-Fi, GSM, DSL.

### Канальный уровень

Канальный уровень (data link layer) используется для организации передачи данных по сети между устройствами и для контроля ошибок целостности данных. Если на физическом уровне обеспечивается передача битов информации, то на канальном — передача [кадров (фреймов)](https://ru.wikipedia.org/wiki/Кадр_(телекоммуникации)).

Каждый кадр позволяет передать 1446 байтов информации и содержит кроме служебной информации контрольную сумму кадра — [хэш-сумма](https://ru.wikipedia.org/wiki/Контрольная_сумма), которая рассчитывается по данным перед передачей и после передачи позволяет проверить сохранность данных. После получения хэш-сумма вновь рассчитывается по пришедшим данным и должна совпасть с той, которая передаётся в кадре. Если совпадает, можно считать, что данные переданы верно.

### Сетевой уровень

Сетевой уровень (network layer) позволяет прокладывать путь данных по сети от одного сетевого устройства к другому, то есть определяет маршрут.

Маршрутизация — важная составляющая работы сети. Существуют даже специальные устройства — маршрутизаторы. Наиболее известный разработчикам протокол сетевого уровня — это [IP (Internet Protocol)](https://ru.wikipedia.org/wiki/Internet_Protocol). Он позволяет переправить пакеты от одного сетевого устройства к другому. Пакеты — это контейнеры для данных, реализованные уже не на физическом уровне, как кадры, а на программном. Протокол IP не гарантирует соответствия порядка при доставке пакетов изначальному порядку во время отправки, не гарантирует он и то, что пакеты будут доставлены или не будут продублированы. За это отвечают протоколы более высоких уровней.

Создатели интернета спроектировали работу сетевых устройств как распределённой системы. Работу такой системы очень сложно парализовать. Путь внутри сети определяется для каждого пакета отдельно. Такая архитектура системы сложна, но обеспечивает устойчивое взаимодействие устройств, которые соединены любым образом в единую сеть.

### Транспортный уровень

Транспортный уровень (transport layer) обеспечивает необходимую целостность данных и выстраивает пакеты в правильный порядок.

Веб-разработчикам чаще всего приходится сталкиваться с протоколами TCP и UDP. TCP используется для данных, целостность и порядок которых должны быть гарантированы, UDP — для данных, целостность которых важна только в конкретный момент времени внутри небольшого блока.

Вы наверняка знакомы с подёргиванием видео или небольшими прерываниями звука, если пользовались потоковыми сервисами (например, YouTube, Apple Music, Spotify и другими), которые используют под капотом в основном UDP. Зато, когда загружается страничка какого-то сайта, потерь нет. Это как раз проверка целостности на уровне протокола TCP.

### Сеансовый уровень

Сеансовый уровень (session layer) позволяет организовать сеанс связи между устройствами сети. Это необходимо для работы приложений.

Вы можете знать протокол [RPC](/js/api/#rpc) (Remote Procedure Call Protocol — удалённый вызов процедур), если пользовались API на его основе (например, JSON-RPC, GraphQL или gRPC). Однако более распространённый протокол PPTP (Point-to-Point Tunneling Protocol) менее известен широкой аудитории, при этом используется он, например, для организации работы VPN (Virtual Private Network), обеспечивая туннель между компьютером и локальной сетью, имеющей подключение к интернету.

### Уровень представления

Уровень представления (presentation layer) служит для организации преобразования данных (кодирования и декодирования), преобразования протоколов и прочих служебных задач высокого уровня.

С помощью протоколов этого уровня данные в форматах, которые используются на более низких уровнях, преобразуются к формату, который подходит для работы приложений. На этом уровне появляются абстракции представления данных — форматы и структуры данных, что позволяет подготовить данные к пересылке по сети и произвести обратное преобразование.

Например, преобразование изображений от битов, которые путешествуют по сети, к форматам типа JPEG или TIFF происходит именно на этом уровне.

### Прикладной уровень

Прикладной уровень (application layer) — уровень приложений, то есть уровень, который обеспечивает максимальный уровень абстракции данных.

Протоколы прикладного уровня вам наверняка знакомы: HTTP, SMTP, POP3, FTP, SIP, TELNET и другие. Использование сетевых служб (доступ к файлам и базам данных, пересылка электронной почты) позволяет приложениям на разных сетевых устройствах взаимодействовать друг с другом.

## Другие модели

Безусловно модель OSI очень сложна и не раз подвергалась критике. В то же время эта модель предоставляет наиболее полное представление о том, как передаются данные по сети — от физической среды для передачи данных до особенностей организаций данных в специальные структуры, форматы и системы.

Иногда из модели OSI выделяют несколько уровней или отдельные семейства протоколов, которые могут использоваться для конкретных практических задач на программном уровне, в отрыве от конкретной на уровне аппаратной реализации. Примером могут служить модели [DOD](https://ru.wikipedia.org/wiki/TCP/IP), [IPX/SPX](https://ru.wikipedia.org/wiki/IPX/SPX) или [AppleTalk](https://ru.wikipedia.org/wiki/AppleTalk). Но это удобно лишь с практической точки зрения: отсечь всё лишнее, чтобы вести разработку программного обеспечения наиболее эффективным способом.

Модель TCP/IP разрабатывалась для описания протоколов передачи данных в распределённых сетях и использовалась при проектировании оборудования и создания программного обеспечения для прообраза современного интернета. Четыре уровня этой модели соответствуют семи уровням модели OSI следующим образом:

1. Уровень сетевого доступа TCP/IP (Network Access Layer) включает:
    - Физический уровень OSI.
    - Канальный уровень OSI.
2. Межсетевой уровень TCP/IP (Internet Layer) соответствует:
    - Сетевому уровню OSI.
3. Транспортный уровень TCP/IP (Transport Layer) соответствует:
    - Транспортному уровню OSI.
4. Прикладной уровень TCP/IP (Application layer) включает:
    - Прикладной уровень OSI.
    - Представления уровень OSI.
    - Сеансовый уровень OSI.

Модель IPX/SPX была разработана изначально для организации сетей в операционной системе DOS. Протоколы IPX для маршрутизации и SPX для передачи данных были широко распространены в 90-х годах прошлого века, а потом уступили пальму первенства стеку TCP/IP, поскольку не обладали достаточной эффективностью при передаче данных в глобальных сетях. Сейчас количество операционных систем, в которых реализован стек протоколов IPX/SPX стремительно сокращается. Модель IPX/SPX использует три уровня, аналогичных модели OSI:

1. Сетевой.
2. Транспортный.
3. Сеансовый.
