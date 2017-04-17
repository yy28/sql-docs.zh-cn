---
title: "步骤 1：下载示例数据（数据库内高级分析教程）| Microsoft Docs"
ms.custom: 
ms.date: 04/19/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 32a5d5ad-c58a-4669-a90d-ef296b48fcd8
caps.latest.revision: 10
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d7490bf6191aad3b51195716f947ac87cf98599f
ms.lasthandoff: 04/11/2017

---
# <a name="step-1-download-the-sample-data-in-database-advanced-analytics-tutorial"></a>步骤 1：下载示例数据（数据库内高级分析教程）
在此步骤中，将下载示例数据集和演练中使用的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本文件。 数据和脚本文件都可在 Github 上共享，但 PowerShell 脚本会将数据和脚本文件下载到选择的本地目录。  
  
## <a name="download-the-data-and-scripts"></a>下载数据和脚本  
  
1.  打开 Windows PowerShell 命令控制台。  
  
    如果创建目标目录或将文件写入指定目标需要管理权限，请使用“以管理员身份运行”选项。  
  
2.  运行以下 PowerShell 命令，将参数 DestDir 的值更改为任何本地目录。  此处使用的默认值是“TempRSQL”。  
  
    ```  
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”  
    $wc = New-Object System.Net.WebClient  
    $wc.DownloadFile($source, $ps1_dest)  
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’  
  
    ```  
  
    如果 DestDir 中指定的文件夹不存在，则可以通过 PowerShell 脚本创建。  
  
    > [!TIP]  
    > 如果遇到错误，可以通过使用 Bypass 参数并将更改范围限制在当前会话，暂时将执行 PowerShell 脚本的策略设置为“不受限制”（仅用于本次演练）。  
    >   
    >````  
    > Set\-ExecutionPolicy Bypass \-Scope Process  
    >````   
    > 运行此命令不会导致配置更改。  
  
    根据 Internet 连接，下载可能需要一段时间。  
  
3.  所有文件下载完成之后，PowerShell 脚本将打开 DestDir 指定的文件夹。 在 PowerShell 命令提示符中，运行以下命令并查看已下载的文件。  
  
    ```  
    ls  
    ```  
  
    **结果：**  
  
    ![通过 PowerShell 脚本下载的文件列表](../../advanced-analytics/r-services/media/rsql-devtut-filelist.PNG "通过 PowerShell 脚本下载的文件列表")  
  
## <a name="next-step"></a>下一步  
[步骤 2：使用 PowerShell 将数据导入 SQL Server](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)  
  
## <a name="previous-step"></a>上一步  
[适用于 SQL 开发人员的数据库内高级分析（教程）](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
[SQL Server R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  


