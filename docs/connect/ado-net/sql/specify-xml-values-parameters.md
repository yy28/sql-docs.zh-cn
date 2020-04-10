---
title: 将 XML 值指定为参数
description: 演示如何将 XML 数据作为参数传递给命令。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 2c4d08b8-fc29-4614-97fa-29c8ff7ca5b3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: f53811919e6bec8e1d5c5985c303e282ce81ed07
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919993"
---
# <a name="specifying-xml-values-as-parameters"></a>将 XML 值指定为参数

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

如果查询需要值为 XML 字符串的参数，开发人员可以使用 SqlXml 数据类型的实例提供该值  。 真的没有任何窍门；SQL Server 中的 XML 列接受参数值的方式与其他数据类型完全相同。  
  
## <a name="example"></a>示例  
以下控制台应用程序在 AdventureWorks 数据库中新建一个表  。 新表包括一个名为 SalesID 的列和一个名为 SalesInfo 的 XML 列   。  
  
> [!NOTE]
>  默认情况下，在安装 SQL Server 时不安装 AdventureWorks 示例数据库  。 可以通过运行 SQL Server 安装程序来安装它。  
  
该示例准备一个 <xref:Microsoft.Data.SqlClient.SqlCommand> 对象以在新表中插入行。 保存的文件为 SalesInfo 列提供所需的 XML 数据  。  
  
若要创建运行示例所需的文件，请在与项目相同的文件夹中创建一个新的文本文件。 将文件命名为 MyTestStoreData.xml。 在记事本中打开该文件，然后复制并粘贴以下文本：  
  
```xml  
<StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>International Bank</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1970</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>7000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>T1</Internet>  
  <NumberEmployees>2</NumberEmployees>  
</StoreSurvey>  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
using System.Xml;  
using System.Data.SqlTypes;  
  
class Class1  
{  
    static void Main()  
    {  
        using (SqlConnection connection = new SqlConnection(GetConnectionString()))  
       {  
        connection.Open();  
        //  Create a sample table (dropping first if it already  
        //  exists.)  
  
        string commandNewTable =   
            "IF EXISTS (SELECT * FROM dbo.sysobjects " +   
            "WHERE id = " +  
                  "object_id(N'[dbo].[XmlDataTypeSample]') " +   
            "AND OBJECTPROPERTY(id, N'IsUserTable') = 1) " +   
            "DROP TABLE [dbo].[XmlDataTypeSample];" +   
            "CREATE TABLE [dbo].[XmlDataTypeSample](" +   
            "[SalesID] [int] IDENTITY(1,1) NOT NULL, " +   
            "[SalesInfo] [xml])";  
        SqlCommand commandAdd =   
                   new SqlCommand(commandNewTable, connection);  
        commandAdd.ExecuteNonQuery();  
        string commandText =   
            "INSERT INTO [dbo].[XmlDataTypeSample] " +   
            "([SalesInfo] ) " +   
            "VALUES(@xmlParameter )";  
        SqlCommand command =   
                  new SqlCommand(commandText, connection);  
  
        //  Read the saved XML document as a   
        //  SqlXml-data typed variable.  
        SqlXml newXml =   
            new SqlXml(new XmlTextReader("MyTestStoreData.xml"));  
  
        //  Supply the SqlXml value for the value of the parameter.  
        command.Parameters.AddWithValue("@xmlParameter", newXml);  
  
        int result = command.ExecuteNonQuery();  
        Console.WriteLine(result + " row was added.");  
        Console.WriteLine("Press Enter to continue.");  
        Console.ReadLine();  
    }  
  }  
  
    private static string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,              
        // you can retrieve it from a configuration file.   
        return "Data Source=(local);Integrated Security=true;" +  
        "Initial Catalog=AdventureWorks; ";  
    }  
}  
```  
  
## <a name="next-steps"></a>后续步骤
- <xref:System.Data.SqlTypes.SqlXml>
- [SQL Server 中的 XML 数据](xml-data-sql-server.md)
