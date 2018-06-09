---
title: 步骤 1 中下载示例数据 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 754140cbc1c2b35338794b6919076b99c3052562
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "35249730"
---
# <a name="step-1-download-the-sample-data"></a>步骤 1： 下载示例数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用本教程，本文摘自[SQL 开发人员的数据库中 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在 Github 上共享的数据和用于本教程的脚本。 在此步骤中，你可以使用 PowerShell 脚本以将数据和脚本文件下载到你选择的本地目录。

## <a name="run-the-script"></a>运行脚本

1. 打开 Windows PowerShell 命令控制台。

    使用选项，**以管理员身份运行**，如果创建目标目录，或将文件写入到指定的目标需要管理权限。

2. 运行以下 PowerShell 命令，将参数 DestDir 的值更改为任何本地目录。  我们已在此处使用的默认值是`C:\temp\pysql`。

    ```ps
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/PythonSQL/Download_Scripts_SQL_Walkthrough.ps1'
    $ps1_dest = "$pwd\Download_Scripts_SQL_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir 'C:\temp\pysql'
    ```
    
    如果 DestDir 中指定的文件夹不存在，则可以通过 PowerShell 脚本创建。
    
    如果遇到错误，暂时将设置到的 PowerShell 脚本执行的策略**不受限制**本演练中，通过使用**绕过**自变量和范围对当前会话的更改。 运行此命令不会导致配置更改。
    
    ```ps
    Set-ExecutionPolicy Bypass -Scope Process
    ```

3. 具体取决于你的 internet 连接，下载可能需要一些时间。 

## <a name="view-results"></a>查看结果

所有文件下载完成之后，PowerShell 脚本将打开 DestDir 指定的文件夹。 

+ 在 PowerShell 命令提示符，运行以下命令，以列出已下载的文件。

    ```ps
    ls
    ```

![通过 PowerShell 脚本下载的文件列表](media/sqldev-python-filelist.png "通过 PowerShell 脚本下载的文件列表")

## <a name="next-step"></a>下一步

[步骤 2：使用 PowerShell 将数据导入 SQL Server](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="previous-step"></a>上一步

[数据库中 Python 分析 SQL 开发人员](sqldev-in-database-python-for-sql-developers.md)

## <a name="see-also"></a>请参阅

[机器学习服务与 Python](../python/sql-server-python-services.md)


