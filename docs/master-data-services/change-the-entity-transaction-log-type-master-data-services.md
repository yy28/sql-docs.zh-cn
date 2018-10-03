---
title: 更改实体事务日志类型 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: 75250b32-3384-43c2-9b5c-1607cc3aa7b3
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: aa1298d938d4845be7e13688baf9a01d88812e66
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765615"
---
# <a name="change-the-entity-transaction-log-type-master-data-services"></a>更改实体事务日志类型 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  可以将实体的事务日志类型更改为属性、成员或无。  
  
|事务日志类型|描述|  
|--------------------------|-----------------|  
|Attribute|在属性级别保存实体更改日志。<br /><br /> 保存事务日志，与 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中的行为一致。|  
|成员|在行级别保存实体更改日志。<br /><br /> 任何属性更改都将触发新的行修订。<br /><br /> 当使用行事务日志类型时，实体存储为缓慢更改维度类型 4。 支持类型 2 订阅视图和类型 4（历史记录）订阅视图。 有关详细信息，请参阅[订阅视图格式 (Master Data Services)](../master-data-services/subscription-view-formats-master-data-services.md)<br /><br /> 提供较好的性能。|  
|None|不保存任何更改日志。<br /><br /> 提供最好的性能。|  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   必须有权访问“系统管理”功能区域。有关详细信息，请参阅[功能区域权限 (Master Data Services)](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
-   实体必须存在。 有关详细信息，请参阅[创建实体 (Master Data Services)](../master-data-services/create-an-entity-master-data-services.md)。  
  
 **更改事务日志类型**  
  
1.  在主数据管理器中，单击“系统管理” 。  
  
2.  在“管理模型”  页上，选择要编辑的实体模型行，然后单击“实体” 。  
  
3.  在“管理实体”  页上，选择要更新的实体行，然后单击“编辑” 。  
  
4.  在下拉列表中选择事务日志类型。  
  
5.  单击 **“保存”**。  
  
  
