---
title: 执行带命名空间的 XPath 查询 （SQLXML 托管类） |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- namespaces property
- XPath queries [SQLXML], SQLXML Managed Classes
- queries [SQLXML], SQLXML Managed Classes
- XPath queries [SQLXML], namespaces
- Managed Classes [SQLXML], executing XPath queries
- SQLXML Managed Classes, executing XPath queries
- namespaces [SQLXML], XPath queries
ms.assetid: c6fc46d8-6b42-4992-a8f1-a8d4b8886e6e
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6855136c4f636ca0fb74f0d806ac191b201f1709
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43069500"
---
# <a name="executing-xpath-queries-with-namespaces-sqlxml-managed-classes"></a>执行带命名空间的 XPath 查询（SQLXML 托管类）
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XPath 查询可以包含命名空间。 如果架构元素为限定命名空间（使用目标命名空间），则针对该架构的 XPath 查询必须指定该命名空间。  
  
 由于 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 中不支持使用通配符 (*)，因此必须使用命名空间前缀来指定 XPath 查询。 若要解析此前缀，使用命名空间属性指定命名空间绑定。  
  
 在以下示例中，XPath 查询指定命名空间使用通配符字符 (\*) 和 local-name （) and namespace-uri （) XPath 函数。 此 XPath 查询返回所有元素，其中的本地名称是**员工**和命名空间 URI 为**urn: myschema:Contacts**:  
  
```  
/*[local-name() = 'Contact' and namespace-uri() = 'urn:myschema:Contacts']  
```  
  
 在 SQLXML 4.0 中，用命名空间前缀来指定此 XPath 查询。 例如， **x： 请联系**，其中**x**为命名空间前缀。 请看以下 XSD 架构：  
  
```  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:con="urn:myschema:Contacts"  
            targetNamespace="urn:myschema:Contacts">  
<complexType name="ContactType">  
  <attribute name="CID" sql:field="ContactID" type="ID"/>  
  <attribute name="FName" sql:field="FirstName" type="string"/>  
  <attribute name="LName" sql:field="LastName"/>   
</complexType>  
<element name="Contact" type="con:ContactType" sql:relation="Person.Contact"/>  
</schema>  
```  
  
 此架构所定义的目标命名空间，因为 （例如"Employee") 针对此架构的 XPath 查询必须包括命名空间。  
  
 以下 C# 应用程序示例针对前述 XSD 架构 (MySchema.xml) 执行 XPath 查询。 若要解析此前缀，请使用 SqlXmlCommand 对象的命名空间属性指定命名空间绑定。  
  
> [!NOTE]  
>  在该代码中，必须在连接字符串中提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testXPath()  
      {  
         //Stream strm;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandText = "x:Contact[@CID='1']";  
         cmd.CommandType = SqlXmlCommandType.XPath;  
         cmd.RootTag = "ROOT";  
         cmd.Namespaces = "xmlns:x='urn:myschema:Contacts'";  
         cmd.SchemaPath = "MySchema.xml";  
         using (Stream strm = cmd.ExecuteStream()){  
            using (StreamReader sr = new StreamReader(strm)){  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;  
      }  
      public static int Main(String[] args)  
      {  
         testXPath();  
         return 0;  
      }  
   }  
```  
  
 若要测试该示例，必须在计算机上安装 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework。  
  
### <a name="to-test-the-application"></a>测试应用程序  
  
1.  将在该示例中提供的 XSD 架构 (MySchema.xml) 保存到某个文件夹中。  
  
2.  在此示例中在其中存储架构的同一文件夹中保存的 C# 代码 (DocSample.cs) 提供。 （如果将文件存储在其他文件夹中，则必须编辑代码并为映射架构指定相应的目录路径。）  
  
3.  编译代码。 若要在命令提示符下编译此代码，请使用：  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     这将创建一个可执行文件 (DocSample.exe)。  
  
4.  在命令提示符下，执行 DocSample.exe。  
  
  
