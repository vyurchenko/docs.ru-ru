---
title: "Creating Prototypes in Managed Code | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "prototypes in managed code"
  - "COM interop, DLL functions"
  - "unmanaged functions"
  - "platform invoke, creating prototypes"
  - "COM interop, platform invoke"
  - "interoperation with unmanaged code, DLL functions"
  - "interoperation with unmanaged code, platform invoke"
  - "platform invoke, object fields"
  - "DLL functions"
  - "object fields in platform invoke"
ms.assetid: ecdcf25d-cae3-4f07-a2b6-8397ac6dc42d
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# Creating Prototypes in Managed Code
В этом разделе описывается доступ к неуправляемым функциям и представлено несколько полей атрибутов, которые уточняют определение метода в управляемом коде.  Примеры, демонстрирующие способы создания объявлений на основе .NET, которые используются с вызовом неуправляемого кода, представлены в разделе [Маршалинг данных при вызове неуправляемого кода](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md).  
  
 Чтобы обратиться к неуправляемой функции DLL из управляемого кода, нужно знать ее имя и имя библиотеки DLL, которая ее экспортирует.  Имея эту информацию, можно приступать к написанию управляемого определения для неуправляемой функции, реализованной в библиотеке DLL.  Кроме того, можно настроить способ, которым вызов неуправляемого кода создает функцию и маршалирует данные в функцию и обратно.  
  
> [!NOTE]
>  Функции Win32 API, которые распределяют строку, позволяют освободить строку с помощью такого метода, как `LocalFree`.  Вызов неуправляемого кода обрабатывает эти параметры иначе.  Для вызовов неуправляемого кода следует использовать параметр типа `IntPtr`, а не `String`.  Чтобы вручную преобразовать тип в строку и вручную освободить его, можно использовать методы, предоставленные классом <xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>.  
  
## Основы объявления  
 Как показано в примерах ниже, управляемые определения неуправляемых функций зависят от используемого языка.  Более полные примеры кода представлены в разделе [Примеры вызовов неуправляемого кода](../../../docs/framework/interop/platform-invoke-examples.md).  
  
```vb  
Imports System.Runtime.InteropServices  
Public Class Win32  
    Declare Auto Function MessageBox Lib "user32.dll" _  
       (ByVal hWnd As Integer, _  
        ByVal txt As String, ByVal caption As String, _  
        ByVal Typ As Integer) As IntPtr  
End Class  
```  
  
 Для применения полей <xref:System.Runtime.InteropServices.DllImportAttribute.BestFitMapping>, <xref:System.Runtime.InteropServices.DllImportAttribute.CallingConvention>, <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling>, <xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig>, <xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError> или <xref:System.Runtime.InteropServices.DllImportAttribute.ThrowOnUnmappableChar> к объявлению [!INCLUDE[vbprvbext](../../../includes/vbprvbext-md.md)] необходимо использовать атрибут <xref:System.Runtime.InteropServices.DllImportAttribute> вместо оператора `Declare`.  
  
```vb  
Imports System.Runtime.InteropServices  
Public Class Win32  
   <DllImport ("user32.dll", CharSet := CharSet.Auto)> _  
   Public Shared Function MessageBox (ByVal hWnd As Integer, _  
        ByVal txt As String, ByVal caption As String, _  
        ByVal Typ As Integer) As IntPtr  
   End Function  
End Class  
  
```  
  
```csharp  
using System.Runtime.InteropServices;  
[DllImport("user32.dll")]  
    public static extern IntPtr MessageBox(int hWnd, String text,   
                                       String caption, uint type);  
  
```  
  
```cpp  
using namespace System::Runtime::InteropServices;  
[DllImport("user32.dll")]  
    extern "C" IntPtr MessageBox(int hWnd, String* pText,  
    String* pCaption unsigned int uType);  
```  
  
## Настройка определения  
 Поля атрибутов, заданные явно или неявно, определяют выполнение управляемого кода.  Вызов неуправляемого кода выполняется в соответствии с набором значений по умолчанию различных полей, хранящихся в сборке как метаданные.  Это поведение по умолчанию можно изменить, настроив значения одного или нескольких полей.  Во многих случаях для установки значения используется <xref:System.Runtime.InteropServices.DllImportAttribute>.  
  
 Ниже приведен полный набор полей атрибутов, относящихся к вызову неуправляемого кода.  Для каждого поля в таблице указано значение по умолчанию и дана ссылка на инструкцию по использованию поля для определения неуправляемых функций DLL.  
  
|Поле|Описание|  
|----------|--------------|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.BestFitMapping>|Включает или отключает наилучшее сопоставление.|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.CallingConvention>|Задает соглашение о вызовах, которое должно использоваться при передаче аргументов методов.  Значение по умолчанию — `WinAPI`, что соответствует режиму `__stdcall` для 32\-разрядных платформ на базе процессора Intel.|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.CharSet>|Управляет декорированием имен и способом маршалинга строковых аргументов в функцию.  Значение по умолчанию — `CharSet.Ansi`.|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint>|Указывает точку входа DLL для вызова.|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling>|Определяет, должна ли изменяться точка входа в соответствии с кодировкой.  Значение по умолчанию зависит от языка программирования.|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig>|Определяет, должна ли сигнатура управляемого метода преобразовываться в неуправляемую сигнатуру, которая возвращает значение HRESULT и имеет дополнительный аргумент \[out, retval\] для возвращаемого значения.<br /><br /> Значение по умолчанию — `true` \(сигнатура не должна преобразовываться\).|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError>|Позволяет вызывающему объекту использовать функцию интерфейса API `Marshal.GetLastWin32Error` для определения факта ошибки при выполнении метода.  В Visual Basic значение по умолчанию — `true`, а в C\# и C\+\+ — `false`.|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.ThrowOnUnmappableChar>|Управляет возникновением исключения при появлении несопоставимого символа Юникода, который преобразуется в символ ANSI "?".|  
  
 Подробную справочную информацию см. в разделе [Класс DllImportAttribute](frlrfSystemRuntimeInteropServicesDllImportAttributeClassTopic).  
  
## Вопросы безопасности при вызове неуправляемого кода  
 Члены `Assert`, `Deny` и `PermitOnly` перечисления <xref:System.Security.Permissions.SecurityAction> называются *модификаторами обхода стека*.  Эти члены игнорируются, если они используются как декларативные атрибуты в объявлениях вызова неуправляемого кода и операторах COM языка IDL.  
  
### Примеры вызовов неуправляемого кода  
 Примеры вызовов неуправляемого кода в этом разделе иллюстрируют использование атрибута `RegistryPermission` с модификаторами обхода стека.  
  
 В примере кода ниже модификаторы <xref:System.Security.Permissions.SecurityAction> `Assert`, `Deny` и `PermitOnly` не учитываются.  
  
```  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Assert, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionAssert();  
  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Deny, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.PermitOnly, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
```  
  
 Однако модификатор `Demand` в следующем примере принимается.  
  
```  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
```  
  
 Модификаторы <xref:System.Security.Permissions.SecurityAction> действительно правильно работают, если они заданы для класса, содержащего \(инкапсулирующего\) вызов неуправляемого кода.  
  
```cpp  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
public ref class PInvokeWrapper  
{  
public:  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionDeny();  
};  
```  
  
```csharp  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
class PInvokeWrapper  
{  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionDeny();  
}  
  
```  
  
 Модификаторы <xref:System.Security.Permissions.SecurityAction> также правильно работают в сценарии с вложением, когда они задаются для объекта, выполняющего вызов неуправляемого кода.  
  
```cpp  
{  
public ref class PInvokeWrapper  
public:  
    [DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionDeny();  
  
    [RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    public static bool CallRegistryPermission()  
    {  
     return CallRegistryPermissionInternal();  
    }  
};  
```  
  
```csharp  
class PInvokeScenario  
{  
    [DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionInternal();  
  
    [RegistryPermission(SecurityAction.Assert, Unrestricted = true)]  
    public static bool CallRegistryPermission()  
    {  
     return CallRegistryPermissionInternal();  
    }  
}  
```  
  
#### Примеры COM\-взаимодействия  
 Примеры COM\-взаимодействия в этом разделе иллюстрируют использование атрибута `RegistryPermission` с модификаторами обхода стека.  
  
 В приведенных ниже объявлениях интерфейса COM\-взаимодействия модификаторы `Assert`, `Deny` и `PermitOnly` не учитываются по аналогии с примерами вызовов неуправляемого кода в предыдущем разделе.  
  
```  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IAssertStubsItf  
{  
[RegistryPermission(SecurityAction.Assert, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.Assert, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IDenyStubsItf  
{  
[RegistryPermission(SecurityAction.Deny, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.Deny, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IAssertStubsItf  
{  
[RegistryPermission(SecurityAction.PermitOnly, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.PermitOnly, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
  
```  
  
 Кроме того, модификатор `Demand` недопустим в сценариях объявления интерфейса COM\-взаимодействия, как показано ниже.  
  
```  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IDemandStubsItf  
{  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.Demand, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
```  
  
## См. также  
 [Consuming Unmanaged DLL Functions](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)   
 [Specifying an Entry Point](../../../docs/framework/interop/specifying-an-entry-point.md)   
 [Specifying a Character Set](../../../docs/framework/interop/specifying-a-character-set.md)   
 [Platform Invoke Examples](../../../docs/framework/interop/platform-invoke-examples.md)   
 [Platform Invoke Security Considerations](http://msdn.microsoft.com/ru-ru/bbcc67f7-50b5-4917-88ed-cb15470409fb)   
 [Identifying Functions in DLLs](../../../docs/framework/interop/identifying-functions-in-dlls.md)   
 [Creating a Class to Hold DLL Functions](../../../docs/framework/interop/creating-a-class-to-hold-dll-functions.md)   
 [Calling a DLL Function](../../../docs/framework/interop/calling-a-dll-function.md)