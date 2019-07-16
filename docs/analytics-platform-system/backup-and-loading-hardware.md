---
title: 备份和加载硬件-并行数据仓库
description: 若要部署的端到端数据仓库解决方案 Analytics Platform System (APS) 上并行数据仓库 (PDW)，需要创建一个计划的备份数据仓库和加载数据。 使用本指南来获取和配置将满足您的业务需求的备份和加载服务器。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 90f142a8bb86f99ed5cf5d9ff926bdf849060324
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961419"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>备份和加载硬件概述-并行数据仓库
若要部署的端到端数据仓库解决方案 Analytics Platform System (APS) 上并行数据仓库 (PDW)，需要创建一个计划的备份数据仓库和加载数据。 使用本指南来获取和配置将满足您的业务需求的备份和加载服务器。  
  
## <a name="acquire-and-configure-backup-servers"></a>获取和配置备份服务器  
![备份过程](media/backup-process.png "备份过程")  
  
若要备份的 PDW 数据库，您需要一个或多个备份的服务器。 可以使用现有硬件，也可以购买新硬件。 有关详细信息，请参阅[获取和配置备份服务器](acquire-and-configure-backup-server.md)。 这些说明包括[备份服务器容量规划工作表](backup-capacity-planning-worksheet.md)来帮助你规划用于备份的正确解决方案。  
  
## <a name="acquire-and-configure-loading-servers"></a>获取和配置加载服务器  
![加载过程](media/loading-process.png "加载过程")  
  
若要加载数据，您需要一个或多个加载服务器。 可以使用自己现有的 ETL 或其他服务器，或可以购买新的服务器。 有关详细信息，请参阅[Acquire 和配置加载服务器](acquire-and-configure-loading-server.md)。 这些说明包括[加载服务器容量规划工作表](loading-server-capacity-planning-worksheet.md)来帮助你规划用于加载的正确解决方案。  
  
## <a name="see-also"></a>请参阅  
[备份和还原概述](backup-and-restore-overview.md)  
[加载概述](load-overview.md)  
  
