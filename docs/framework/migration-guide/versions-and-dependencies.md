---
title: "Версии и зависимости платформы .NET Framework | Microsoft Docs"
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
  - "версии, .NET Framework"
ms.assetid: f75a72de-e2f2-4a7a-9574-3f278684ea90
caps.latest.revision: 122
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 118
---
# Версии и зависимости платформы .NET Framework
В каждую версию платформы .NET Framework входит среда CLR, библиотеки базовых классов и другие управляемые библиотеки. В этом разделе описаны основные особенности различных версий платформы .NET Framework, приведены сведения о базовых версиях среды CLR и соответствующих средах разработки, а также указаны версии, устанавливаемые системой Windows.  
  
> [!NOTE]
>  Сведения о скачивании и установке платформы .NET Framework см. в разделе [Руководство по установке](../../../docs/framework/install/guide-for-developers.md).  
  
 В следующей таблице приводится краткий обзор истории версий .NET Framework и сопоставление каждой версии с Visual Studio, Windows и Windows Server. Обратите внимание, что Visual Studio предусматривает работу с различными версиями, поэтому вы не ограничены только указанной версией платформы .NET Framework.  
  
 В каждой новой версии платформы .NET Framework сохранены функции предыдущих версий и добавлены новые функции. Среда CLR определяется своим собственным номером версии. Номер версии платформы .NET Framework увеличивается при каждом выпуске, хотя версия среды CLR увеличивается не всегда. Например, в .NET Framework 4 и более поздние выпуски входит среда CLR 4, а в .NET Framework 2.0, 3.0 и 3.5 — среда CLR 2.0. \(Версии 3 среды CLR не было.\)  
  
 Полный список поддерживаемых операционных систем см. в разделе [Требования к системе](../../../docs/framework/get-started/system-requirements.md). Сведения о загрузке см. в [руководстве по установке](../../../docs/framework/install/guide-for-developers.md). Сведения об определении версий платформы .NET Framework, установленных на компьютере, см. в разделе [Практическое руководство.Определение установленных версий платформы .NET Framework](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md).  
  
 Версии платформы .NET Framework, установленные в версиях операционных систем, помеченные \* в столбцах **Включено в\/может быть установлено в Windows** и **Включено в\/может быть установлено в Windows Server**, необходимо [включить в панели управления](../../../docs/framework/install/net-framework-3-5-on-windows-8-plus.md) \(для Windows\) или с помощью диспетчера сервера \(для Windows Server\).  
  
|Версия платформы .NET Framework|Версия среды CLR|Функции|Включено в версию Visual Studio|✓ Включено в<br />\+ Может быть установлено в<br />Windows|✓ Включено в<br />\+ Может быть установлено в<br />Windows Server|Определение установленной версии .NET|  
|-------------------------------------|----------------------|-------------|-------------------------------------|--------------------------------------------------------|---------------------------------------------------------------|-------------------------------------------|  
|.NET 4.6.2|4|-   Улучшения криптографии, включая поддержку сертификатов X509, содержащих FIS 186 3 DSA, поддержку симметричного шифрования с помощью постоянных ключей, поддержку <xref:System.Security.Cryptography.Xml.SignedXml> для хеширования SHA\-2 и повышенный уровень четкости входных данных для подпрограмм формирования ключа ECDiffieHellman.<br />-   Для приложений Windows Presentation Foundation \(WPF\) — поддержка программируемой клавиатуры и DPI для каждого монитора.<br />-   Поддержка ClickOnce для протоколов TLS 1.1 и TLS 1.2.<br />-   Поддержка преобразования Windows Forms и приложений WPF в приложения UWP.||✓ Юбилейное обновление Windows 10 Anniversary Update<br /><br /> \+ Ноябрьское обновление Windows 10<br /><br /> \+ 10<br />\+ 8.1<br />\+ 7|\+ 2012 R2<br />\+ 2012<br />\+ 2008 R2 с пакетом обновления 1 \(SP1\)|Используйте DWORD `Release`:<br /><br /> -   394802 \(Юбилейное обновление Windows 10 Anniversary Update\)<br />-   394806 \(все другие версии ОС\)<br /><br /> \(см. [инструкции](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)\)|  
|Net 4.6.1|4|-   Поддержка сертификатов X509, содержащих ECDSA<br />-   Поддержка Always Encrypted \(всегда зашифрованы\) для аппаратно защищенных ключей в ADO.NET<br />-   Улучшения проверки орфографии в WPF<br />-   [Подробнее...](../../../docs/framework/whats-new/index.md)||✓ Ноябрьское обновление Windows 10<br /><br /> \+ 10<br />\+ 8.1<br />\+ 8<br />\+ 7|\+ 2012 R2<br />\+ 2012<br />\+ 2008 R2 с пакетом обновления 1 \(SP1\)|Используйте DWORD `Release`:<br /><br /> -   394254 \(ноябрьское обновление Windows 10\)<br />-   394271 \(все другие версии ОС\)<br /><br /> \(см. [инструкции](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)\)|  
|.NET 4.6|4|-   Компиляция с помощью .NET Native<br />-   ASP.NET Core 5<br />-   Усовершенствования трассировки событий<br />-   Поддержка кодировок страниц<br />-   [Подробнее...](../../../docs/framework/whats-new/index.md)|2015, хотя некоторые библиотеки .NET доступны на сайте [NuGet](https://www.nuget.org/). Для получения дополнительной информации см. [.NET Framework и внештатные выпуски](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md).|✓ 10<br />\+ 8.1<br />\+ 8<br />\+ 7<br />\+ Vista|\+ 2012 R2<br />\+ 2012<br />\+ 2008 R2 SP1<br />\+ 2008 SP2|Используйте DWORD `Release`:<br /><br /> -   393295 \(Windows 10\)<br />-   393297 \(все остальные версии ОС\)<br /><br /> \(см. [инструкции](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)\)|  
|4.5.2|4|-   Новые API для системы транзакций и ASP.NET<br />-   Системное DPI\-масштабирование в элементах управления Windows Forms<br />-   Усовершенствования профилирования<br />-   Усовершенствования ETW и ведения журналов нагрузки<br />-   [Подробнее...](../../../docs/framework/whats-new/index.md)|—|\+ 8.1<br />\+ 8<br />\+ 7<br />\+ Vista|\+ 2012 R2<br />\+ 2012<br />\+ 2008 R2 SP1<br />\+ 2008 SP2|Используйте DWORD `Release`: 379893<br />\(см. [инструкции](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)\)|  
|4.5.1|4|-   Поддержка приложений для Магазина Windows Phone<br />-   Автоматическое перенаправление привязки<br />-   Усовершенствования производительности и отладки<br />-   [Подробнее...](../../../docs/framework/whats-new/index.md)|2013|✓ 8.1<br />\+ 8<br />\+ 7<br />\+ Vista|✓ 2012 R2<br />\+ 2012<br />\+ 2008 R2 SP1<br />\+ 2008 SP2|Используйте DWORD `Release`:<br /><br /> -   378675 \(Windows 8.1\)<br />-   378758 \(все остальные\)<br /><br /> \(см. [инструкции](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)\)|  
|4.5|4|-   Поддержка приложений для Магазина Windows<br />-   Обновления WPF, WCF, WF, ASP.NET<br />-   [Подробнее...](../../../docs/framework/whats-new/index.md)|2012|✓ 8<br />\+ 7<br />\+ Vista|✓ 2012<br />\+ 2008 R2 SP1<br />\+ 2008 SP2|Используйте DWORD `Release`: 378389<br />\(см. [инструкции](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)\)|  
|4|4|-   Расширенные библиотеки базовых классов<br />-   Кроссплатформенная разработка с помощью переносимой библиотеки классов<br />-   Контракты для кода, платформы MEF, среды DLR<br />-   [Подробнее...](http://msdn.microsoft.com/library/ms171868\(v=vs.100\).aspx)|2010|\+ 7<br />\+ Vista|\+ 2008 R2 SP1<br />\+ 2008 SP2<br />\+ 2003|См. [инструкции](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)|  
|3.5|2.0|-   Веб\-сайты с поддержкой AJAX<br />-   LINQ<br />-   Динамические данные<br />-   [Подробнее...](http://msdn.microsoft.com/library/ms171868\(v=vs.90\).aspx)|2008|✓ 10✓ 8.1\*<br />✓ 8\*<br />✓ 7<br />\+ Vista|✓2008 R2 SP1\*<br />\+ 2012 R2<br />\+ 2012<br />\+ 2008 SP2<br />\+ 2003|См. [инструкции](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)|  
|3.0|2.0|-   WPF, WCF, WF, CardSpace|—|✓ Vista|✓ 2008 R2 SP1\*<br />✓ 2008 SP2\*<br />\+ 2003|См. [инструкции](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)|  
|2.0|2.0|-   Универсальные шаблоны<br />-   Добавления ASP.NET<br />-   [Подробнее...](http://msdn.microsoft.com/library/t357fb32\(v=vs.80\).aspx)|2005|—|✓ 2008 R2 SP1<br />✓ 2008 SP2<br />✓ 2003|См. [инструкции](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)|  
|1.1|1.1|-   Обновления ASP.NET и ADO.NET<br />-   Параллельное выполнение<br />-   [Подробнее...](http://msdn.microsoft.com/library/9wtde3k4\(v=vs.80\).aspx)|2003|—|✓ 2003|См. [инструкции](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)|  
|1,0|1,0|Первая версия .NET Framework.|Visual Studio .NET|—|—|См. [инструкции](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)|  
  
 Как правило, не требуется удалять какие\-либо версии .NET Framework, уже установленные на вашем компьютере, потому что используемое приложение может зависеть от конкретной версии. В случае удаления какой\-либо версии его исполнение может завершиться ошибкой. Можно загружать несколько версий платформы .NET Framework на одном компьютере одновременно. Это значит, что можно установить платформу .NET Framework без удаления предыдущих версий. Дополнительные сведения см. в разделе [Начало работы](../../../docs/framework/get-started/index.md).  
  
## Выбор целевой платформы и запуск приложений .NET Framework для версии 4.5 и более поздних  
 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] — это обновление на месте, которое заменяет [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] на компьютере, и аналогично [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] 4.5.2, 4.6, 4.6.1 и 4.6.2 — это обновления на месте для [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]. Это означает, что они используют ту же версию среды выполнения, но версии сборок обновлены и содержат новые типы и члены. После установки одного из этих обновлений приложения [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] и [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] должны продолжать работу без повторной компиляции. Однако обратное неверно. Не рекомендуется запускать приложения, нацеленные на более поздние версии .NET Framework, в более ранней версии .NET Framework. Например, не рекомендуется запускать приложение, предназначенное для [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], на [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]. Применяются следующие правила.  
  
-   В [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] можно выбрать [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] в качестве целевой платформы для проекта \(при этом задается свойство <xref:Microsoft.Build.Tasks.GetReferenceAssemblyPaths.TargetFrameworkMoniker%2A?displayProperty=fullName>\), чтобы компилировать проект как сборку или исполняемый файл [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]. Эту сборку или исполняемый файл можно использовать на любом компьютере, где установлена платформа [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], 4.5.1, 4.5.2, 4.6 или 4.6.1.  
  
-   В Visual Studio можно выбрать [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] в качестве целевой платформы для проекта \(при этом задается свойство <xref:Microsoft.Build.Tasks.GetReferenceAssemblyPaths.TargetFrameworkMoniker%2A?displayProperty=fullName>\), чтобы скомпилировать проект как сборку или исполняемый файл [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]. Эту сборку или исполняемый файл следует запускать только на компьютерах с установленной платформой [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] или более поздней версией. Исполняемый файл с целевой платформой [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] будет заблокирован для выполнения на компьютере, где установлена только более ранняя версия .NET Framework, например [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], и пользователю будет предложено установить версию [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]. Кроме того, сборки [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] не должны вызываться из приложения, предназначенного для более ранней версии .NET Framework, такой как [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  
  
     [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] и [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] используются здесь только в качестве примеров. Этот принцип применяется к любому приложению, предназначенному для более поздней версии .NET Framework, чем установленная в системе, в которой оно выполняется.  
  
 Некоторые изменения в платформе .NET Framework могут потребовать внесения изменений в код приложения. Ознакомьтесь с разделом [Совместимость приложений](../../../docs/framework/migration-guide/application-compatibility.md), прежде чем выполнять существующие приложения с использованием [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] или более поздних версий. Дополнительные сведения об установке текущей версии см. в разделе [Руководство по установке](../../../docs/framework/install/guide-for-developers.md). Дополнительные сведения о поддержке платформы .NET Framework см. на странице [Политика жизненного цикла поддержки платформы Microsoft .NET Framework](http://go.microsoft.com/fwlink/?LinkId=196607) веб\-сайта поддержки Майкрософт.  
  
## Выбор более старых версий в качестве целевой платформы и запуск приложений  
 Версии .NET Framework 2.0, 3.0 и 3.5 построены на базе одной и той же версии среды CLR \(CLR 2.0\). Эти версии представляют последовательные уровни единой установки. Каждая версия построена на базе предыдущих версий. Невозможно запустить версии 2.0, 3.0 и 3.5 параллельно на одном компьютере. При установке версии 3.5 автоматически создаются уровни версий 2.0 и 3.0, и приложения, созданные для версий 2.0, 3.0 и 3.5, могут выполняться в версии 3.5. Однако в .NET Framework 4 этот принцип "слоев" закончился. Начиная с .NET Framework 4, разработчики могут использовать внутрипроцессное параллельное размещение для запуска нескольких версий среды CLR в одном процессе. Для получения дополнительной информации см. [сборки и параллельное выполнение](../../../docs/framework/app-domains/assemblies-and-side-by-side-execution.md).  
  
 Кроме того, если в приложении выбрана целевая платформа версии 2.0, 3.0 или 3.5, пользователям может потребоваться включить .NET Framework 3.5 на компьютере с [!INCLUDE[win8](../../../includes/win8-md.md)] или [!INCLUDE[win81](../../../includes/win81-md.md)], прежде чем они смогут запустить это приложение. Для получения дополнительной информации см. [Установка платформы .NET Framework 3.5 в Windows 8 и более поздних версий](../../../docs/framework/install/net-framework-3-5-on-windows-8-plus.md).  
  
## Следующие шаги  
  
-   Если у вас отсутствует опыт работы с .NET Framework, [ознакомьтесь](../../../docs/framework/get-started/overview.md) с общими сведениями об этой платформе, основными понятиями и ключевыми функциями.  
  
-   Сведения о новых функциях и улучшениях в [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] и ее доработанных выпусках см. в разделе [Новые возможности](../../../docs/framework/whats-new/index.md).  
  
-   Сведения о миграции приложения с платформы .NET Framework 4 на [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] и ее доработанные выпуски см. в [руководстве по миграции](../Topic/Migration%20Guide%20to%20the%20.NET%20Framework%204.6%20and%204.5%20.md).  
  
-   Сведения о том, как определить, какие версии и обновления установлены на компьютере, см. в разделах [Практическое руководство.Определение установленных версий платформы .NET Framework](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md) и [Практическое руководство.Определение установленных обновлений платформы .NET Framework](../../../docs/framework/migration-guide/how-to-determine-which-net-framework-updates-are-installed.md).  
  
## См. также  
 [Совместимость версий](../../../docs/framework/migration-guide/version-compatibility.md)   
 [Политика жизненного цикла поддержки Microsoft .NET Framework](http://go.microsoft.com/fwlink/?LinkId=196607)   
 [Устранение неполадок](../../../docs/framework/install/troubleshoot-blocked-installations-and-uninstallations.md)