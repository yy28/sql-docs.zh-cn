---
title: Azure 数据 Studio SQL Server 代理扩展 |Microsoft Docs
description: Azure Data Studio 的 SQL Server 代理扩展 （预览版）
ms.custom: tools|sos
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.prod_service: sql-tools
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 5804aa146ddf79f6c3c4ccba48edd86d297c5c72
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "48038080"
---
# <a name="sql-server-agent-extension-preview"></a>SQL Server 代理扩展 （预览版）

SQL Server 代理扩展 （预览版） 是用于管理和故障排除 SQL 代理作业和配置扩展。 此扩展当前处于预览状态。

密钥的操作包括：
- 列出 SQL Server 代理作业上的 SQL Server 配置
- 查看作业历史记录与作业执行结果
- 基本作业控件启动和停止作业

## <a name="install-the-sql-server-agent-extension"></a>安装 SQL Server 代理扩展

1. 若要開啟擴充管理員及存取可用的擴充功能，選取 [擴充功能] 圖示，或選取**檢視**功能表中的**擴充功能**。

2. 选择要查看其详细信息的可用扩展。

   ![安装代理](media/extensions/sql-server-agent-extension/install-sql-agent.png)

1. 选择所需的扩展并**安装**它。
2. 選取**重新載入**啟用該擴充功能 （只有第一次安裝擴充功能時需要）。
1. 透過滑鼠右鍵點選伺服器或資料庫並點選**管理**，瀏覽您的管理儀表板。
2. 已安裝的擴充功能會以索引標籤方式顯示在您的管理儀表板上：

   ![查看代理](media/extensions/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>查看作业

当您连接到 SQL Server 代理扩展时，您看到的第一件事是所有代理作业的列表。

   ![查看作业](media/extensions/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 代理的详细信息[检查我们的文档。](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent?view=sql-server-2017)


