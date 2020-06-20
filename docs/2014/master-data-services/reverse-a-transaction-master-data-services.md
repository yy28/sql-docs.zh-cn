---
title: 撤消事物 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], reversing
ms.assetid: 6f7c3f07-0f64-4283-8c9c-93facd00a046
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1bc306eda0d7c12bfbb6d7fc32e50189b213c30b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971097"
---
# <a name="reverse-a-transaction-master-data-services"></a>撤消事务 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，管理员可以在需要撤消操作时撤消事务。 事务的示例包括属性值更改、层次结构移动或成员删除。  
  
## <a name="prerequisites"></a>必备条件  
  
-   您必须有权访问 **“版本管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
### <a name="to-reverse-a-transaction"></a>撤消事务  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 主页上，单击 **“版本管理”**。  
  
2.  在菜单栏上，单击 **“事务”**。  
  
3.  在 **“事务”** 页上，从 **“模型”** 列表中选择某个模型。  
  
4.  **** 从“版本”列表中，选择某一版本。  
  
5.  单击网格中您要撤消的事务所对应的行。  
  
6.  单击 **“撤消事务”**。  
  
7.  在确认对话框中，单击 **“确定”**。 将向网格添加另一事务以记录撤消的事务。  
  
## <a name="see-also"></a>另请参阅  
 [Master Data Services 的事务 &#40;&#41;](../../2014/master-data-services/transactions-master-data-services.md)   
 [重新激活成员或集合 (Master Data Services)](../../2014/master-data-services/reactivate-a-member-or-collection-master-data-services.md)  
  
  
