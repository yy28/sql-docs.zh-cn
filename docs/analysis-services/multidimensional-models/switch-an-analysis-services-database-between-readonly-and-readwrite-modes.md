---
title: "在 ReadOnly 和 ReadWrite 模式之间切换 Analysis Services 数据库 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ReadOnly 属性"
  - "ReadWriteMode 命令"
  - "操作 [Analysis Services - 多维数据]"
ms.assetid: 4eff8181-08dd-4fad-b091-d400fc21a020
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 16
---
# 在 ReadOnly 和 ReadWrite 模式之间切换 Analysis Services 数据库
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库管理员可以在多个仅限查询的服务器之间分配查询工作负载这种大型任务中，更改表格或多维数据库的读/写模式。  
  
 可以通过多种方式来切换数据库模式。 本文档介绍下列常见方案：  
  
-   使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   使用 AMO 以编程方式  
  
-   使用 XMLA 或 TMSL 的脚本  
  
## 使用 Management Studio 以交互方式切换数据库的读/写模式  
  
1.  在对象资源管理器中，右键单击数据库并选择“属性”。  
  
     记下其位置。 如果数据库存储位置为空，则表明数据库文件夹位于服务器数据文件夹中。  
  
2.  右键单击该数据库并选择“分离…”  
  
3.  为要分离的数据库分配一个密码，然后单击 **“确定”** 执行分离命令。  
  
4.  在对象资源管理器中，右键单击“数据库”文件夹，然后选择“附加…”。  
  
5.  在 **“文件夹”** 文本框中，键入数据库文件夹的原始位置。 也可以使用浏览按钮 (**…**) 查找数据库文件夹。  
  
6.  针对该数据库选择读写模式。  
  
7.  键入密码，然后单击  “确定”执行附加命令。  
  
## 使用 AMO 以编程方式切换数据库的读写模式  
 在 C# 应用程序中，用必要的参数调用 `SwitchReadWrite()`。 编译和执行您的代码以移动该数据库。  
  
```  
private void SwitchReadWrite(Server server, string dbName, ReadWriteMode dbReadWriteMode)  
{  
    if (server.Databases.ContainsName(dbName))  
    {  
        Database db;  
        string databaseLocation;  
        db = server.Databases[dbName];  
        databaseLocation = db.DbStorageLocation;  
  
              if (databaseLocation == null)  
            {  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
  
    String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);  
  
   if (possibleFolders.Length > 1)  
         {  
         List<String> sortedFolders = new List<string>(possibleFolders.Length);  
         sortedFolders.AddRange(possibleFolders);  
         sortedFolders.Sort();  
         databaseLocation = sortedFolders[sortedFolders.Count - 1];  
         }  
         else  
         {  
         databaseLocation = possibleFolders[0];  
          }  
        }  
    db.Detach();  
    server.Attach(databaseLocation, dbReadWriteMode);  
    }  
}  
  
```  
  
## 使用 XMLA 借助于脚本切换数据库的读/写模式  
 以下说明适用于兼容模式 1050、1100 或 1103 下的多维数据库和表格数据库。  
  
1.  在对象资源管理器中，右键单击数据库并选择“属性”。  
  
     记下其位置。 如果数据库存储位置为空，则表明数据库文件夹位于服务器数据文件夹中。  
  
2.  右键单击该数据库并选择“分离…”  
  
3.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中打开一个新的 XMLA 选项卡。  
  
4.  复制下面的 XMLA 脚本模板：  
  
    ```  
    <Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Object>  
          <DatabaseID>%dbName%</DatabaseID>  
          <Password>%password%</Password>  
       </Object>  
    </Detach>  
    ```  
  
5.  将 `%dbName%` 替换为数据库名称，将 `%password%` 替换为您的密码。 % 字符是模板的一部分，必须将其删除。  
  
6.  执行 XMLA 命令。  
  
7.  在新的 XMLA 选项卡中复制下面的 XMLA 脚本模板  
  
    ```  
    <Attach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Folder>%dbFolder%</Folder>  
       <ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>  
    </Attach>  
    ```  
  
8.  将 `%dbFolder%` 替换为数据库文件夹的完整 UNC 路径，将 `%ReadOnlyMode%` 替换为相应值（**ReadOnly** 或 **ReadWrite**），并将 `%password%` 替换为你的密码。 % 字符是模板的一部分，必须将其删除。  
  
9. 执行 XMLA 命令。  
  
## 另请参阅  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Analysis Services 中的高可用性和可伸缩性](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)   
 [附加和分离 Analysis Services 数据库](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [数据库存储位置](../../analysis-services/multidimensional-models/database-storage-location.md)   
 [数据库 ReadWriteMode](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [附加元素](../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [分离元素](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [ReadWriteMode 元素](../../analysis-services/xmla/xml-elements-properties/readwritemode-element.md)   
 [DbStorageLocation 元素](../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)  
  
  