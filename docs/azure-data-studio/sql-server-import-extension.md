---
title: SQL Server 导入扩展
titleSuffix: Azure Data Studio
description: 安装和使用 Azure Data Studio 的 SQL Server 导入扩展（预览版）
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 012c2c880e81c095e90086cf26ebffd6117d534e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "67959125"
---
# <a name="sql-server-import-extension-preview"></a>SQL Server 导入扩展（预览版）

SQL Server 导入扩展（预览版）将 .txt 和 .csv 文件转换为 SQL 表。 此向导使用名为 [Program Synthesis using Examples (PROSE)](https://microsoft.github.io/prose/) 的 Microsoft 研究框架，以使用最少的用户输入来智能分析文件。 它是功能强大的数据整理框架，也是在 Microsoft Excel 中为“快速填充”提供支持的技术

若要了解有关此功能的 SSMS 版本的详细信息，请阅读[本文](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard)。


## <a name="install-the-sql-server-import-extension"></a>安装 SQL Server 导入扩展

1. 若要打开扩展管理器并访问可用扩展，请选择扩展图标，或在“视图”菜单中选择“扩展”   。
2. 选择某个可用扩展以查看其详细信息。

   ![导入扩展管理器](media/sql-server-import-extension/import-wizard-install.png)

1. 选择所需的扩展并“安装”它  。
2. 选择“重新加载”以启用扩展（仅在第一次安装扩展时是必需的）  。

## <a name="start-import-wizard"></a>启动导入向导

1. 若要启动 SQL Server 导入，请先在“服务器”选项卡中建立与服务器的连接。
2. 建立连接后，向下钻取到想要将文件导入 SQL 表的目标数据库。
3. 右键单击数据库，然后单击“导入向导”  。
    ![打开导入向导](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>导入文件
1. 右键单击以启动向导时，服务器和数据库已自动填充。 如果存在其他活动连接，则可以在下拉列表中进行选择。 
    
    单击“浏览”选择文件  。 它应该根据文件名自动填充表名，但也可以自行更改。

    默认情况下，架构将是 dbo，但可进行更改。 单击“下一步”继续。 
    ![输入文件](media/sql-server-import-extension/import-wizard-input-file.png)
1. 向导将根据前 50 行生成预览。 除验证数据是否准确外，此页上没有其他操作。 单击“下一步”继续。 
    ![打开导入向导](media/sql-server-import-extension/import-wizard-preview-data.png)
2. 在此页上，可以更改列名、数据类型、是否为主键或是否允许 null 值。 可以根据需要执行任意数量的更改。 单击“导入数据”继续操作  。
    ![打开导入向导](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. 此页提供所选操作的摘要。 还可以查看表是否成功插入。 

    如果需要进行更改，可单击“完成，上一步”，或者单击“导入新文件”以快速导入另一个文件   。
    ![打开导入向导](media/sql-server-import-extension/import-wizard-summary.png)
1. 通过刷新目标数据库或对表名运行 SELECT 查询来验证表是否已成功导入。

## <a name="next-steps"></a>后续步骤
- 若要了解有关导入向导的详细信息，请阅读[博客文章](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/)。
- 若要了解有关 PROSE 的详细信息，请阅读[文档](https://microsoft.github.io/prose/)。
