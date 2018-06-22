---
title: 切换 ReadOnly 和 ReadWrite 模式之间的 Analysis Services 数据库 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ReadOnly property
- ReadWriteMode command
- operations [Analysis Services - multidimensional data]
ms.assetid: 4eff8181-08dd-4fad-b091-d400fc21a020
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 184a674d03e6c8fb6b30d10b91b2a58225894ba2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014410"
---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>在 ReadOnly 和 ReadWrite 模式之间切换 Analysis Services 数据库
  通常情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库管理员 (dba) 需要更改表格的读/写模式或多维数据库。 根据业务需要（如在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器池中共享数据库以获得更好的用户体验），经常需要进行上述操作。  
  
 可以通过多种方式来切换数据库模式。 本文档介绍下列常见方案：  
  
-   使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   使用 AMO 以编程方式  
  
-   使用 XMLA 借助于脚本  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>使用 Management Studio 以交互方式切换数据库的读写模式  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的左窗格或右窗格中找到要切换的数据库。  
  
2.  右键单击该数据库并选择 **“属性”**。 查找数据库文件夹并记下其位置。 如果数据库存储位置为空，则表明数据库文件夹位于服务器数据文件夹中。  
  
    > [!IMPORTANT]  
    >  在将数据库分离之后， [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 就不能再帮助您获取数据库位置。  
  
3.  右键单击该数据库并选择 **“分离 ”**。  
  
4.  为要分离的数据库分配一个密码，然后单击 **“确定”** 执行分离命令。  
  
5.  在 **的左窗格或右窗格中找到** “数据库” [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]文件夹。  
  
6.  右键单击 **“数据库”** 文件夹并选择 **“分离 ”**。  
  
7.  在 **“文件夹”** 文本框中，键入数据库文件夹的原始位置。 也可以使用浏览按钮 (**…**) 查找数据库文件夹。  
  
8.  针对该数据库选择读写模式。  
  
9. 键入步骤 3 中使用的密码，然后单击 **“确定”** 执行附加命令。  
  
#### <a name="to-switch-the-readwrite-mode-to-a-database-programmatically-using-amo"></a>使用 AMO 以编程方式切换数据库的读写模式  
  
1.  在 C# 应用程序中，修改以下示例代码并完成所指示的任务。  
  
 `private void SwitchReadWrite(Server server, string dbName,`  
  
 `ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `string databaseLocation;`  
  
 `db = server.Databases[dbName];`  
  
 `databaseLocation = db.DbStorageLocation;`  
  
 `if (databaseLocation == null)`  
  
 `{`  
  
 `string dataDir = server.ServerProperties["DataDir"].Value;`  
  
 `String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);`  
  
 `if (possibleFolders.Length > 1)`  
  
 `{`  
  
 `List<String> sortedFolders = new List<string>(possibleFolders.Length);`  
  
 `sortedFolders.AddRange(possibleFolders);`  
  
 `sortedFolders.Sort();`  
  
 `databaseLocation = sortedFolders[sortedFolders.Count - 1];`  
  
 `}`  
  
 `else`  
  
 `{`  
  
 `databaseLocation = possibleFolders[0];`  
  
 `}`  
  
 `}`  
  
 `db.Detach();`  
  
 `server.Attach(databaseLocation, dbReadWriteMode);`  
  
 `}`  
  
 `}`  
  
1.  在 C# 应用程序中，用必要的参数调用 `SwitchReadWrite()` 。  
  
2.  编译和执行您的代码以移动该数据库。  
  
#### <a name="to-switch-the-readwrite-mode-to-a-database-by-script-using-xmla"></a>使用 XMLA 借助于脚本切换数据库的读写模式  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的左窗格或右窗格中找到要切换的数据库。  
  
2.  右键单击该数据库并选择 **“属性”**。 查找数据库文件夹并记下其位置。 如果数据库存储位置为空，则表明数据库文件夹位于服务器数据文件夹中。  
  
    > [!IMPORTANT]  
    >  在将数据库分离之后， [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 就不能再帮助您获取数据库位置。  
  
3.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中打开一个新的 XMLA 选项卡。  
  
4.  复制下面的 XMLA 脚本模板：  
  
 `<Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  将 `%dbName%` 替换为数据库名称，将 `%password%` 替换为您的密码。 % 字符是模板的一部分，必须将其删除。  
  
2.  执行 XMLA 命令。  
  
3.  在新的 XMLA 选项卡中复制下面的 XMLA 脚本模板  
  
 `<Attach xmlns="http://schemas.microsoft.com/analysisservices/2003` `/engine` `">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  将 `%dbFolder%` 替换为数据库文件夹的完整 UNC 路径，将 `%ReadOnlyMode%` 替换为相应值（`ReadOnly` 或 `ReadWrite`），并将 `%password%` 替换为您的密码。 % 字符是模板的一部分，必须将其删除。  
  
2.  执行 XMLA 命令。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [附加和分离 Analysis Services 数据库](attach-and-detach-analysis-services-databases.md)   
 [数据库存储位置](database-storage-location.md)   
 [数据库 Readwritemode](database-readwritemodes.md)   
 [附加元素](../xmla/xml-elements-commands/attach-element.md)   
 [分离元素](../xmla/xml-elements-commands/detach-element.md)   
 [ReadWriteMode 元素](../xmla/xml-elements-properties/readwritemode-element.md)   
 [DbStorageLocation 元素](../xmla/xml-elements-properties/dbstoragelocation-element.md)  
  
  