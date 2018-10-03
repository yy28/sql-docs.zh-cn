---
title: 使用 CommandText 属性执行模板文件 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], executing template files
- SQLXML Managed Classes, executing template files
- templates [SQLXML], SQLXML Managed Classes
- executing template files [SQLXML]
- CommandText property
ms.assetid: f1b1278d-252d-4a06-836e-4ef77f338ef9
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1d78a1c9823bdce65eb946ebf2ab7c9d75463d0f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781725"
---
# <a name="executing-template-files-by-using-the-commandtext-property"></a>使用 CommandText 属性执行模板文件
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  此示例说明了如何通过使用 CommandTextproperty 指定 SQL 或 XPath 查询组成的模板文件。 而不是作为 CommandText 值中指定的 SQL 或 XPath 查询，可以指定文件名称，作为值。 在以下示例中，CommandType 属性指定为 SqlXmlCommandType.TemplateFile。  
  
 示例应用程序执行下面的模板：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
    SELECT TOP 2 ContactID, FirstName, LastName   
    FROM   Person.Contact  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 这是 C# 示例应用程序。 若要测试该应用程序，请保存模板 (TemplateFile.xml)，然后执行该应用程序。  
  
> [!NOTE]  
>  在代码中，必须在连接字符串中提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
  
      public static int testParams()  
      {  
         //Stream strm;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandType = SqlXmlCommandType.TemplateFile;  
         cmd.CommandText = "TemplateFile.xml";  
         using (Stream strm = cmd.ExecuteStream()){  
            using (StreamReader sr = new StreamReader(strm)){  
                Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
  
         return 0;        
      }  
      public static int Main(String[] args)  
      {  
         testParams();     
         return 0;  
      }  
   }  
```  
  
### <a name="to-test-the-application"></a>测试应用程序  
  
1.  确保已在计算机上安装了 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework。  
  
2.  将该示例中提供的 XML 模板 (TemplateFile.xml) 保存在某个文件夹中。  
  
3.  在此示例中在其中存储架构的同一文件夹中保存的 C# 代码 (DocSample.cs) 提供。 （如果将文件存储在其他文件夹中，则必须编辑代码并为映射架构指定相应的目录路径。）  
  
4.  编译代码。 若要在命令提示符下编译此代码，请使用：  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     这将创建一个可执行文件 (DocSample.exe)。  
  
5.  在命令提示符下，执行 DocSample.exe。  
  
 如果向模板传递参数，参数名称必须以 at 符号 (@);例如，p.Name="\@ContactID"，其中 p 是 SqlXmlParameter 对象。  
  
 下面是接受一个参数后的已更新模板。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:header>  
     <sql:param name='ContactID'>1</sql:param>    
  </sql:header>  
  <sql:query>  
    SELECT ContactID, FirstName, LastName  
    FROM   Person.Contact  
    WHERE  ContactID=@ContactID  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 下面是传递参数所使用的已更新代码，用于执行模板。  
  
```  
public static int testParams()  
{  
  
   Stream strm;  
   SqlXmlParameter p;  
  
   SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
   cmd.CommandType = SqlXmlCommandType.TemplateFile;  
   cmd.CommandText = "TemplateFile.xml";  
   p = cmd.CreateParameter();  
   p.Name="@ContactID";  
   p.Value = "1";  
   strm = cmd.ExecuteStream();  
   StreamReader sw = new StreamReader(strm);  
   Console.WriteLine(sw.ReadToEnd());  
   return 0;        
}  
```  
  
  
