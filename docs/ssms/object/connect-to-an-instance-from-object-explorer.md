---
title: "连接到 SQL Server 或 Azure SQL 数据库 | Microsoft Docs"
ms.custom: 
ms.date: 08/25/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 2d5048825b3c71ecaec5da0f6ae75277994d1697
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-a-sql-server-or-azure-sql-database"></a>连接到 SQL Server 或 Azure SQL 数据库

要使用服务器和数据库，需首先连接到服务器。 可以同时连接到多个服务器。

[SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) 支持多种类型的连接。 本文详细介绍如何接到 SQL Server 和 Azure SQL 数据库（连接到 Azure SQL 逻辑服务器）。 有关其他连接选项的相关信息，请参阅此页面底部的[链接](#see-also)。
  
## <a name="connecting-to-a-server"></a>连接到服务器  

1. 在“对象资源管理器”中，单击“连接”>“数据库引擎...”。

   ![connect](../media/connect-to-server/connect-db-engine.png)

1. 填写“连接到服务器”窗体，并单击“连接”：

   ![连接到服务器](../media/connect-to-server/connect.png)

1. 如果正在连接 Azure SQL Server，系统可能提示登录创建防火墙规则。 单击“登录...”（如果不执行此操作，请跳到下方步骤 6）

   ![防火墙](../media/connect-to-server/firewall-rule-sign-in.png)

1. 成功登录后，窗体中预填充有你的特定 IP 地址。 如果 IP 地址更改频繁，将访问权限设定在一个范围内可能更简单，因此，请选择最适合环境的选项。 

   ![防火墙](../media/connect-to-server/new-firewall-rule.png)

1. 要创建防火墙规则并连接到服务器，请单击“确定”。

1. 成功连接后，服务器将出现在“对象资源管理器”中：

   ![已连接](../media/connect-to-server/connected.png)

## <a name="next-steps"></a>后续步骤

[设计、创建和更新表](../visual-db-tools/design-tables-visual-database-tools.md)

## <a name="see-also"></a>另请参阅

[SQL Server Management Studio (SSMS)](../sql-server-management-studio-ssms.md)  
[下载 SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)  
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)  
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)  
[Azure 存储](../f1-help/connect-to-microsoft-azure-storage.md)  

