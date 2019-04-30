---
title: SQL Server dacpac 扩展
titleSuffix: Azure Data Studio
description: 安装和使用适用于 Azure Data Studio SQL Server dacpac 扩展 （预览版）
ms.custom: seodec18
ms.date: 03/18/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 383a7b2bbd6e8ebaab5f1e66b10a10c9584800ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309228"
---
# <a name="sql-server-dacpac-extension-preview"></a>SQL Server dacpac 扩展（预览版）

**数据层应用程序向导**提供了一种易于使用的体验来部署和提取.dacpac 文件并导入和导出.bacpac 文件。

这种体验目前处于其初始预览状态。 请报告问题和功能请求[此处。](https://github.com/microsoft/azuredatastudio/issues)

![data-actions](media/sql-server-dacpac-extension/data-tier-application-actions.png)

 ### <a name="requirements"></a>要求
 * 此向导需要与 SQL Server 实例启动的活动连接。

 ### <a name="how-do-i-start-the-data-tier-application-wizard"></a>如何启动数据层应用程序向导？
 * 在向导的主入口点是右键单击对象资源管理器中的数据库，然后单击**数据层应用程序向导**。
 * 如果用户连接到 SQL Server 实例，用户可以启动向导从命令面板 (Ctrl + Shift + P) 通过搜索**数据层应用程序向导。**

 ### <a name="why-would-i-use-the-data-tier-application-wizard"></a>为什么要使用的数据层应用程序向导？
 创建此向导以添加提取和部署.dacpac 文件并导入和导出.bacpac 文件在 Azure Data Studio 的功能。

## <a name="install-the-sql-server-dacpac-extension"></a>安装 SQL Server dacpac 扩展

1. 若要開啟擴充管理員及存取可用的擴充功能，選取 [擴充功能] 圖示，或選取**檢視**功能表中的**擴充功能**。

2. 选择 SQL Server dacpac 扩展，然后单击**安装**。
1. 選取**重新載入**啟用該擴充功能 （只有第一次安裝擴充功能時需要）。
2. 透過滑鼠右鍵點選伺服器或資料庫並點選**管理**，瀏覽您的管理儀表板。
3. 已安裝的擴充功能會以索引標籤方式顯示在您的管理儀表板上：

## <a name="next-steps"></a>后续步骤

若要详细了解 dacpac，[检查我们的文档。](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)