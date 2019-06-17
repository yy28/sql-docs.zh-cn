---
title: SQL Server 导入扩展
titleSuffix: Azure Data Studio
description: 安装和使用适用于 Azure Data Studio SQL Server 导入扩展 （预览版）
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 5866e70945e7a507c0a8887abf006858d37c2bf0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798010"
---
# <a name="sql-server-import-extension-preview"></a>SQL Server 导入扩展 （预览版）

SQL Server 导入扩展 （预览版） 将 SQL 表转换为.txt 和.csv 文件。 此向导利用 Microsoft Research framework 称为[使用示例 （文本） 的程序合成](https://microsoft.github.io/prose/)智能地分析具有最少的用户输入的文件。 它是一个功能强大的框架，用于数据整理，并且支持快速填充在 Microsoft Excel 中的相同技术

若要了解有关此功能的 SSMS 版本的详细信息，可以读取[这篇文章](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard)。


## <a name="install-the-sql-server-import-extension"></a>安装 SQL Server 导入扩展

1. 若要開啟擴充管理員及存取可用的擴充功能，選取 [擴充功能] 圖示，或選取**檢視**功能表中的**擴充功能**。
2. 选择要查看其详细信息的可用扩展。

   ![导入扩展管理器](media/sql-server-import-extension/import-wizard-install.png)

1. 选择所需的扩展并**安装**它。
2. 選取**重新載入**啟用該擴充功能 （只有第一次安裝擴充功能時需要）。

## <a name="start-import-wizard"></a>启动导入向导

1. 若要启动 SQL Server 导入，首先在服务器选项卡中要进行连接到服务器。
2. 建立连接后，深化到你想要将文件导入 SQL 表的目标数据库。
3. 右键单击数据库，然后单击**导入向导**。
    ![打开导入向导](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>导入文件
1. 右键单击以启动向导，服务器和数据库都已自动填充。 如果有其他活动连接，您可以选择下拉列表中。 
    
    通过单击选择一个文件**浏览。** 它应自动填充的表名称基于文件名，但您还可以更改它自己。

    默认情况下，该架构将是 dbo，但可以更改它。 单击 **“下一步”** 继续。
    ![输入的文件](media/sql-server-import-extension/import-wizard-input-file.png)
1. 向导将生成预览基于前 50 行。 没有在此页上执行任何其他操作而非验证数据看起来准确。 单击 **“下一步”** 继续。
    ![打开导入向导](media/sql-server-import-extension/import-wizard-preview-data.png)
2. 在此页上，您可以更改为列名称，数据类型，它是主键，还是以允许 null。 可以任意更改。 单击**导入数据**以继续。
    ![打开导入向导](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. 此页提供了所选的操作的摘要。 此外可以查看您的表插入不论成功与否。 

    您可以单击**完成后上, 一步**如果你需要进行的更改，或**导入新文件**快速导入另一个文件。
    ![打开导入向导](media/sql-server-import-extension/import-wizard-summary.png)
1. 如果您的表已成功通过验证导入刷新您的目标数据库或表名称上运行 SELECT 查询。

## <a name="next-steps"></a>后续步骤
- 若要了解有关导入向导的详细信息，请阅读[博客文章](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/)。
- 若要了解有关 PROSE 的详细信息，请阅读[文档。](https://microsoft.github.io/prose/)
