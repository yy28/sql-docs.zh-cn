---
title: 第 1 课下载示例数据和脚本嵌入 R （SQL Server 机器学习） |Microsoft Docs
description: 本教程演示如何在 SQL Server 中嵌入 R 存储过程和 T-SQL 函数
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 74a60a95da4fb701f3862c36e35a4bada6ef933b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38030375"
---
# <a name="lesson-1-download-data-and-scripts"></a>第 1 课： 下载数据和脚本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是有关如何在 SQL Server 中使用 R 的 SQL 开发人员教程的一部分。

在此步骤中，你将下载示例数据集和[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本本教程中使用的文件。 在 GitHub 上共享数据和脚本文件，但 PowerShell 脚本将为你选择的本地目录下载的数据和脚本文件。

## <a name="download-tutorial-files-from-github"></a>从 Github 下载教程文件

1.  打开 Windows PowerShell 命令控制台。
  
    如果创建目标目录或将文件写入指定目标需要管理权限，请使用“以管理员身份运行”选项。
  
2.  运行以下 PowerShell 命令，将参数 DestDir 的值更改为任何本地目录。  此处使用的默认值是“TempRSQL”。
  
    ```ps
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
  
    ![通过 PowerShell 脚本下载的文件列表](media/rsql-devtut-filelist.png "通过 PowerShell 脚本下载的文件列表")
  
## <a name="next-lesson"></a>下一课

[第 2 课： 将数据导入 SQL Server 使用 PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)

## <a name="previous-lesson"></a>上一课

[SQL 开发人员的嵌入的 R 分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)
