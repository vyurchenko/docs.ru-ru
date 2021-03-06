---
title: "Основы работы с Visual Basic строка | Документы Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- strings [Visual Basic], Like operator
- strings [Visual Basic], Visual Basic
- strings [Visual Basic], regular expressions
ms.assetid: 5674418d-f00d-4f72-9f98-d15897793350
caps.latest.revision: 14
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a9475c57f01c78fd5c4e2d2674f22f18ad4772e5
ms.lasthandoff: 03/13/2017

---
# <a name="string-basics-in-visual-basic"></a>Основы работы со строками в Visual Basic
Тип данных `String` представляет последовательность символов (каждый из которых, в свою очередь, представляет экземпляр типа данных `Char`). В этом разделе рассмотрены базовые понятия строк в [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## <a name="string-variables"></a>Строковые переменные  
 Экземпляру строки можно назначить литеральное значение, которое представляет ряд символов. Пример:  
  
 [!code-vb[VbVbalrStrings&#63;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_1.vb)]  
  
 Переменная `String` также может принимать любое выражение, результатом которого является строка. Ниже приведены примеры.  
  
 [!code-vb[VbVbalrStrings&#64;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_2.vb)]  
  
 Любой литерал, который присваивается переменной `String`, должен быть заключен в кавычки (""). Это означает, что кавычки в пределах строки не могут быть представлены кавычкой. Например, следующий код вызовет ошибку компиляции:  
  
 [!code-vb[VbVbalrStrings&#65;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_3.vb)]  
  
 Этот код вызывает ошибку, так как компилятор завершает строку после второй пары кавычек, а остаток строки интерпретируется как код. Чтобы устранить эту проблему, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] интерпретирует два символа кавычек в строковом литерале как один символ кавычек в строке. В следующем примере показан правильный способ указания кавычек в строке:  
  
 [!code-vb[VbVbalrStrings&#66;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_4.vb)]  
  
 В предыдущем примере два символа кавычек перед словом `Look` становятся одним символом кавычек в строке. Три символа кавычек в конце строки представляют один символ кавычек в строке и конечный символ строки.  
  
 Строковые литералы могут содержать несколько строк:  
  
```vb  
Dim x = "hello  
world"  
  
```  
  
 Результирующая строка содержит последовательности новых строк, используемых в строковом литерале (vbcr, vbcrlf и т. д.).  Вам больше не требуется использовать старое решение:  
  
```vb  
Dim x = <xml><![CDATA[Hello  
World]]></xml>.Value  
  
```  
  
## <a name="characters-in-strings"></a>Символы в строках  
 Строку можно представить как последовательность значений `Char`. При этом тип `String` имеет встроенные функции, которые позволяют работать со строками, как с массивами. Как и все массивы в [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)], строки — это массивы с индексацией с нуля. К определенному символу в строке можно обратиться с помощью свойства `Chars`, которое предоставляет механизм доступа к символу по позиции, в которой он отображается в строке. Пример:  
  
 [!code-vb[VbVbalrStrings&#67;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_5.vb)]  
  
 В приведенном выше примере свойство `Chars` строки возвращает четвертый символ в строке, `D`, и присваивает его `myChar`. Вы также можете получить длину определенной строки с помощью свойства `Length`. Если вам требуется выполнить несколько манипуляций со строкой, можно преобразовать ее в массив экземпляров `Char` с помощью функции `ToCharArray` строки. Пример:  
  
 [!code-vb[VbVbalrStrings&#68;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_6.vb)]  
  
 Переменная `myArray` теперь содержит массив значений `Char`, каждое из которых представляет символ из `myString`.  
  
## <a name="the-immutability-of-strings"></a>Неизменность строк  
 Строка *неизменяемый*, то есть, его значение невозможно изменить после его создания. Однако это не мешает назначить строковой переменной более одного значения. Рассмотрим следующий пример.  
  
 [!code-vb[VbVbalrStrings&#69;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_7.vb)]  
  
 Здесь строковая переменная создается, получает значение, которое затем изменяется.  
  
 В частности, в первой строке создается экземпляр типа `String`, которому присваивается значение `This string is immutable`. Во второй строке примера создается новый экземпляр, которому присваивается значение `Or is it?`. При этом строковая переменная удаляет ссылку на первый экземпляр и сохраняет ссылку на новый экземпляр.  
  
 В отличие от других встроенных типов данных `String` — это ссылочный тип. Если переменная ссылочного типа передается в качестве аргумента функции или подпрограмме, вместо фактического значения строки передается ссылка на адрес в памяти, где хранятся данные. Поэтому в предыдущем примере имя переменной остается таким же, но оно указывает на другой экземпляр класса `String`, который содержит новое значение.  
  
## <a name="see-also"></a>См. также  
 [Знакомство со строками в Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)   
 [Тип данных String](../../../../visual-basic/language-reference/data-types/string-data-type.md)   
 [Тип данных char](../../../../visual-basic/language-reference/data-types/char-data-type.md)   
 [Основные операции со строками](http://msdn.microsoft.com/library/8133d357-90b5-4b62-9927-43323d99b6b6)
