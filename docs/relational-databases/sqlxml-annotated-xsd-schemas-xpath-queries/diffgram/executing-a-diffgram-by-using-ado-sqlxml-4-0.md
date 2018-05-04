---
title: 使用 ADO (SQLXML 4.0) 执行 DiffGram |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], SQLOLEDB Provider
- ADO [SQLXML]
- SQLXMLOLEDB Provider, DiffGrams
- data providers [SQLXML], SQLOLEDB Provider
- DiffGrams [SQLXML], ADO
ms.assetid: 741fce82-de83-4923-86eb-30acb5b9a5e6
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0abe2dca94097aa084adc7100059b4e802a50b58
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="executing-a-diffgram-by-using-ado-sqlxml-40"></a>使用 ADO 执行 DiffGram (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  该 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 应用程序使用 ADO 建立与 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的连接，然后执行 DiffGram。 在该应用程序中，DiffGram 和 XSD 架构存储在文件中。 该应用程序从指定的文件加载 DiffGram。 你可以使用任一 Diffgram （和关联的 XSD 架构） 中所述[DiffGram 示例](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。  
  
 以下是示例应用程序的过程：  
  
-   **Conn**对象 (**ADODB。连接**) 建立到 SQL Server 的特定服务器上运行的实例的连接。  
  
-   **Cmd**对象 (**ADODB.Command**) 建立的连接上执行。  
  
-   将命令方言设置为 DBGUID_MSSQLXML。  
  
-   DiffGram 复制到命令流 (**strmIn**) 从文件。  
  
-   命令的输出流设置为**StrmOut**对象 (**ADODB。流式传输**) 接收任何返回的数据。  
  
-   当使用 SQLOLEDB 访问接口时，默认情况下，您将获取 Sqlxmlx.dll 提供的 Microsoft SQLXML 功能。 若要将与 SQLOLEDB 访问接口，使用 Sqlxml4.dll **SQLXML 版本**属性必须设置为**SQLXML.4.0** SQLOLEDB 访问接口上**连接**对象。  
  
-   执行该命令 (DiffGram)。  
  
 以下代码为示例应用程序。  
  
> [!NOTE]  
>  在该代码中，必须在连接字符串中提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。  
  
```  
Private Sub Command1_Click()  
  Dim cmd As New ADODB.Command  
  Dim conn As New ADODB.Connection  
  Dim strmOut As New ADODB.Stream  
  Dim strmIn As New ADODB.Stream  
  
  'Open a connection to SQL Server.  
  conn.Provider = "SQLOLEDB"  
  conn.Open "server=SqlServerName; database=tempdb; Integrated Security=SSPI; "  
  conn.Properties("SQLXML Version") = "SQLXML.4.0"  
  Set cmd.ActiveConnection = conn  
  strmIn.Open  
  strmIn.Charset = "UTF-8"  
  strmIn.LoadFromFile "C:\SomeFilePath\SampleDiffGram.xml"  
  strmIn.Position = 0  
  Set cmd.CommandStream = strmIn  
  
  strmOut.Open  
  cmd.Properties("Output Stream").Value = strmOut  
  cmd.Properties("Output Encoding").Value = "UTF-8"  
  
  cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  cmd.Properties("Mapping Schema") = "C:\SomeFilePath\SampleDiffGram.xml"  
  cmd.Execute , , adExecuteStream  
  strmOut.Position = 0  
  Set cmd = Nothing  
  strmOut.Charset = "UTF-8"  
  strmOut.SaveToFile "C:\DropIt.txt", adSaveCreateOverWrite  
  strmOut.Close  
  Set strmOut = Nothing  
  
End Sub  
```  
  
### <a name="to-test-the-diffgram"></a>测试 DiffGram  
  
1.  到你的计算机上的文件夹，将 Diffgram 和相应的 XSD 架构的任何一个复制中的示例之一[DiffGram 示例](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。  
  
2.  打开 Visual Basic 并创建标准 EXE 项目。  
  
3.  将这些引用添加到项目中：  
  
    ```  
    Microsoft ActiveX Data Objects 2.8 Library  
    ```  
  
4.  在工具箱中，单击**CommandButton**，然后在窗体上绘制按钮。  
  
5.  双击该按钮编辑代码，并添加本主题中提供的应用程序代码。  
  
6.  编辑代码以指定 DiffGram 和 XSD 文件名， 并根据需要编辑连接字符串。  
  
7.  执行应用程序。 执行结果取决于您执行的 DiffGram。  
  
  
