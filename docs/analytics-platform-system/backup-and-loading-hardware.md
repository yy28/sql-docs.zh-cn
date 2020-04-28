---
title: 备份 & 加载硬件
description: 若要使用并行数据仓库（PDW）在分析平台系统（AP）上部署端到端数据仓库解决方案，需要创建备份数据仓库和加载数据的计划。 使用本指南来获取和配置可满足你的业务要求的备份和加载服务器。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4dd4fba91b1507f711a66a88f40b2fa2ea35e1ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401362"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>备份和加载硬件概述-并行数据仓库
若要使用并行数据仓库（PDW）在分析平台系统（AP）上部署端到端数据仓库解决方案，需要创建备份数据仓库和加载数据的计划。 使用本指南来获取和配置可满足你的业务要求的备份和加载服务器。  
  
## <a name="acquire-and-configure-backup-servers"></a>获取和配置备份服务器  
![备份过程](media/backup-process.png "备份过程")  
  
若要备份 PDW 数据库，需要一个或多个备份服务器。 你可以使用自己的现有硬件或购买新硬件。 有关详细信息，请参阅[获取和配置备份服务器](acquire-and-configure-backup-server.md)。 这些说明包括[备份服务器容量规划工作表](backup-capacity-planning-worksheet.md)，可帮助你规划正确的备份解决方案。  
  
## <a name="acquire-and-configure-loading-servers"></a>获取和配置加载服务器  
![正在加载进程](media/loading-process.png "加载进程")  
  
若要加载数据，需要一个或多个加载服务器。 你可以使用自己的现有 ETL 或其他服务器，也可以购买新服务器。 有关详细信息，请参阅[获取和配置加载服务器](acquire-and-configure-loading-server.md)。 这些说明包括[负载服务器容量规划工作表](loading-server-capacity-planning-worksheet.md)，可帮助你规划正确的加载解决方案。  
  
## <a name="see-also"></a>另请参阅  
[备份和还原概述](backup-and-restore-overview.md)  
[负载概述](load-overview.md)  
  
