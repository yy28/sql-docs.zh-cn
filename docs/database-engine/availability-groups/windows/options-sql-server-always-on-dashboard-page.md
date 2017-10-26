---
title: "选项（SQL Server AlwaysOn、“仪表板”页）| Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Alwayson.Dashboard
ms.assetid: 4369b588-e982-4b57-80a1-beb2e879ce0b
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6edac25ccc503679e45bdc3477a819e0285e2909
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="options-sql-server-always-on-dashboard-page"></a>选项（SQL Server AlwaysOn、“面板”页）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 的“选项”对话框的“SQL Server AlwaysOn 面板”页配置 AlwaysOn 面板。  
  
 **若要访问此页，请执行以下操作：**  
  
 在“工具”菜单上，单击“选项”，展开 **SQL Server AlwaysOn** 文件夹，然后单击“面板”。  
  
## <a name="on-this-page"></a>在此页上  
 **启用自动刷新。**  
 单击此选项可以启用自动刷新。 相应的选项包括：  
  
-   “刷新时间间隔（秒）”字段显示仪表板刷新的秒数。 默认值为 30。 启用自动刷新时，您可以编辑此字段以更改刷新间隔。  
  
-   **“连接重试次数”** 显示面板尝试连接到承载着面板所监视的可用性组的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的次数。 默认值为 65535。 启用自动刷新时，您可以编辑此字段以更改连接重试次数。  
  
 **启用用户定义的 AlwaysOn 策略。**  
 如果你已定义了自己的 AlwaysOn 策略，单击此选项即可启用你的策略。  
  
## <a name="see-also"></a>另请参阅  
 [使用 AlwaysOn 面板 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  

