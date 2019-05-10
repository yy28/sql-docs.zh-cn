---
title: 撤消事物 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], reversing
ms.assetid: 6f7c3f07-0f64-4283-8c9c-93facd00a046
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d44c240962e27f04e44414866c12dcee07b6b50c
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65485947"
---
# <a name="reverse-a-transaction-master-data-services"></a>撤消事务 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，管理员可以在需要撤消操作时撤消事务。 事务的示例包括属性值更改、层次结构移动或成员删除。 本主题仅适用于事务日志类型为“属性”的实体的事务。 请转到实体资源管理器页，查看事务日志类型为“成员”的实体的事务历史记录。  
  
## <a name="prerequisites"></a>先决条件  
  
-   您必须有权访问 **“版本管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-reverse-a-transaction"></a>撤消事务  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 主页上，单击“版本管理” 。  
  
2.  在菜单栏上，单击 **“事务”**。  
  
3.  在 **“事务”** 页上，从 **“模型”** 列表中选择某个模型。  
  
4.   从“版本”列表中，选择某一版本。  
  
5.  单击网格中您要撤消的事务所对应的行。  
  
6.  单击 **“撤消事务”**。  
  
7.  在确认对话框中，单击 **“确定”**。 将向网格添加另一事务以记录撤消的事务。  
  
## <a name="see-also"></a>请参阅  
 [事务 (Master Data Services)](../master-data-services/transactions-master-data-services.md)   
 [重新激活成员或集合 (Master Data Services)](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)  
 [回退成员修订历史记录](../master-data-services/rollback-member-revision-history-master-data-services.md)
  
  
