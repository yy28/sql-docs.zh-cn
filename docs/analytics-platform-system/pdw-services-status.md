---
title: "PDW 服务状态 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fc9bee2-c372-4c4a-956c-fb54215d8918
caps.latest.revision: "14"
ms.openlocfilehash: 7a6b1a1f9a6ef922833930abf00ca10482648141
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="pdw-services-status"></a>PDW 服务状态
并行数据仓库**服务状态**页 Microsoft 分析平台系统 Configuration Manager 中显示的当前状态的所有 SQL Server PDW 服务，并提供的功能来停止和启动 PDW 服务。 这是唯一受支持的方法启动和停止 PDW 服务。 请注意，单个组件或服务无法启动独立。  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>若要启动或停止设备服务  
  
1.  若要启动设备服务，请单击**启动设备**。  
  
2.  若要停止设备服务，请单击**停止设备**。  
  
没有必要单击**应用**时启动和停止使用设备服务**启动设备**和**停止设备**。  
  
![DWConfig 设备 PDW 服务](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> 停止 PDW 区域还将 PDW 代理 (sqldwagent) 停止节点上的 HDInsight 区域中。 HDInsight 区域是仍正常工作，但是运行状况监视将不可用。 （PDW 代理需要 PDW 控制节点，以报告运行状况监视。）  
  
## <a name="see-also"></a>另请参阅  
[电源 AP 设备打开或关闭 &#40;分析平台系统 &#41;](power-the-aps-appliance-on-or-off.md)  
  
