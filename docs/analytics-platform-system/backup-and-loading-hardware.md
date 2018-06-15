---
title: 备份和加载硬件-并行数据仓库
description: 若要部署端到端数据仓库解决方案分析平台系统 (AP) 上并行数据仓库 (PDW)，你需要创建备份数据仓库和加载数据的计划。 使用本指南来获取和配置将根据业务需求的备份和加载服务器。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4d7f7b6b4edea9dacab7287a7936b7fd87fd7973
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544729"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>备份和加载硬件概述-并行数据仓库
若要部署端到端数据仓库解决方案分析平台系统 (AP) 上并行数据仓库 (PDW)，你需要创建备份数据仓库和加载数据的计划。 使用本指南来获取和配置将根据业务需求的备份和加载服务器。  
  
## <a name="acquire-and-configure-backup-servers"></a>获取和配置备份服务器  
![备份过程](media/backup-process.png "备份过程")  
  
若要备份 PDW 数据库，你需要一个或多个备份服务器。 你可以使用现有硬件或购买新硬件。 有关详细信息，请参阅[获取和配置备份服务器](acquire-and-configure-backup-server.md)。 这些说明包括[备份服务器容量规划工作表](backup-capacity-planning-worksheet.md)来帮助你规划备份的理想解决方案。  
  
## <a name="acquire-and-configure-loading-servers"></a>获取和配置加载服务器  
![加载过程](media/loading-process.png "加载过程")  
  
若要加载数据，你需要一个或多个加载服务器。 你可以使用你自己现有 ETL 或其他服务器，或者，你可以购买新的服务器。 有关详细信息，请参阅[获取和配置加载服务器](acquire-and-configure-loading-server.md)。 这些说明包括[加载服务器容量规划工作表](loading-server-capacity-planning-worksheet.md)来帮助你规划加载的理想解决方案。  
  
## <a name="see-also"></a>另请参阅  
[备份和还原概述](backup-and-restore-overview.md)  
[负载概述](load-overview.md)  
  
