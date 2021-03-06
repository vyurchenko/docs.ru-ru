---
title: "Настройка HTTP и HTTPS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "настройка HTTP [WCF]"
ms.assetid: b0c29a86-bc0c-41b3-bc1e-4eb5bb5714d4
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Настройка HTTP и HTTPS
Службы и клиенты WCF могут взаимодействовать по протоколам HTTP и HTTPS.  Параметры HTTP\/HTTPS задаются с помощью служб IIS или посредством использования средства командной строки.  Когда служба WCF размещается в службах IIS, параметры HTTP или HTTPS можно задать в службах IIS \(с помощью средства inetmgr.exe\).  Если служба WCF является резидентной, параметры HTTP или HTTPS задаются с помощью средства командной строки.  
  
 Понадобится как минимум настроить регистрацию URL\-адресов и добавить исключение брандмауэра для URL\-адреса, который будет использовать служба.  
  
 Выбор средства настройки параметров HTTP зависит от операционной системы компьютера.  
  
 При работе в [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] или [!INCLUDE[wxp](../../../../includes/wxp-md.md)] следует использовать средство HttpCfg.exe.  [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] автоматически устанавливает этот инструмент.  При работе в [!INCLUDE[wxp](../../../../includes/wxp-md.md)] средство можно загрузить на странице [Средства поддержки Windows XP с пакетом обновления 2 \(SP2\)](http://go.microsoft.com/fwlink/?LinkId=88606).  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Обзор Httpcfg](http://go.microsoft.com/fwlink/?LinkId=88605).  
  
 При работе в [!INCLUDE[wv](../../../../includes/wv-md.md)] или Windows 7 эти параметры можно задать с помощью средства Netsh.exe.  
  
## Настройка резервирований пространства имен  
 Резервирование пространства имен назначает права на часть пространства имен URL\-адреса HTTP определенной группе пользователей.  Резервирование предоставляет этим пользователям право создавать службы, которые ожидают передачи данных в указанной части пространства имен.  Резервирования представляют собой URL\-префиксы, а это значит, что одно резервирование охватывает все подпути пути резервирования.  Резервирования пространства имен позволяют использовать подстановочные знаки двумя способами.  В документации по API HTTP\-сервера описывается [порядок разрешения утверждений пространства имен, включающих подстановочные знаки](http://go.microsoft.com/fwlink/?LinkId=94841).  
  
 Запущенное приложение может создать аналогичный запрос для добавления регистраций пространства имен.  Регистрации и резервирования конкурируют за части пространства имен.  Резервирование может иметь приоритет над регистрацией в соответствии с порядком разрешения, описанным в разделе [порядок разрешения утверждений пространства имен, включающих подстановочные знаки](http://go.microsoft.com/fwlink/?LinkId=94841).  В этом случае резервирование не позволяет запущенному приложению получать запросы.  
  
### Запуск Windows XP или Server 2003.  
 Используйте команду `httpcfg.exe set urlacl` для изменения резервирований пространства имен.  В [документации по средствам поддержки Windows](http://go.microsoft.com/fwlink/?LinkId=94840) описывается синтаксис средства Httpcfg.exe.  Для изменения прав резервирования для части пространства имен необходимо обладать привилегиями администратора или владеть соответствующей частью пространства имен.  Первоначально все пространство имен HTTP принадлежит локальному администратору.  
  
 Ниже приведен синтаксис команды Httpcfg с параметром `set urlacl`.  
  
```  
httpcfg set urlacl /u {http://URL:Port/ | https://URL:Port/} /aACL  
  
```  
  
 При использовании `/u` требуется параметр `set urlacl`.  Он использует строку, которая содержит полный URL\-адрес, выполняющий функции ключа записи для выполняемого резервирования.  
  
 При использовании `/a` также требуется параметр `set urlacl`.  Он использует строку, содержащую список управления доступом \(ACL\) в форме строки SDDL \(Security Descriptor Definition Language\).  
  
 Ниже приведен пример использования этой команды.  
  
```  
httpcfg.exe set urlacl /u http://myhost:8000/ /a "O:AOG:DAD:(A;;RPWPCCDCLCSWRCWDWOGA;;;S-1-0-0)"  
  
```  
  
### Работа в Windows Vista, Windows Server 2008 R2 или Windows 7  
 При работе в [!INCLUDE[wv](../../../../includes/wv-md.md)], Windows Server 2008 R2 или Windows 7 используйте средство Netsh.exe.  Ниже приведен пример использования этой команды.  
  
```  
netsh http add urlacl url=http://+:80/MyUri user=DOMAIN\user  
  
```  
  
 Эта команда добавляет резервирование URL\-адресов для указанного пространства имен URL\-адреса для DOMAIN\\учетной записи пользователя.  Для дополнительных сведений об использовании команды netsh введите «netsh http add urlacl» в командной строке и нажмите клавишу ВВОД.  
  
## Настройка исключения брандмауэра  
 При резидентном размещении службы WCF, которая осуществляет взаимодействие по протоколу HTTP, необходимо добавить исключение в конфигурацию брандмауэра, чтобы входящие соединения могли использовать определенный URL\-адрес.  Дополнительные сведения см. в разделе [Открытие портов в брандмауэре Windows \(Windows 7\)](http://go.microsoft.com/fwlink/?LinkId=239961).  
  
## Настройка SSL\-сертификатов  
 Протокол SSL использует сертификаты в клиенте и службе для хранения ключей шифрования.  Сервер предоставляет свой SSL\-сертификат при подключении, чтобы клиент мог проверить удостоверение сервера.  Для обеспечения взаимной проверки на обеих сторонах подключения сервер также запрашивает сертификат у клиента.  
  
 Сертификаты хранятся в централизованном хранилище в соответствии с IP\-адресом и номером порта подключения.  Специальный IP\-адрес 0.0.0.0 соответствует любому IP\-адресу локального компьютера.  Обратите внимание, что хранилище сертификатов не различает URL\-адреса по пути.  Службы с одним и тем же сочетанием IP\-адреса и порта должны иметь общие сертификаты, даже если их пути в URL\-адресе различаются.  
  
 Пошаговые инструкции см. в разделе [Практическое руководство. Настройка порта с использованием SSL\-сертификата](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md).  
  
## Настройка списка ожидания передачи данных по протоколу IP  
 API HTTP\-сервера привязывается к IP\-адресу и порту только после регистрации URL\-адреса пользователем.  По умолчанию API HTTP\-сервера привязывается к порту в URL\-адресе для всех IP\-адресов компьютера.  Если приложение, не использующее API HTTP\-сервера, ранее привязалось к этому сочетанию IP\-адреса и порта, возникает конфликт.  Список ожидания передачи данных по протоколу IP позволяет службам [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] совместно существовать с приложениями, которые используют порт для некоторых IP\-адресов компьютера.  Если в списке ожидания передачи данных по протоколу IP содержатся какие\-либо записи, API HTTP\-сервера привязывается только к IP\-адресам, указанным в списке.  Для изменения списка ожидания передачи данных по протоколу IP требуются привилегии администратора.  
  
### Запуск Windows XP или Server 2003.  
 Для изменения списка ожидания передачи данных по протоколу IP используйте средство httpcfg, как показано в следующем примере.  В [документации по средствам поддержки Windows](http://go.microsoft.com/fwlink/?LinkId=94840) описывается синтаксис средства httpcfg.exe.  
  
```  
httpcfg.exe set iplisten -i 0.0.0.0:8000  
```  
  
### Работа в Windows Vista или Windows 7  
 Для изменения списка ожидания передачи данных по протоколу IP используйте средство netsh, как показано в следующем примере.  
  
```  
netsh http add iplisten ipaddress=0.0.0.0:8000  
```  
  
## Другие параметры конфигурации  
 При работе с привязкой <xref:System.ServiceModel.WsDualHttpBinding> клиентское соединение использует значения по умолчанию, совместимые с резервированием пространства имен и брандмауэром Windows.  При необходимости настроить базовый адрес клиента для двустороннего соединения, необходимо, кроме того, настроить эти параметры HTTP в клиенте так, чтобы они соответствовали новому адресу.  
  
 API HTTP\-сервера имеет некоторые дополнительные параметры конфигурации, которые не доступны через HttpCfg.  Эти параметры сохраняются в реестре и применяются ко всем приложениям, выполняемым в системах, которые используют API HTTP\-сервера.  Информацию об этих параметрах см. в разделе [Параметры реестра Http.sys для служб IIS](http://go.microsoft.com/fwlink/?LinkId=94843).  В большинстве случаев пользователям не нужно изменять эти параметры.  
  
## Проблемы, возникающие при работе с Windows XP  
 Службы IIS не поддерживают совместное использование портов в [!INCLUDE[wxp](../../../../includes/wxp-md.md)].  Если служба [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] предпринимает попытку использовать пространство имен с тем же портом при выполняемых службах IIS, происходит сбой запуска службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  По умолчанию как IIS, так и [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] используют порт 80.  Необходимо либо изменить назначение порта для одной из служб, либо назначить службу [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] сетевому адаптеру, не используемому службами IIS, с помощью списка ожидания передачи данных по протоколу IP.  Службы IIS 6.0 и более поздних версий были переработаны для использования API HTTP\-сервера.  
  
## См. также  
 <xref:System.ServiceModel.WsDualHttpBinding>   
 [Практическое руководство. Настройка порта с использованием SSL\-сертификата](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)