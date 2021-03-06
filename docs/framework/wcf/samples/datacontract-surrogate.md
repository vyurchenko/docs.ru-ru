---
title: "Суррогат DataContract | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b0188f3c-00a9-4cf0-a887-a2284c8fb014
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Суррогат DataContract
В этом образце показано, каким образом такие процессы, как сериализация, десериализация, экспорт и импорт схемы, могут быть настроены при помощи заменяющего класса контракта данных.В этом образце показано, как использовать заменяющий класс в сценариях клиента и сервера, в которых данные сериализуются и передаются между клиентом и службой [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
> [!NOTE]
>  Процедура настройки и инструкции по построению для данного образца приведены в конце этого раздела.  
  
 В этом образце используется следующий контракт службы.  
  
```  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
[AllowNonSerializableTypes]  
public interface IPersonnelDataService  
{  
    [OperationContract]  
    void AddEmployee(Employee employee);  
  
    [OperationContract]  
    Employee GetEmployee(string name);  
}  
```  
  
 Операция `AddEmployee` позволяет пользователям добавлять данные о новых сотрудниках, а операция `GetEmployee` поддерживает поиск сотрудников по имени.  
  
 В этих операциях используется следующий тип данных.  
  
```  
[DataContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
class Employee  
{  
    [DataMember]  
    public DateTime dateHired;  
  
    [DataMember]  
    public Decimal salary;  
  
    [DataMember]  
    public Person person;  
}  
  
```  
  
 В типе `Employee` класс `Person` \(показан в следующем образце кода\) не может быть сериализован с помощью <xref:System.Runtime.Serialization.DataContractSerializer>, поскольку он не является допустимым классом контракта данных.  
  
```  
public class Person  
{  
    public string firstName;  
  
    public string lastName;  
  
    public int age;  
  
    public Person() { }  
}  
```  
  
 Можно применить атрибут `DataContract` к классу `Person`, но это не всегда возможно.Например, класс `Person` может быть определен в отдельной сборке, управлять которой невозможно.  
  
 С учетом этого ограничения одним из способов сериализации класса `Person` является его замена на другой класс, отмеченный атрибутом `DataContractAttribute`, и копирование необходимых данных в новый класс.Целью является отображение класса `Person` как DataContract в сериализаторе <xref:System.Runtime.Serialization.DataContractSerializer>.Обратите внимание, что это один способ сериализации классов, отличных от классов контракта данных.  
  
 В этом образце класс `Person` логически заменяется на другой класс с именем `PersonSurrogated`.  
  
```  
[DataContract(Name="Person", Namespace = "http://Microsoft.ServiceModel.Samples")]  
public class PersonSurrogated  
{  
    [DataMember]  
    public string FirstName;  
  
    [DataMember]  
    public string LastName;  
  
    [DataMember]  
    public int Age;  
}  
  
```  
  
 Заменяющий класс контракта данных используется для обеспечения такой замены.Заменяющий класс контракта данных является классом, который реализует <xref:System.Runtime.Serialization.IDataContractSurrogate>.В этом образце класс `AllowNonSerializableTypesSurrogate` реализует этот интерфейс.  
  
 В реализации интерфейса первой задачей является установка сопоставления типов из класса `Person` с классом `PersonSurrogated`.Используется как во время сериализации, так и во время экспорта схемы.Такое сопоставление обеспечивается путем реализации метода <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%28System.Type%29>.  
  
```  
public Type GetDataContractType(Type type)  
{  
    if (typeof(Person).IsAssignableFrom(type))  
    {  
        return typeof(PersonSurrogated);  
    }  
    return type;  
}  
  
```  
  
 Метод <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%28System.Object%2CSystem.Type%29> сопоставляет экземпляр класса `Person` с экземпляром класса `PersonSurrogated` во время сериализации, как показано в следующем образце кода.  
  
```  
public object GetObjectToSerialize(object obj, Type targetType)  
{  
    if (obj is Person)  
    {  
        Person person = (Person)obj;  
        PersonSurrogated personSurrogated = new PersonSurrogated();  
        personSurrogated.FirstName = person.firstName;  
        personSurrogated.LastName = person.lastName;  
        personSurrogated.Age = person.age;  
        return personSurrogated;  
    }  
    return obj;  
}  
  
```  
  
 Метод <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDeserializedObject%28System.Object%2CSystem.Type%29> обеспечивает обратное сопоставление для десериализации, как показано в следующем образце кода.  
  
```  
public object GetDeserializedObject(object obj,   
Type targetType)  
{  
    if (obj is PersonSurrogated)  
    {  
        PersonSurrogated personSurrogated = (PersonSurrogated)obj;  
        Person person = new Person();  
        person.firstName = personSurrogated.FirstName;  
        person.lastName = personSurrogated.LastName;  
        person.age = personSurrogated.Age;  
        return person;  
    }  
    return obj;  
}  
  
```  
  
 Чтобы сопоставить контракт данных `PersonSurrogated` с существующим классом `Person` во время импорта схемы, в образце реализуется метод <xref:System.Runtime.Serialization.IDataContractSurrogate.GetReferencedTypeOnImport%28System.String%2CSystem.String%2CSystem.Object%29>, как показано в следующем образце кода.  
  
```  
public Type GetReferencedTypeOnImport(string typeName,   
               string typeNamespace, object customData)  
{  
if (  
typeNamespace.Equals("http://schemas.datacontract.org/2004/07/DCSurrogateSample")  
)  
    {  
         if (typeName.Equals("PersonSurrogated"))  
        {  
             return typeof(Person);  
        }  
     }  
     return null;  
}  
  
```  
  
 В следующем образце кода показано завершение реализации интерфейса <xref:System.Runtime.Serialization.IDataContractSurrogate>.  
  
```  
public System.CodeDom.CodeTypeDeclaration ProcessImportedType(  
          System.CodeDom.CodeTypeDeclaration typeDeclaration,   
          System.CodeDom.CodeCompileUnit compileUnit)  
{  
    return typeDeclaration;  
}  
public object GetCustomDataToExport(Type clrType,   
                               Type dataContractType)  
{  
    return null;  
}  
  
public object GetCustomDataToExport(  
System.Reflection.MemberInfo memberInfo, Type dataContractType)  
{  
    return null;  
}  
public void GetKnownCustomDataTypes(  
        KnownTypeCollection customDataTypes)  
{  
    // It does not matter what we do here.  
    throw new NotImplementedException();  
}  
  
```  
  
 В этом образце заменяющий класс включается в ServiceModel с помощью атрибута `AllowNonSerializableTypesAttribute`.Разработчикам пришлось бы применить этот атрибут к контракту службы, как показано в контракте службы `IPersonnelDataService` выше.Этот атрибут реализует `IContractBehavior` и настраивает заменяющий класс в операциях методов `ApplyClientBehavior` и `ApplyDispatchBehavior`.  
  
 В этом случае необходимости в атрибуте нет. В этом образце он используется в демонстрационных целях.Пользователи могут также включить заменяющий класс вручную, добавив похожее поведение `IContractBehavior`, `IEndpointBehavior` или `IOperationBehavior` с использованием кода или конфигурации.  
  
 Реализация `IContractBehavior` ищет операции, в которых используется DataContract, проверяя в них наличие зарегистрированного поведения `DataContractSerializerOperationBehavior`.При его наличии она задает свойство `DataContractSurrogate` для этого поведения.В следующем образце кода показано, как это можно сделать.Задание заменяющего класса для этого поведения операции позволяет ему участвовать в сериализации и десериализации.  
  
```  
public void ApplyClientBehavior(ContractDescription description, ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.ClientRuntime proxy)  
{  
    foreach (OperationDescription opDesc in description.Operations)  
    {  
        ApplyDataContractSurrogate(opDesc);  
    }  
}  
  
public void ApplyDispatchBehavior(ContractDescription description, ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.DispatchRuntime dispatch)  
{  
    foreach (OperationDescription opDesc in description.Operations)  
    {  
        ApplyDataContractSurrogate(opDesc);  
    }  
}  
  
private static void ApplyDataContractSurrogate(OperationDescription description)  
{  
    DataContractSerializerOperationBehavior dcsOperationBehavior = description.Behaviors.Find<DataContractSerializerOperationBehavior>();  
    if (dcsOperationBehavior != null)  
    {  
        if (dcsOperationBehavior.DataContractSurrogate == null)  
            dcsOperationBehavior.DataContractSurrogate = new AllowNonSerializableTypesSurrogate();  
    }  
}  
```  
  
 Чтобы подключить заменяющий класс для использования при создании метаданных, необходимо выполнить дополнительные действия.Одним из механизмов реализации этого является предоставление расширения `IWsdlExportExtension`, как показано в этом образце.Еще одним способом является непосредственное изменение `WsdlExporter`.  
  
 Атрибут `AllowNonSerializableTypesAttribute` реализует `IWsdlExportExtension` и `IContractBehavior`.В этом случае расширение может быть как `IContractBehavior`, так и `IEndpointBehavior` .Реализация метода `IWsdlExportExtension.ExportContract` включает заменяющий класс путем его добавления в `XsdDataContractExporter`, используемый во время создания схемы для DataContract.В следующем фрагменте кода показано, как это сделать.  
  
```  
public void ExportContract(WsdlExporter exporter, WsdlContractConversionContext context)  
{  
    if (exporter == null)  
        throw new ArgumentNullException("exporter");  
  
    object dataContractExporter;  
    XsdDataContractExporter xsdDCExporter;  
    if (!exporter.State.TryGetValue(typeof(XsdDataContractExporter), out dataContractExporter))  
    {  
        xsdDCExporter = new XsdDataContractExporter(exporter.GeneratedXmlSchemas);  
        exporter.State.Add(typeof(XsdDataContractExporter), xsdDCExporter);  
    }  
    else  
    {  
        xsdDCExporter = (XsdDataContractExporter)dataContractExporter;  
    }  
    if (xsdDCExporter.Options == null)  
        xsdDCExporter.Options = new ExportOptions();  
  
    if (xsdDCExporter.Options.DataContractSurrogate == null)  
        xsdDCExporter.Options.DataContractSurrogate = new AllowNonSerializableTypesSurrogate();  
}  
```  
  
 При выполнении образца клиент вызывает операцию AddEmployee после вызова операции GetEmployee, чтобы проверить, выполнен ли первый вызов успешно.Результат запроса операции GetEmployee отображается в окне консоли клиента.Операция GetEmployee должна успешно выполнить поиск сотрудника и вывести результат "found".  
  
> [!NOTE]
>  В этом примере показано, как подключить заменяющий класс для сериализации, десериализации и создания метаданных.В нем не показано, как подключить заменяющий класс для создания кода из метаданных.Образец использования заменяющего класса для создания кода клиента см. в образце [Пользовательская публикация WSDL](../../../../docs/framework/wcf/samples/custom-wsdl-publication.md).  
  
### Настройка, построение и выполнение образца  
  
1.  Убедитесь, что выполнены процедуры, описанные в разделе [Процедура однократной настройки образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Чтобы построить версию решения для языка C\#, воспользуйтесь инструкциями в разделе [Построение образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Чтобы выполнить образец на одном или нескольких компьютерах, следуйте инструкциям в разделе [Выполнение примеров Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Этот образец расположен в следующем каталоге.  
>   
>  `<диск_установки>:\WF_WCF_Samples\WCF\Extensibility\DataContract`  
  
## См. также