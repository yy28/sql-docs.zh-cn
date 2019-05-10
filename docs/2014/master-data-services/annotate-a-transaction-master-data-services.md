---
title: 为事物添加批注 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- annotations [Master Data Services], for transactions
ms.assetid: f5a6b2ca-56de-4e42-9da8-fba0ac3e8d92
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 87e33ff166f07c10ee8b0b32eac5590f486e70c1
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483917"
---
# <a name="annotate-a-transaction-master-data-services"></a>为事务添加批注 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，为保留历史记录的目的而希望提供有关事务的支持详细信息时，可以为事务添加批注。  
  
> [!NOTE]  
>  您无法删除批注。  
  
## <a name="prerequisites"></a>先决条件  
  
-   若要为创建的事务添加批注，您必须有权访问 **“资源管理器”** 功能区域，并且必须至少对要添加批注的模型对象具有 **“更新”** 权限。  
  
-   若要为所有用户的事务添加批注，您必须有权访问 **“版本管理”** 功能区域并且必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
### <a name="to-annotate-a-transaction-in-explorer"></a>为资源管理器中为事务添加批注  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 在  主页上，从“模型”列表中，选择模型。  
  
2.   从“版本”列表中，选择某一版本。  
  
3.  单击 **“资源管理器”**。  
  
4.  从菜单栏中指向 **“实体”** ，然后单击包含具有要添加批注的事务的成员的实体。  
  
5.  在网格中，单击该成员所在的行。  
  
6.  单击 **“查看事务”**。  
  
7.  在 **“查看事务”** 对话框中，单击要添加批注的事务。  
  
8.  在该对话框的底部的框中，键入您的批注。  
  
9. 单击 **“添加批注”**。 该批注显示在 **“批注”** 窗格中。  
  
### <a name="to-annotate-a-transaction-in-version-management-administrators-only"></a>在版本管理中为事务添加批注（仅限管理员）  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 主页上，单击 **“版本管理”**。  
  
2.  在菜单栏上，单击 **“事务”**。  
  
3.  在 **“事务”** 窗格中，单击网格中您要添加批注的事务所对应的行。  
  
4.  在 **“事务批注”** 窗格的 **“批注”** 框中，键入您的批注。  
  
5.  单击“确定” 。  
  
## <a name="see-also"></a>请参阅  
 [批注 (Master Data Services)](../../2014/master-data-services/annotations-master-data-services.md)   
 [事务 (Master Data Services)](../../2014/master-data-services/transactions-master-data-services.md)  
  
  
