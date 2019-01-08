---
title: 移动 Analysis Services 数据库 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- moving databases [Anlysis Services]
- moving databases
- operations [Analysis Services - multidimensional data]
ms.assetid: fa644e5d-e276-445e-98d9-673afcfb83fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0939540af0c302832925a7a1bef6367718b8c1be
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369276"
---
# <a name="move-an-analysis-services-database"></a>移动 Analysis Services 数据库
  很多情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库管理员 (dba) 希望将多维或表格模型数据库移到另一个位置。 根据业务需要（例如，将数据库移到另一个磁盘以获得更好的性能、为数据库扩容获取空间或升级产品），经常需要进行上述操作。  
  
 可以通过多种方式来移动数据库。 本文档介绍下列常见方案：  
  
-   使用 SSMS 以交互方式  
  
-   使用 AMO 以编程方式  
  
-   使用 XMLA 借助于脚本  
  
 所有方案都要求用户能够访问数据库文件夹并使用某种方法将文件移到所需的最终目标。  
  
> [!NOTE]  
>  在不向数据库分配密码的情况下分离数据库会使该数据库处于不安全状态。 我们建议您为数据库分配密码以保护机密信息。 还要向数据库文件夹、子文件夹和文件应用相应的访问安全性以防止对它们进行未经授权的访问。  
  
## <a name="procedures"></a>过程  
  
#### <a name="moving-a-database-interactively-using-ssms"></a>使用 SSMS 以交互方式移动数据库  
  
1.  在 SSMS 的左窗格或右窗格中找到要移动的数据库。  
  
2.  右键单击数据库并选择**分离...**  
  
3.  为要分离的数据库分配一个密码，然后单击 **“确定”** 执行分离命令。  
  
4.  使用可用来移动文件的任何操作系统机制或标准方法，将数据库文件夹移到新位置。  
  
5.  在 SSMS 的左窗格或右窗格中找到 **“数据库”** 文件夹。  
  
6.  右键单击**数据库**文件夹，然后选择**附加...**  
  
7.  在 **“文件夹”** 文本框中，键入数据库文件夹的新位置。 或者，可以使用浏览按钮 (**...**) 以查找数据库文件夹。  
  
8.  选择`ReadWrite`数据库模式。  
  
9. 键入步骤 3 中使用的密码，然后单击 **“确定”** 执行附加命令。  
  
#### <a name="moving-a-database-programmatically-using-amo"></a>使用 AMO 以编程方式移动数据库  
  
1.  在 C# 应用程序中，修改以下示例代码并完成所指示的任务。  
  
 `private void MoveDb(Server server, string dbName,`  
  
 `string dbInitialLocation, string dbFinalLocation,`  
  
 `string dbPassword, ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `//Verify dbInitialLocation exists before continuing`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `//Save current cursor and change cursor to Cursors.WaitCursor`  
  
 `db = server.Databases[dbName];`  
  
 `db.Detach(dbPassword);`  
  
 `//Add your own code to copy the database files to the destination where you intend to attach the database`  
  
 `//Verify dbFinalLocation exists before continuing`  
  
 `server.Attach(dbFinalLocation, dbReadWriteMode, dbPassword);`  
  
 `//Restore cursor to its original`  
  
 `}`  
  
 `}`  
  
1.  在 C# 应用程序中，用必要的参数调用 `MoveDb()` 。  
  
2.  编译和执行您的代码以移动该数据库。  
  
#### <a name="moving-a-database-by-script-using-xmla"></a>使用 XMLA 借助于脚本移动数据库  
  
1.  在 SSMS 中打开一个新的 XMLA 选项卡。  
  
2.  复制下面的 XMLA 脚本模板  
  
 `<Detach xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  将 `%dbName%` 替换为数据库名称，将 `%password%` 替换为您的密码。 % 字符是模板的一部分，必须将其删除。  
  
2.  执行 XMLA 命令。  
  
3.  使用可用来移动文件的任何操作系统机制或标准方法，将数据库文件夹移到新位置。  
  
4.  在新的 XMLA 选项卡中复制下面的 XMLA 脚本模板  
  
 `<Attach xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="https://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  将 `%dbFolder%` 替换为数据库文件夹的完整 UNC 路径，将 `%ReadOnlyMode%` 替换为相应值（`ReadOnly` 或 `ReadWrite`），并将 `%password%` 替换为您的密码。 % 字符是模板的一部分，必须将其删除。  
  
2.  执行 XMLA 命令。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [附加和分离 Analysis Services 数据库](attach-and-detach-analysis-services-databases.md)   
 [数据库存储位置](database-storage-location.md)   
 [数据库 ReadWriteMode](database-readwritemodes.md)   
 [附加元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [分离元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [ReadWriteMode 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/readwritemode-element)   
 [DbStorageLocation 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)  
  
  
