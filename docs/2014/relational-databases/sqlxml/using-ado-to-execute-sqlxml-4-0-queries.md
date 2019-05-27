---
title: 使用 ADO 执行 SQLXML 4.0 查询 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- query testers [SQLXML]
- test scripts
- ADO [SQLXML]
- queries [SQLXML], ADO
- SQLXML, ADO
ms.assetid: 3d54e3bb-7c5f-427e-82f8-1403a54c4f53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2a8f5cdb74385852a0feef0f9de0d760eb57f13
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66012150"
---
# <a name="using-ado-to-execute-sqlxml-40-queries"></a>使用 ADO 执行 SQLXML 4.0 查询
  在 SQLXML 的早期版本中，使用 SQLXML IIS 虚拟目录和 SQLXML ISAPI 筛选器支持基于 HTTP 的查询执行。 在 SQLXML 4.0 中，由于从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，本机 XML Web 服务提供了类似的重叠功能，因此已删除上述组件。  
  
 或者，您也可以利用在 Microsoft 数据访问组件 (MDAC) 2.6 中首次引入并在后续版本中延续使用的 ActiveX 数据对象 (ADO) 的 SQLXML 扩展来执行查询，并配合使用 SQLXML 4.0 和基于 COM 的应用程序。  
  
 本主题说明了如何将 SQLXML 和 ADO 作为 Visual Basic Scripting Edition (VBScript) 应用程序（带有 .vbs 文件扩展名的脚本）的一部分使用。 本主题还提供了可帮助您重新创建和测试 SQLXML 4.0 文档中的查询示例的初始设置过程。  
  
## <a name="creating-the-sqlxml-40-test-script"></a>创建 SQLXML 4.0 测试脚本  
 在此过程中，您将创建一个 VBScript (.vbs) 文件（即 Sqlxml4test.vbs），利用 ADO 2.6 和更高版本中的 SQLXML ADO 扩展，您可以使用该文件执行 SQLXML 查询。  
  
#### <a name="to-create-the-sqlxml-40-query-tester-using-ado-vbscript"></a>使用 ADO (VBScript) 创建 SQLXML 4.0 查询测试程序。  
  
1.  将以下代码复制并粘贴到文本文件。 将该文件另存为 Sqlxml4test.vbs。  
  
    ```  
    WScript.Echo "Query process may take a few seconds to complete. Please be patient."  
  
    ' Note that for SQL Server Native Client to be used as the data provider,  
    ' it needs to be installed on the client computer first. Also, SQLXML extensions   
    ' for ADO are used and available in MDAC 2.6 or later.  
  
    'Set script variables.  
    inputFile = "@@FILE_NAME@@"  
    strServer = "@@SERVER_NAME@@"  
    strDatabase = "@@DATABASE_NAME@@"  
    dbGuid = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  
    ' Establish ADO connection to SQL Server and   
    ' create an instance of the ADO Command object.  
    Set conn = CreateObject("ADODB.Connection")  
    Set cmd = CreateObject("ADODB.Command")  
    conn.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Server=" & strServer & _  
              ";Database=" & strDatabase & ";Integrated Security=SSPI"  
    Set cmd.ActiveConnection = conn  
  
    ' Create the input stream as an instance of the ADO Stream object.  
    Set inStream = CreateObject("ADODB.Stream")  
    inStream.Open  
    inStream.Charset = "utf-8"  
    inStream.LoadFromFile inputFile  
  
    ' Set ADO Command instance to use input stream.  
    Set cmd.CommandStream = inStream  
  
    ' Set the command dialect.  
    cmd.Dialect = dbGuid  
  
    ' Set a second ADO Stream instance for use as a results stream.   
    Set outStream = CreateObject("ADODB.Stream")  
    outStream.Open  
  
    ' Set dynamic properties used by the SQLXML ADO command instance.   
    cmd.Properties("XML Root").Value = "ROOT"  
    cmd.Properties("Output Encoding").Value = "UTF-8"  
  
    ' Connect the results stream to the command instance and execute the command.  
    cmd.Properties("Output Stream").Value = outStream  
    cmd.Execute , , 1024  
  
    ' Echo cropped/partial results to console.  
    WScript.Echo Left(outStream.ReadText, 1023)  
  
    inStream.Close  
    outStream.Close  
    ```  
  
2.  为尝试测试的示例和测试环境更新以下脚本值。  
  
    -   查找“`@@FILE_NAME@@`”并将其替换为模板文件的名称。  
  
    -   查找“`@@SERVER_NAME@@`”并将其替换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称（例如，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在本地运行，则替换为“`(local)`”）。  
  
    -   查找“`@@DATABASE_NAME@@`”并将其替换为数据库名称（例如，“`AdventureWorks2012`”或“`tempdb`”）。  
  
     如果尝试在本地计算机上重新创建的示例的特定说明提到了任何其他值，则必须更新这些值。  
  
3.  保存文件并将其关闭。  
  
4.  确定已创建作为尝试在本地计算机上重新创建的示例的一部分的所有附加文件，例如 XML 模板或架构。 这些文件应位于您保存测试脚本文件 (Sqlxml4test.vbs) 的相同目录中。  
  
5.  按照下一部分中如何使用 SQLXML 4.0 测试脚本的说明操作。  
  
## <a name="using-the-sqlxml-40-test-script"></a>使用 SQLXML 4.0 测试脚本  
 以下过程说明如何使用 Sqlxml4test.vbs 文件测试本文档中提供的示例查询。  
  
#### <a name="to-use-the-sqlxml-40-query-tester"></a>使用 SQLXML 4.0 查询测试程序  
  
1.  验证是否安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client，如下所示：  
  
    1.  从**启动**菜单，依次指向**设置**，然后单击**控制面板**。  
  
    2.  在控制面板中，打开**添加或删除程序**  
  
    3.  在当前安装的程序列表中，确认**Microsoft SQL Server Native Client**出现在列表中。  
  
        > [!NOTE]  
        >  如果你需要安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client，请参阅[安装 SQL Server Native Client](../native-client/applications/installing-sql-server-native-client.md)。  
  
2.  验证客户端计算机上安装的 MDAC 版本是否为 2.6 版或更高版本。 如果需要验证 MDAC 版本信息，您可以使用 MDAC 组件检查器工具，可从 Microsoft 网站 (www.microsoft.com) 免费下载该工具。 有关详细信息，请在此 Microsoft 网站中搜索“MDAC Component 检查器”。  
  
3.  执行脚本。  
  
     您可以在命令行使用 Cscript.exe 来执行 VBScript 文件，也可以通过双击 Sqlxml4test.vbs 文件调用 Windows 脚本宿主 (WScript.exe) 来执行该文件。  
  
     执行时，脚本应显示一则消息，通知您在返回并显示查询结果作为脚本输出之前，执行此脚本可能需要花费一些时间。 显示输出时，请将其内容与示例的预期结果相比较。  
  
  
