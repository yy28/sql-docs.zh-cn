---
title: "步骤 1： 下载示例数据 |Microsoft 文档"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 147860e9af8cce86d1a7ccbd3e53f20d240fcd49
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="step-1-download-the-sample-data"></a>步骤 1：下载示例数据

在此步骤中，你将下载示例数据集和脚本。 数据和脚本文件都可在 Github 上共享，但 PowerShell 脚本会将数据和脚本文件下载到选择的本地目录。

## <a name="download-the-data-and-scripts"></a>下载数据和脚本

1. 打开 Windows PowerShell 命令控制台。

    使用选项，**以管理员身份运行**，如果创建目标目录，或将文件写入到指定的目标需要管理权限。

2. 运行以下 PowerShell 命令，将参数 DestDir 的值更改为任何本地目录。  我们已在此处使用的默认值是**TempPythonSQL**。

    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/PythonSQL/Download_Scripts_SQL_Walkthrough.ps1'
    $ps1_dest = "$pwd\Download_Scripts_SQL_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir 'C:\tempPythonSQL'
    ```
    
    如果 DestDir 中指定的文件夹不存在，则可以通过 PowerShell 脚本创建。
    
    如果遇到错误，可以暂时将设置到的 PowerShell 脚本执行的策略**不受限制**仅对于本演练，使用**绕过**自变量和范围对当前的更改会话。 运行此命令不会导致配置更改。
    
    `Set\-ExecutionPolicy Bypass \-Scope Process`

3. 根据 Internet 连接，下载可能需要一段时间。 所有文件下载完成之后，PowerShell 脚本将打开 DestDir 指定的文件夹。 在 PowerShell 命令提示符中，运行以下命令并查看已下载的文件。

    ```
    ls
    ```
**结果：**

![通过 PowerShell 脚本下载的文件列表](media/sqldev-python-filelist.png "通过 PowerShell 脚本下载的文件列表")

## <a name="next-step"></a>下一步

[步骤 2：使用 PowerShell 将数据导入 SQL Server](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="previous-step"></a>上一步

[数据库中 Python 分析 SQL 开发人员](sqldev-in-database-python-for-sql-developers.md)

## <a name="see-also"></a>另请参阅

[机器学习服务与 Python](../python/sql-server-python-services.md)



