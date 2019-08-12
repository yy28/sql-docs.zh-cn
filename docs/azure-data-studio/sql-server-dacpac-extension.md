---
title: SQL Server dacpac 扩展
titleSuffix: Azure Data Studio
description: 安装和使用 Azure Data Studio 的 SQL Server dacpac 扩展（预览版）
ms.custom: seodec18
ms.date: 03/18/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: e40e377310b33034b4abecdc5e58eab17d39695d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959197"
---
# <a name="sql-server-dacpac-extension-preview"></a>SQL Server dacpac 扩展（预览版）

“数据层应用程序向导”提供了一种易于使用的体验，可用于部署和提取 .dacpac 文件以及导入和导出 bacpac 文件  。

此体验目前处于初始预览阶段。 请在[此处](https://github.com/microsoft/azuredatastudio/issues)报告问题和提出功能请求。

![data-actions](media/sql-server-dacpac-extension/data-tier-application-actions.png)

 ### <a name="requirements"></a>要求
 * 此向导需要连接 SQL Server 实例才能启动。

 ### <a name="how-do-i-start-the-data-tier-application-wizard"></a>如何启动数据层应用程序向导？
 * 向导的主入口点是右键单击对象资源管理器中的数据库，然后单击“数据层应用程序向导”  。
 * 如果用户已连接 SQL Server 实例，还可以通过搜索“数据层应用程序向导”，从命令面板 (Ctrl + Shift + P) 启动向导。 

 ### <a name="why-would-i-use-the-data-tier-application-wizard"></a>为什么要使用数据层应用程序向导？
 创建此向导的目的是添加在 Azure Data Studio 中提取和部署 .dacpac 文件以及导入和导出 bacpac 文件的功能。

## <a name="install-the-sql-server-dacpac-extension"></a>安装 SQL Server dacpac 扩展

1. 若要打开扩展管理器并访问可用扩展，请选择扩展图标，或在“视图”菜单中选择“扩展”   。
2. 选择 SQL Server dacpac 扩展，并单击“安装”  。
1. 选择“重新加载”以启用扩展（仅在第一次安装扩展时是必需的）  。
2. 右键单击服务器或数据库，然后选择“管理”，导航到管理仪表板  。
3. 已安装的扩展显示为管理仪表板上的选项卡：

## <a name="next-steps"></a>后续步骤

若要了解有关 dacpac 的详细信息，[请查看我们的文档。](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)