---
title: 备份和加载 AP PDW 硬件概述
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: 若要部署端到端数据仓库解决方案分析平台系统 (AP) 与 SQL Server 并行数据仓库 (PDW)，你需要创建备份数据仓库和加载数据的计划。
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 3a2ae046-f8d8-4a5c-b3c1-6ecee005df6c
caps.latest.revision: 9
ms.openlocfilehash: 8979b0d7b14f3e6b3de2834fdc800c5281d057ad
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="backup-and-loading-hardware-overview"></a>备份和加载硬件概述
若要部署端到端数据仓库解决方案分析平台系统 (AP) 与 SQL Server 并行数据仓库 (PDW)，你需要创建备份数据仓库和加载数据的计划。 使用本指南来获取和配置将根据业务需求的备份和加载服务器。  
  
## <a name="acquire-and-configure-backup-servers"></a>获取和配置备份服务器  
![备份过程](media/backup-process.png "备份过程")  
  
若要备份 PDW 数据库，你需要一个或多个备份服务器。 你可以使用现有硬件或购买新硬件。 有关详细信息，请参阅[获取和配置备份服务器](acquire-and-configure-backup-server.md)。 这些说明包括[备份服务器容量规划工作表](backup-capacity-planning-worksheet.md)来帮助你规划备份的理想解决方案。  
  
## <a name="acquire-and-configure-loading-servers"></a>获取和配置加载服务器  
![加载过程](media/loading-process.png "加载过程")  
  
若要加载数据，你需要一个或多个加载服务器。 你可以使用你自己现有 ETL 或其他服务器，或者，你可以购买新的服务器。 有关详细信息，请参阅[获取和配置加载服务器](acquire-and-configure-loading-server.md)。 这些说明包括[加载服务器容量规划工作表](loading-server-capacity-planning-worksheet.md)来帮助你规划加载的理想解决方案。  
  
## <a name="see-also"></a>另请参阅  
[备份和还原概述](backup-and-restore-overview.md)  
[负载概述](load-overview.md)  
  
