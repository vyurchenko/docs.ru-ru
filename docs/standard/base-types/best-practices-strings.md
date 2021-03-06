---
title: "Рекомендации по использованию строк в .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "рекомендации, сравнение и сортировка строк"
  - "сравнение строк"
  - "сортировка строк"
  - "сравнение строк [платформа .NET Framework], рекомендации"
  - "сортировка по строкам"
  - "строки [платформа .NET Framework], основные операции со строками"
  - "строки [платформа .NET Framework], рекомендации"
  - "строки [платформа .NET Framework], сравнение"
  - "строки [платформа .NET Framework], поиск"
  - "строки [платформа .NET Framework], сортировка"
ms.assetid: b9f0bf53-e2de-4116-8ce9-d4f91a1df4f7
caps.latest.revision: 35
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 35
---
# Рекомендации по использованию строк в .NET Framework
<a name="top"></a> Платформа .NET Framework предоставляет расширенную поддержку разработки локализованных и глобализованных приложений и упрощает применение правил текущего или какого\-то определенного языка и региональных параметров при выполнении общих операций, таких как сортировка строк и их отображение. Однако сортировка и сравнение строк не всегда выполняется с учетом языка и региональных параметров. Например, строки, которые используются внутри приложения, как правило, должны обрабатываться одинаково независимо от выбранного языка и региональных параметров. Если независимые от языка и региональных параметров строковые данные, такие как теги XML, теги HTML, имена пользователей, пути к файлам и имена системных объектов, интерпретируются как зависимые от языка и региональных параметров, в коде приложения могут возникать незначительные ошибки, может наблюдаться низкая производительность, а в некоторых случаях и проблемы безопасности.  
  
 В этом разделе рассматриваются методы сортировки, сравнения строк и использования прописных и строчных букв в .NET Framework, представлены рекомендации по выбору подходящего метода обработки строк и дополнительная информация об этих методах. Кроме того, рассматривается отображение и хранение форматированных данных, например числовых данных или даты и времени.  
  
 В этом разделе содержатся следующие подразделы.  
  
-   [Рекомендации по использованию строк](#recommendations_for_string_usage)  
  
-   [Явное задание сравнений строк](#specifying_string_comparisons_explicitly)  
  
-   [Подробные сведения о сравнении строк](#the_details_of_string_comparison)  
  
-   [Выбор элемента StringComparison для своего вызова метода](#choosing_a_stringcomparison_member_for_your_method_call)  
  
-   [Общие методы сравнения строк в .NET Framework](#common_string_comparison_methods_in_the_net_framework)  
  
-   [Методы, выполняющие сравнение строк опосредованно](#methods_that_perform_string_comparison_indirectly)  
  
-   [Отображение и сохранение форматированных данных](#Formatted)  
  
<a name="recommendations_for_string_usage"></a>   
## Рекомендации по использованию строк  
 Если вы выполняете разработку на платформе .NET Framework, следуйте нескольким простым рекомендациям по работе со строками.  
  
-   Используйте перегрузки, которые явно задают правила сравнения строк для операций со строками. Как правило, это подразумевает вызов перегрузки метода, который имеет параметр типа <xref:System.StringComparison>.  
  
-   Используйте <xref:System.StringComparison?displayProperty=fullName> или <xref:System.StringComparison?displayProperty=fullName> для сравнений в качестве безопасной альтернативы по умолчанию для сопоставления строк независимо от языка и региональных параметров.  
  
-   Используйте сравнения с <xref:System.StringComparison?displayProperty=fullName> или <xref:System.StringComparison?displayProperty=fullName> для повышения производительности.  
  
-   Используйте строковые операции, основанные на <xref:System.StringComparison?displayProperty=fullName>, при отображении выходных данных пользователю.  
  
-   Используйте нелингвистические значения <xref:System.StringComparison?displayProperty=fullName> или <xref:System.StringComparison?displayProperty=fullName> вместо строковых операций на основе <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>, если лингвистические аспекты в сравнении не важны \(например, выполняется сравнение символов\).  
  
-   Используйте метод <xref:System.String.ToUpperInvariant%2A?displayProperty=fullName> вместо <xref:System.String.ToLowerInvariant%2A?displayProperty=fullName> при нормализации строк для сравнения.  
  
-   Используйте перегрузку метода <xref:System.String.Equals%2A?displayProperty=fullName> для проверки равенства двух строк.  
  
-   Используйте методы <xref:System.String.Compare%2A?displayProperty=fullName> и <xref:System.String.CompareTo%2A?displayProperty=fullName> для сортировки строк, но не для проверки их равенства.  
  
-   Используйте форматирование с учетом языка и региональных параметров для отображения нестроковых данных, например чисел и дат, в пользовательском интерфейсе. Для сохранения нестроковых данных в строковой форме используйте форматирование инвариантного языка и региональных параметров.  
  
 При использовании строк избегайте следующих действий.  
  
-   Не используйте перегрузки, которые не задают правила сравнения строк для операций со строками в явной или неявной форме.  
  
-   В большинстве случаев не стоит использовать строковые операции, основанные на <xref:System.StringComparison?displayProperty=fullName>. Одним из немногочисленных исключений является случай сохранения лингвистически значимых данных, которые, тем не менее, не зависят от языка и региональных параметров.  
  
-   Не используйте перегрузку метода <xref:System.String.Compare%2A?displayProperty=fullName> или <xref:System.String.CompareTo%2A> и проверяйте возвращаемое значение \(ноль\), чтобы определить, равны ли строки.  
  
-   Не используйте форматирование с учетом языка и региональных параметров для сохранения числовых данных или данных даты и времени в виде строки.  
  
 [К началу](#top)  
  
<a name="specifying_string_comparisons_explicitly"></a>   
## Явное задание сравнений строк  
 Большинство методов обработки строк в.NET Framework являются перегруженными. Как правило, одна или несколько перегрузок принимают настройки по умолчанию, а другие — нет и вместо этого определяют требуемый точный способ сравнения и обработки строк. Большинство методов, не использующих значения по умолчанию, включают параметр типа <xref:System.StringComparison>, который представляет собой перечисление, явно задающее правила сравнения строк по языку, региональным параметрам и регистру. В следующей таблице описаны элементы перечисления <xref:System.StringComparison>.  
  
|Элемент StringComparison|Описание|  
|------------------------------|--------------|  
|<xref:System.StringComparison>|Выполняет сравнение с учетом регистра, используя текущий язык и региональные параметры.|  
|<xref:System.StringComparison>|Выполняет сравнение без учета регистра, используя текущий язык и региональные параметры.|  
|<xref:System.StringComparison>|Выполняет сравнение с учетом регистра, используя инвариантный язык и региональные параметры.|  
|<xref:System.StringComparison>|Выполняет сравнение без учета регистра, используя инвариантный язык и региональные параметры.|  
|<xref:System.StringComparison>|Выполняет порядковое сравнение.|  
|<xref:System.StringComparison>|Выполняет порядковое сравнение без учета регистра.|  
  
 Например, метод <xref:System.String.IndexOf%2A>, который возвращает индекс подстроки в объект <xref:System.String>, соответствующий символу или строке, имеет девять перегрузок.  
  
-   <xref:System.String.IndexOf%28System.Char%29>, <xref:System.String.IndexOf%28System.Char%2CSystem.Int32%29>, и <xref:System.String.IndexOf%28System.Char%2CSystem.Int32%2CSystem.Int32%29>, которые по умолчанию выполняют порядковый поиск символа в строке \(с учетом регистра и без учета языка и региональных параметров\).  
  
-   Методы <xref:System.String.IndexOf%28System.String%29>, <xref:System.String.IndexOf%28System.String%2CSystem.Int32%29> и <xref:System.String.IndexOf%28System.String%2CSystem.Int32%2CSystem.Int32%29>, которые по умолчанию выполняют поиск подстроки в строке с учетом регистра, языка и региональных параметров.  
  
-   Методы <xref:System.String.IndexOf%28System.String%2CSystem.StringComparison%29>, <xref:System.String.IndexOf%28System.String%2CSystem.Int32%2CSystem.StringComparison%29> и <xref:System.String.IndexOf%28System.String%2CSystem.Int32%2CSystem.Int32%2CSystem.StringComparison%29>, которые включают параметр типа <xref:System.StringComparison>, что позволяет задать форму сравнения.  
  
 Рекомендуется выбрать перегрузку, не использующую значения по умолчанию, по следующим причинам.  
  
-   Некоторые перегрузки с параметрами по умолчанию \(те, которые выполняют поиск <xref:System.Char> в экземпляре строки\) выполняют порядковое сравнение, в то время как другие \(выполняющие поиск строки в экземпляре строки\) учитывают язык и региональные параметры. Сложно запомнить, какое значение по умолчанию использует тот или иной метод, перегрузки легко перепутать.  
  
-   Назначение кода, вызовы методов в котором зависят от значений по умолчанию, не ясно. В следующем примере, где используются значения по умолчанию, сложно определить, действительно ли разработчик намеревался выполнить порядковое или лингвистическое сравнение двух строк или различие регистра между `protocol` и http могло привести к тому, что проверка на равенство возвратит значение `false`.  
  
     [!code-csharp[Conceptual.Strings.BestPractices#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/explicitargs1.cs#1)]
     [!code-vb[Conceptual.Strings.BestPractices#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/explicitargs1.vb#1)]  
  
 В общем случае рекомендуется вызывать метод, который не зависит от значений по умолчанию, поскольку это делает назначение кода однозначным. Это, в свою очередь, делает код более читаемым и упрощает отладку и обслуживание. В следующем примере рассматриваются вопросы, возникшие в предыдущем примере. Он явно демонстрирует, что используется порядковое сравнение и что различия регистра игнорируются.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/explicitargs1.cs#2)]
 [!code-vb[Conceptual.Strings.BestPractices#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/explicitargs1.vb#2)]  
  
 [К началу](#top)  
  
<a name="the_details_of_string_comparison"></a>   
## Подробные сведения о сравнении строк  
 Сравнение строк является основой многих связанных со строками операций, в частности сортировки и проверки на равенство. Строки сортируются в определенном порядке: если my отображается до string в сортированном списке строк, текст my должен быть меньше или равен тексту string. Кроме того, неявное сравнение определяет равенство. Операция сравнения возвращает 0 для строк, которые она считает равными. Правильно интерпретировать это следующим образом: ни одна из строк не меньше другой. Наиболее значимые операции со строками включают обе следующие процедуры или хотя бы одну из них: сравнение с другой строкой и выполнение правильно определенной операции сортировки.  
  
 Однако оценка двух строк на равенство или порядок сортировки не дает единственно верного результата; результат также зависит от критериев, используемых для сравнения строк. В частности, операции сравнения строк, которые являются порядковыми или основаны на правилах учета регистра или сортировки текущего языка и региональных параметров или инвариантного языка и региональных параметров \(независимые от языкового стандарта региональные параметры на основе английского языка\), могут давать разные результаты.  
  
<a name="current_culture"></a>   
### Сравнение строк с использованием текущего языка и региональных параметров  
 Одним из критериев является использование правил текущего языка и региональных параметров при сравнении строк. В сравнениях, основанных на текущем языке и региональных параметрах, используется текущий язык, региональные параметры или языковой стандарт потока. Если пользователь не задал язык и региональные параметры, используется настройка по умолчанию в окне **Региональные параметры** на панели управления. Следует всегда использовать сравнения на основе текущего языка и региональных параметров, если речь идет о лингвистически релевантных данных и данных, отражающих взаимодействие с пользователем, где важны язык и региональные параметры.  
  
 Однако поведение сравнения и использования регистра в .NET Framework меняется при изменении языка и региональных параметров. Это происходит, если приложение выполняется на компьютере с другим языком и региональными параметрами, нежели на компьютере, где приложение было разработано, либо если выполняющий поток меняет свой язык и региональные параметры. Это поведение является преднамеренным, однако до сих пор остается неочевидным для многих разработчиков. В следующем примере показаны различия в порядке сортировки в американском английском \(en\-US\) и шведском языке \(sv\-SE\). Обратите внимание, что слова ångström, Windows и Visual Studio показаны в разных местах массива сортированных строк.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison1.cs#3)]
 [!code-vb[Conceptual.Strings.BestPractices#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison1.vb#3)]  
  
 Сравнения без учета регистра, где используются текущий язык и региональные параметры, выполняются так же, как сравнения с учетом языка и региональных параметров с той разницей, что регистр игнорируется в соответствии с правилами текущего языка и региональных параметров потока. Это поведение может также проявляться в порядке сортировки.  
  
 Сравнения, использующие семантику текущего языка и региональных параметров, используются по умолчанию для следующих методов.  
  
-   Перегрузки <xref:System.String.Compare%2A?displayProperty=fullName>, не включающие параметр <xref:System.StringComparison>.  
  
-   Перегрузки <xref:System.String.CompareTo%2A?displayProperty=fullName>.  
  
-   Метод по умолчанию <xref:System.String.StartsWith%28System.String%29?displayProperty=fullName> и метод <xref:System.String.StartsWith%28System.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=fullName> с параметром <xref:System.Globalization.CultureInfo>, который имеет значение `null`.  
  
-   Метод по умолчанию <xref:System.String.EndsWith%28System.String%29?displayProperty=fullName> и метод <xref:System.String.EndsWith%28System.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=fullName> с параметром <xref:System.Globalization.CultureInfo>, который имеет значение `null`.  
  
-   Перегрузки <xref:System.String.IndexOf%2A?displayProperty=fullName>, принимающие в качестве параметра поиска <xref:System.String> и не имеющие параметра <xref:System.StringComparison>.  
  
-   Перегрузки <xref:System.String.LastIndexOf%2A?displayProperty=fullName>, принимающие в качестве параметра поиска <xref:System.String> и не имеющие параметра <xref:System.StringComparison>.  
  
 В любом случае рекомендуется вызвать перегрузку, имеющую параметр <xref:System.StringComparison>, чтобы сделать назначение вызова метода очевидным.  
  
 При лингвистической интерпретации нелингвистических строковых данных, а также если строковые данные определенного языка и региональных параметров интерпретируются с использованием правил другого языка, могут возникать малозаметные и не столь малозаметные ошибки. Типичный пример — проблема турецкого I.  
  
 Почти во всех латинских алфавитах, включая американский английский, символ i \(\\u0069\) является строчной версией символа I \(\\u0049\). Это правило учета регистра быстро становится значением по умолчанию для тех, кто программирует для этих языков. Однако в турецком алфавите \(tr\-TR\) используется I с точкой — İ \(\\u0130\), которая является прописной версией i. В турецком языке также есть строчная i без точки, ı \(\\u0131\), прописной для которой является I. Эта же особенность имеется и в азербайджанском языке \("az"\).  
  
 Таким образом, допущения о прописной версии буквы i или строчной версии буквы I не являются правильными для всех языков. При использовании перегрузок по умолчанию для сравнения строк они будут меняться в зависимости от языков и региональных параметров. Если сравниваются нелингвистические данные, при использовании перегрузок по умолчанию может быть получен нежелательный результат, как показывает следующий пример с попыткой сравнить строки file и FILE без учета регистра.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/turkish1.cs#11)]
 [!code-vb[Conceptual.Strings.BestPractices#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/turkish1.vb#11)]  
  
 Это сравнение может вызвать значительные проблемы, если язык и региональные параметры случайно использовались в конфиденциальных параметрах, как показано в следующем примере. Вызов метода, например `IsFileURI("file:")`, возвращает значение `true`, если текущий язык — американский английский, и значение `false`, если текущий язык — турецкий. Следовательно, в системах на турецком языке кто\-то может попытаться обойти механизмы безопасности, блокирующие доступ к URI без учета регистра, которые начинаются с текста «FILE:».  
  
 [!code-csharp[Conceptual.Strings.BestPractices#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/turkish1.cs#12)]
 [!code-vb[Conceptual.Strings.BestPractices#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/turkish1.vb#12)]  
  
 В этом случае, поскольку «file:» должен интерпретироваться как нелингвистический идентификатор без учета языка и региональных параметров, нужно писать код, как показано в следующем примере.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/turkish1.cs#13)]
 [!code-vb[Conceptual.Strings.BestPractices#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/turkish1.vb#13)]  
  
### Порядковые операции со строками  
 Указание значения <xref:System.StringComparison?displayProperty=fullName> или <xref:System.StringComparison?displayProperty=fullName> в вызове метода является признаком нелингвистического сравнения, в котором признаки естественного языка игнорируются. Методы, которые вызываются с этими значениями <xref:System.StringComparison>, принимают решения о строковых операциях на основе простых байтовых сравнений, а не таблиц регистров или эквивалентности, которые параметризуются языком и региональными параметрами. В большинстве случаев такой подход наиболее соответствует предполагаемой интерпретации строк, ускоряя выполнение кода и делая его более надежным.  
  
 Порядковые сравнения — это сравнения строк, в которых каждый байт каждой строки сравнивается без лингвистической интерпретации; например, windows не равно Windows. По сути, это вызов функции `strcmp` среды выполнения C. Используйте такое сравнение, когда контекст определяет, что строки должны точно совпадать, или требует использования консервативной политики соответствия. Кроме того, порядковое сравнение — это самая быстрая операция сравнения, потому что при расчете результата не применяются лингвистические правила.  
  
 Строки в платформе .NET Framework могут содержать внедренные символы null. Одним из очевидных различий между порядковым сравнением и сравнением с учетом языка и региональных параметров \(включая сравнения, в которых используется инвариантный язык и региональные параметры\) является различие в обработке внедренных символов null в строке. Эти символы игнорируются при использовании методов <xref:System.String.Compare%2A?displayProperty=fullName> и <xref:System.String.Equals%2A?displayProperty=fullName> для сравнений с учетом языка и региональных параметров \(включая сравнения, использующие инвариантный язык\). В результате в сравнениях с учетом языка и региональных параметров строки, содержащие внедренные символы null, считаются равными строкам, которые таких символов не содержат.  
  
> [!IMPORTANT]
>  Несмотря на то что в методах сравнения строк не учитываются внедренные символы null, методы поиска строк, такие как <xref:System.String.Contains%2A?displayProperty=fullName>, <xref:System.String.EndsWith%2A?displayProperty=fullName>, <xref:System.String.IndexOf%2A?displayProperty=fullName>, <xref:System.String.LastIndexOf%2A?displayProperty=fullName> и <xref:System.String.StartsWith%2A?displayProperty=fullName>, эти символы учитывают.  
  
 В следующем примере выполняется сравнение с учетом языка и региональных параметров строки Aa с аналогичной строкой, содержащей несколько внедренных символов null между А и а, и показано, почему две строки рассматриваются как равные.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/embeddednulls1.cs#19)]
 [!code-vb[Conceptual.Strings.BestPractices#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/embeddednulls1.vb#19)]  
  
 Однако строки не считаются равными, если выполняется порядковое сравнение, как показано в следующем примере.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/embeddednulls2.cs#20)]
 [!code-vb[Conceptual.Strings.BestPractices#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/embeddednulls2.vb#20)]  
  
 Порядковые сравнения без учета регистра — это следующий наиболее консервативной подход к решению задачи. В этих сравнениях почти всегда игнорируется регистр. Так, windows совпадает с Windows. При работе с символами ASCII эта политика эквивалентна сравнению <xref:System.StringComparison?displayProperty=fullName> за исключением того, что стандартные правила регистра ASCII игнорируются. Следовательно, любой символ в последовательности \[A, Z\] \(\\u0041–\\u005A\) соответствует соответствующему символу в последовательности \[a, z\] \(\\u0061–\\007A\). Правила регистра за пределами диапазона ASCII используют таблицы инвариантного языка. Поэтому следующее сравнение  
  
 [!code-csharp[Conceptual.Strings.BestPractices#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison2.cs#4)]
 [!code-vb[Conceptual.Strings.BestPractices#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison2.vb#4)]  
  
 эквивалентно следующему сравнению \(но выполняется быстрее\):  
  
 [!code-csharp[Conceptual.Strings.BestPractices#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison2.cs#5)]
 [!code-vb[Conceptual.Strings.BestPractices#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison2.vb#5)]  
  
 Эти сравнения по\-прежнему выполняются очень быстро.  
  
> [!NOTE]
>  Поведение строки файловой системы, ключей реестра и значений, а также переменные среды лучше всего представлены типом <xref:System.StringComparison?displayProperty=fullName>.  
  
 И <xref:System.StringComparison?displayProperty=fullName>, и <xref:System.StringComparison?displayProperty=fullName> используют двоичные значения непосредственно и лучше всего подходят для сопоставления. При отсутствии точной информации о параметрах сравнения используйте одно из этих двух значений. Однако, поскольку они выполняют побайтовое сравнение, лингвистическая сортировка \(как в словаре английского языка\) не выполняется, однако используется двоичный порядок сортировки. В большинстве случаев для пользователя эти результаты будут выглядеть странно.  
  
 Порядковая семантика используется по умолчанию для перегрузок <xref:System.String.Equals%2A?displayProperty=fullName>, которые не содержат аргумента <xref:System.StringComparison> \(включая оператор равенства\). В любом случае рекомендуется вызвать перегрузку, содержащую параметр <xref:System.StringComparison>.  
  
### Строковые операции, использующие инвариантный язык и региональные параметры  
 В сравнениях с инвариантным языком используется свойство <xref:System.Globalization.CultureInfo.CompareInfo%2A>, возвращаемое статическим свойством <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>. Это поведение одинаково во всех системах; оно преобразует любые символы за пределами своего диапазона в то, что оно считает эквивалентными инвариантными символами. Эта политика может пригодиться для реализации единого набора поведений строк в разных языках и региональных параметрах, однако часто это дает непредвиденные результаты.  
  
 Сравнения без учета регистра с инвариантным языком также используют статическое свойство <xref:System.Globalization.CultureInfo.CompareInfo%2A>, возвращаемое статическим свойством <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> для сведений сравнения. Любые различия регистров в этих преобразуемых символах игнорируются.  
  
 Сравнения с использованием <xref:System.StringComparison?displayProperty=fullName> и <xref:System.StringComparison?displayProperty=fullName> работают одинаково в строках ASCII. Однако <xref:System.StringComparison?displayProperty=fullName> принимает лингвистические решения, которые могут не подходить для строк, которые нужно интерпретировать как набор байтов. Объект `CultureInfo.InvariantCulture.CompareInfo` заставляет метод <xref:System.String.Compare%2A> интерпретировать определенные наборы символов как эквивалентные. Например, следующие элементы эквивалентны только в инвариантном языке.  
  
 InvariantCulture: a \+ ̊ \= å  
  
 Латинская строчная буква А, а \(\\u0061\), находясь рядом с объединяющим кольцом над символом «\+» , « ̊» \(\\u030a\), интерпретируется как строчная латинская буква а с кольцом над ней, å \(\\u00e5\). Как показано в следующем примере, это поведение отличается от порядкового сравнения.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison3.cs#15)]
 [!code-vb[Conceptual.Strings.BestPractices#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison3.vb#15)]  
  
 При интерпретации имен файлов, файлов cookie или чего\-либо еще, где могут появляться такие сочетания, как å, порядковые сравнения по\-прежнему являются наиболее понятным и подходящим поведением.  
  
 В целом в инвариантном языке очень мало свойств, которые могли бы сделать его полезным для сравнения. Он выполняет сравнения с учетом лингвистических параметров, что не позволяет гарантировать полную эквивалентность символов, однако не подходит для отображения на любом языке. Одной из оснований использования <xref:System.StringComparison?displayProperty=fullName> для сравнения является необходимость сохранить упорядоченные данные для идентичного отображения на разных языках. Например, если к приложению прилагается крупный файл данных, содержащий список сортированных идентификаторов для отображения, добавление в этот список потребует вставки элементов с сортировкой в инвариантном стиле.  
  
 [К началу](#top)  
  
<a name="choosing_a_stringcomparison_member_for_your_method_call"></a>   
## Выбор элемента StringComparison для своего вызова метода  
 В следующей таблице приведено сопоставление семантического контекста строк элементу перечисления <xref:System.StringComparison>.  
  
|Данные|Поведение|Соответствующее сравнение System.StringComparison<br /><br /> значение|  
|------------|---------------|--------------------------------------------------------------------|  
|Внутренние идентификаторы с учетом регистра<br /><br /> Идентификаторы с учетом регистра в таких стандартах, как XML и HTTP.<br /><br /> Параметры безопасности с учетом регистра.|Нелингвистические идентификаторы с точным соответствием байтов.|<xref:System.StringComparison>|  
|Внутренние идентификаторы без учета регистра.<br /><br /> Идентификаторы без учета регистра в таких стандартах, как XML и HTTP.<br /><br /> Пути к файлам.<br /><br /> Ключи реестра и значения.<br /><br /> Переменные среды.<br /><br /> Идентификаторы ресурсов \(например, имена дескрипторов\).<br /><br /> Параметры безопасности без учета регистра.|Нелингвистический идентификатор, в котором регистр не учитывается; особенно данные, хранящиеся в большинстве системных служб Windows.|<xref:System.StringComparison>|  
|Некоторые сохраненные лингвистически релевантные данные.<br /><br /> Отображение лингвистических данных, требующее фиксированного порядка сортировки.|Лингвистически релевантные данные без учета языка и региональных параметров.|<xref:System.StringComparison><br /><br /> \-или\-<br /><br /> <xref:System.StringComparison>|  
|Данные, отображаемые пользователю.<br /><br /> Пользовательский ввод в большинстве случаев.|Данные, требующие местных лингвистических правил.|<xref:System.StringComparison><br /><br /> \-или\-<br /><br /> <xref:System.StringComparison>|  
  
 [К началу](#top)  
  
<a name="common_string_comparison_methods_in_the_net_framework"></a>   
## Общие методы сравнения строк в .NET Framework  
 В следующих разделах описываются методы, которые чаще всего используются для сравнения строк.  
  
### String.Compare  
 Интерпретация по умолчанию: <xref:System.StringComparison?displayProperty=fullName>.  
  
 Поскольку эта операция наиболее тесно связана с интерпретацией строк, необходимо изучить все экземпляры вызовов этого метода, чтобы определить, должны ли строки интерпретироваться с учетом текущего языка и региональных параметров, либо их нужно \(символически\) отделить от языка и региональных параметров. Обычно выбирается последнее, и тогда должно использоваться сравнение <xref:System.StringComparison?displayProperty=fullName>.  
  
 Класс <xref:System.Globalization.CompareInfo?displayProperty=fullName>, возвращаемый свойством <xref:System.Globalization.CultureInfo.CompareInfo%2A?displayProperty=fullName>, также включает метод <xref:System.Globalization.CompareInfo.Compare%2A>, предоставляющий большое количество соответствующих параметров \(порядковый, игнорирование пробела, игнорирование типа каны и т. д.\) посредством перечисления флага <xref:System.Globalization.CompareOptions>.  
  
### String.CompareTo  
 Интерпретация по умолчанию: <xref:System.StringComparison?displayProperty=fullName>.  
  
 В настоящее время этот метод не предлагает перегрузку, задающую тип <xref:System.StringComparison>. Обычно возможно преобразовать этот метод в рекомендованную форму <xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=fullName>.  
  
 Типы, реализующие интерфейсы <xref:System.IComparable> и <xref:System.IComparable%601>, реализуют этот метод. Поскольку не предлагается параметр <xref:System.StringComparison>, реализация типов часто позволяет пользователю задать <xref:System.StringComparer> в своем конструкторе. В следующем примере определяется класс `FileName`, конструктор класса которого включает параметр <xref:System.StringComparer>. Затем этот объект <xref:System.StringComparer> используется в методе `FileName.CompareTo`.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/api1.cs#6)]
 [!code-vb[Conceptual.Strings.BestPractices#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/api1.vb#6)]  
  
### String.Equals  
 Интерпретация по умолчанию: <xref:System.StringComparison?displayProperty=fullName>.  
  
 Класс <xref:System.String> позволяет выполнить проверку на равенство, вызвав статические перегрузки метода <xref:System.String.Equals%2A> или перегрузки экземпляров. Кроме того, можно воспользоваться оператором статического равенства. Перегрузки и оператор используют порядковое сравнение по умолчанию. Однако рекомендуется вызывать перегрузку, которая явно задает тип <xref:System.StringComparison>, даже если требуется выполнить порядковое сравнение. Это упрощает поиск кода для интерпретации определенной строки.  
  
### String.ToUpper и String.ToLower  
 Интерпретация по умолчанию: <xref:System.StringComparison?displayProperty=fullName>.  
  
 Следует соблюдать осторожность, используя эти методы, поскольку принудительное преобразование строки в нижний или верхний регистр часто используется в качестве незначительной нормализации для сравнения строк независимо от регистра. В этом случае целесообразно выполнить сравнение без учета регистра.  
  
 Также доступны методы <xref:System.String.ToUpperInvariant%2A?displayProperty=fullName> и <xref:System.String.ToLowerInvariant%2A?displayProperty=fullName>.<xref:System.String.ToUpperInvariant%2A> — это стандартный способ нормализации регистра. Сравнения, выполненные с помощью <xref:System.StringComparison?displayProperty=fullName>, с точки зрения поведения представляют собой комбинацию из двух вызовов: вызов <xref:System.String.ToUpperInvariant%2A> в обоих аргументах строки и выполнение сравнения с использованием <xref:System.StringComparison?displayProperty=fullName>.  
  
 Также доступны перегрузки для преобразования в верхний и нижний регистр в конкретном языке. Для этого передается объект <xref:System.Globalization.CultureInfo>, представляющий этот язык для метода.  
  
### Char.ToUpper и Char.ToLower  
 Интерпретация по умолчанию: <xref:System.StringComparison?displayProperty=fullName>.  
  
 Эти методы работают аналогично методам <xref:System.String.ToUpper%2A?displayProperty=fullName> и <xref:System.String.ToLower%2A?displayProperty=fullName>, описанным в предыдущем разделе.  
  
### String.StartsWith и String.EndsWith  
 Интерпретация по умолчанию: <xref:System.StringComparison?displayProperty=fullName>.  
  
 По умолчанию оба этих метода выполняют сравнение с учетом языка и региональных параметров.  
  
### String.IndexOf и String.LastIndexOf  
 Интерпретация по умолчанию: <xref:System.StringComparison?displayProperty=fullName>.  
  
 Перегрузки этих методов по умолчанию выполняют сравнения непоследовательно. Все методы <xref:System.String.IndexOf%2A?displayProperty=fullName> и <xref:System.String.LastIndexOf%2A?displayProperty=fullName>, включающие параметр <xref:System.Char>, выполняют порядковое сравнение, однако методы <xref:System.String.IndexOf%2A?displayProperty=fullName> и <xref:System.String.LastIndexOf%2A?displayProperty=fullName> по умолчанию, которые включают параметр <xref:System.String>, выполняют сравнение с учетом языка и региональных параметров.  
  
 Если нужно вызвать метод <xref:System.String.IndexOf%28System.String%29?displayProperty=fullName> или <xref:System.String.LastIndexOf%28System.String%29?displayProperty=fullName> и передать ему строку для определения ее местоположения в текущем экземпляре, рекомендуется вызвать перегрузку, которая явно задает тип <xref:System.StringComparison>. Перегрузки, включающие аргумент <xref:System.Char>, не позволяют задать тип <xref:System.StringComparison>.  
  
 [К началу](#top)  
  
<a name="methods_that_perform_string_comparison_indirectly"></a>   
## Методы, выполняющие сравнение строк опосредованно  
 Некоторые нестроковые методы, основным назначением которых является сравнение строк, используют тип <xref:System.StringComparer>. Класс <xref:System.StringComparer> включает шесть статических свойств, возвращающих экземпляры <xref:System.StringComparer>, методы <xref:System.StringComparer.Compare%2A?displayProperty=fullName> которых выполняют следующие типы сравнения строк.  
  
-   Сравнения строк с учетом языка и региональных параметров с использованием текущего языка и региональных параметров. Этот объект <xref:System.StringComparer> возвращается свойством <xref:System.StringComparer.CurrentCulture%2A?displayProperty=fullName>.  
  
-   Сравнение без учета регистра с использованием текущего языка и региональных параметров. Этот объект <xref:System.StringComparer> возвращается свойством <xref:System.StringComparer.CurrentCultureIgnoreCase%2A?displayProperty=fullName>.  
  
-   Сравнения без учета языка и региональных параметров с использованием правил сравнения слов инвариантного языка. Этот объект <xref:System.StringComparer> возвращается свойством <xref:System.StringComparer.InvariantCulture%2A?displayProperty=fullName>.  
  
-   Сравнения без учета регистра, языка и региональных параметров с использованием правил сравнения слов инвариантного языка. Этот объект <xref:System.StringComparer> возвращается свойством <xref:System.StringComparer.InvariantCultureIgnoreCase%2A?displayProperty=fullName>.  
  
-   Порядковое сравнение. Этот объект <xref:System.StringComparer> возвращается свойством <xref:System.StringComparer.Ordinal%2A?displayProperty=fullName>.  
  
-   Порядковое сравнение без учета регистра. Этот объект <xref:System.StringComparer> возвращается свойством <xref:System.StringComparer.OrdinalIgnoreCase%2A?displayProperty=fullName>.  
  
### Array.Sort и Array.BinarySearch  
 Интерпретация по умолчанию: <xref:System.StringComparison?displayProperty=fullName>.  
  
 При хранении любых данных в коллекции или считывании сохраненных данных из файла или базы данных в коллекцию изменение текущего языка и региональных параметров может сделать недействительными инварианты этой коллекции. Метод <xref:System.Array.BinarySearch%2A?displayProperty=fullName> предполагает, что элементы в массиве, поиск которых необходимо выполнить, уже сортированы. Чтобы отсортировать любой стоковый элемент в массиве метод <xref:System.Array.Sort%2A?displayProperty=fullName> вызывает метод <xref:System.String.Compare%2A?displayProperty=fullName> для упорядочивания отдельных элементов. Использовать средство сравнения с учетом языка и региональных параметров может быть опасно, если язык и региональные параметры изменяются в период между сортировкой массива и поиском в содержимом этого массива. Например, в следующем коде для хранения и извлечения данных используется средство сравнения, которое неявно предоставляется свойством `Thread.CurrentThread.CurrentCulture`. Если язык и региональные параметры могут измениться между вызовом `StoreNames` и `DoesNameExist` и особенно если содержимое массива сохраняется в период между вызовами этих двух методов, двоичный поиск может завершиться ошибкой.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect1.cs#7)]
 [!code-vb[Conceptual.Strings.BestPractices#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect1.vb#7)]  
  
 Рекомендуемый вариант показан в следующем примере, где один и тот же метод порядкового сравнения \(без учета языка и региональных параметров\) используется для сортировки массива и поиска в нем. Измененный код отражается в строках, помеченных в этих двух примерах как `Line A` и `Line B`.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect1.cs#8)]
 [!code-vb[Conceptual.Strings.BestPractices#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect1.vb#8)]  
  
 Если эти данные сохраняются и перемещаются в разных языках, а для представления этих данных пользователю используется сортировка, целесообразно использовать <xref:System.StringComparison?displayProperty=fullName>, действующий с учетом лингвистических правил и, следовательно, повышающий качество выводимых пользователю данных, но при этом не подверженный влиянию изменений в языке и региональных параметрах. В следующем примере два предыдущих примера изменяются так, чтобы для сортировки массива и поиска в нем использовался инвариантный язык.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect1.cs#9)]
 [!code-vb[Conceptual.Strings.BestPractices#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect1.vb#9)]  
  
### Пример коллекций: доступный для кэширования конструктор  
 Хэширование строк — это второй пример операции, на которую влияет способ сравнения строк.  
  
 В следующем примере создается экземпляр объекта <xref:System.Collections.Hashtable> путем передачи его объекту <xref:System.StringComparer>, который возвращается свойством <xref:System.StringComparer.OrdinalIgnoreCase%2A?displayProperty=fullName>. Поскольку класс <xref:System.StringComparer>, который является производным от <xref:System.StringComparer>, реализует интерфейс <xref:System.Collections.IEqualityComparer>, его метод <xref:System.Collections.IEqualityComparer.GetHashCode%2A> используется для вычисления хэш\-кода строк в хэш\-таблице.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect2.cs#10)]
 [!code-vb[Conceptual.Strings.BestPractices#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect2.vb#10)]  
  
 [К началу](#top)  
  
<a name="Formatted"></a>   
## Отображение и сохранение форматированных данных  
 При отображении нестроковых данных, например чисел, дат и времени, пользователям следует форматировать их с использованием параметров языка и региональных параметров пользователя. По умолчанию метод <xref:System.String.Format%2A?displayProperty=fullName> и методы `ToString` числовых типов и типов даты и времени используют текущий язык потока для операций форматирования. Чтобы явно указать, что метод форматирования должен использовать текущий язык и региональные параметры, можно вызвать перегрузку метода форматирования, который имеет параметр `provider`, например [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName> или <xref:System.DateTime.ToString%28System.IFormatProvider%29?displayProperty=fullName>, и передать ему свойство <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>.  
  
 Нестроковые данные можно сохранить в виде двоичных или форматированных данных. Если решено сохранять данные в виде форматированных, нужно вызвать перегрузку метода форматирования, которая включает параметр `provider`, и передать ей свойство <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>. Инвариантный язык и региональные параметры предоставляют согласованный формат для форматированных данных независимо от языка, региональных параметров и компьютера. Напротив, сохранение форматированных данных с использованием языков и региональных параметров, отличающихся от инвариантных, имеет ряд ограничений.  
  
-   Данные, вероятно, станут недоступными для использования после извлечения в системе с другим языком либо если пользователь текущей системы сменит текущий язык и попытается извлечь данные.  
  
-   Свойства языка и региональных параметров на конкретном компьютере могут отличаться от стандартных значений. Пользователь может в любой момент настроить параметры отображения с учетом языка и региональных параметров. По этой причине форматированные данные, которые сохраняются в системе, могут стать недоступными для чтения после изменения настроек языка пользователем. Переносимость форматированных данных с одного компьютера на другой, вероятно, будет еще более ограниченной.  
  
-   Международные, региональные и национальные стандарты, регулирующие форматирование чисел, дат и времени, со временем меняются, и эти изменения отражаются в обновлениях ОС Windows. При изменении правил форматирования данные, форматированные с использованием старых правил, становятся недоступными для чтения.  
  
 В следующем примере демонстрируется ограниченная переносимость в результате использования для сохранения данных форматирования с учетом языка и региональных параметров. В этом примере массив значений даты и времени сохраняется в файл. Данные форматируются с использованием правил английского языка \(США\). После того как приложение сменит текущий язык потока на французский \(Швейцария\), оно попытается прочитать сохраненные значения, используя правила форматирования текущей культуры. При попытке чтения двух элементов данных создается исключение <xref:System.FormatException>, а массив дат теперь содержит два неправильных элемента, равных <xref:System.DateTime.MinValue>.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/persistence.cs#21)]
 [!code-vb[Conceptual.Strings.BestPractices#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/persistence.vb#21)]  
  
 Однако если заменить свойство <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> на <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> в вызовах методов <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName> и <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName>, хранимые данные даты и времени восстанавливаются успешно, как показано ниже.  
  
```  
  
06.05.1758 21:26  
05.05.1818 07:19  
22.04.1870 23:54  
08.09.1890 06:47  
18.02.1905 15:12  
  
```  
  
## См. также  
 [Обработка строк](../../../docs/standard/base-types/manipulating-strings.md)