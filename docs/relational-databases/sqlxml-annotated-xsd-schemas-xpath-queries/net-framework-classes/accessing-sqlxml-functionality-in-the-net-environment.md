---
title: 在 .NET 环境中访问 SQLXML 功能
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], accessing SQLXML functionality
- SQLXML Managed Classes, accessing SQLXML functionality
- DiffGrams [SQLXML], accessing SQLXML functionality
- .NET Framework [SQLXML], accessing SQLXML functionality
ms.assetid: 74744535-2945-414d-9a5b-7e8cc363953a
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9a5edd3555c2d57cf9d615b7158d034571987cb5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "75251519"
---
# <a name="accessing-sqlxml-functionality-in-the-net-environment"></a>在 .NET 环境中访问 SQLXML 功能
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  此示例显示：  
  
-   如何使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 托管类（node.js）在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 环境中访问 Microsoft。  
  
-   在 .NET Framework 环境中生成的 DiffGram 如何向 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表应用数据更新。  
  
 在此应用程序中，XPath 查询是针对 XSD 架构执行的。 XPath 查询的执行将返回一个由联系人数据（**FirstName**， **LastName**）组成的 XML 文档。 应用程序在 .NET Framework 环境中将 XML 文档加载到数据集。 修改该数据集中的数据：对于数据集中的第一个联系人，该联系人的名字被更改为“Susan”。 从该数据集生成 DiffGram，然后将在 DiffGram 中指定的更新（雇员名字的更改）应用到 Person.Contact 表。  
  
> [!NOTE]  
>  在该代码中，必须在连接字符串中提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=SqlServerName;database=AdventureWorks;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      DataRow row;  
      SqlXmlAdapter ad;  
      //need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandText = "Con";  
      cmd.CommandType = SqlXmlCommandType.XPath;  
      cmd.SchemaPath = "MySchema.xml";  
      //load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      row = ds.Tables["Con"].Rows[0];  
      row["FName"] = "Susan";  
      ad.Update(ds);  
      return 0;  
   }  
   public static int Main(String[] args)  
   {  
      testParams();  
      return 0;  
   }  
}  
```  
  
 **测试示例：**  
  
 若要测试该示例，必须在计算机上安装 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework。  
  
1.  将此 XSD 架构 (MySchema.xml) 保存在文件夹中：  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Con" sql:relation="Person.Contact" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="FName"    
                         sql:field="FirstName"   
                         type="xsd:string" />   
            <xsd:element name="LName"    
                         sql:field="LastName"    
                         type="xsd:string" />  
         </xsd:sequence>  
         <xsd:attribute name="ContactID" type="xsd:integer" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
2.  将在该示例中提供的 C# 代码 (DocSample.cs) 保存到存储架构的相同文件夹中。 （如果将文件存储在其他文件夹中，则必须编辑代码并为映射架构指定相应的目录路径。）  
  
3.  编译代码。 若要在命令提示符下编译此代码，请使用：  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     这将创建一个可执行文件 (DocSample.exe)。  
  
 在命令提示符下，执行 DocSample.exe。  
  
  
