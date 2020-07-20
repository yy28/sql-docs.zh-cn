---
title: 连接到 SQL Server 实用工具
description: 了解如何连接到 SQL Server 实用工具，以便可以管理 SQL Server 资源运行状况。 可以通过 SQL Server Management Studio (SSMS) 进行连接。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b9b90b8d-241f-4b74-ac14-de7b10ea1821
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fb961ccd1a1ec3013e186c7b45a54004ff400e07
ms.sourcegitcommit: e08d28530e0ee93c78a4eaaee8800fd687babfcc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/14/2020
ms.locfileid: "86301786"
---
# <a name="connect-to-a-sql-server-utility"></a>连接到 SQL Server 实用工具

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

必须先创建实用工具控制点 (UCP)，然后才能连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具。 有关详细信息，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  

若要查看和管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源运行状况，请使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具。  

通过 SSMS 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具：  

1. 启动 SSMS。

2. 在 SSMS 中，连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的某一实例。

3. 选择“视图”，然后选择“实用工具资源管理器” 。

4. 在“实用工具资源管理器”导航窗格中，选择 :::image type="icon" source="media/connect-to-utility.gif" border="false":::“连接到实用工具”。

5. 在“连接到服务器”对话框中，指定 UCP 实例名称，然后选择“连接” 。

6. 查看实用工具资源管理器导航窗格，以便查看 UCP 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源的树视图。

创建一个新的 UCP 也将您连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具。 有关详细信息，请参阅[创建 SQL Server 实用工具控制点（SQL Server 实用工具）](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)。

## <a name="see-also"></a>另请参阅

- [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)
- [查看资源运行状况策略结果（SQL Server 实用工具）](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)