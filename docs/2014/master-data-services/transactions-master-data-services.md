---
title: 事务 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], about transactions
- transactions [Master Data Services]
ms.assetid: 4cd2fa6f-9c76-4b7a-ae18-d4e5fd2f03f5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8eebb47569a4ccc96437a3e16379c794b83642dd
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65478514"
---
# <a name="transactions-master-data-services"></a>事务 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，每次对成员执行操作时，都记录一个事务。 事务可供所有用户查看并由管理员撤销。 事务显示执行操作的日期、时间和用户以及其他详细信息。 用户可以为事务添加批注，以指示事务发生的时间。  
  
## <a name="when-transaction-are-recorded"></a>何时记录事务  
 当成员处于以下状态时将对事务进行记录：  
  
-   已创建、已删除或重新激活。  
  
-   已更改属性值。  
  
-   在层次结构中移动了位置。  
  
 当业务规则更改属性值时，不记录事务。  
  
## <a name="view-and-manage-transactions"></a>查看和管理事务  
 在“资源管理器”功能区域中，可以查看自行创建的事务并为其添加批注（注释）。  
  
 在 **“版本管理”** 功能区域中，管理员可以查看其有权访问的模型的所有用户的所有事务，并撤消这些事务中的任意事务。  
  
> [!NOTE]  
>  管理员可以查看所有用户的所有事务，除非他们在“版本权限”功能区域应用了只读权限级别。 例如，如果为管理员设置了只读权限和更新权限级别，管理员将无法查看其他用户事务，因为只读权限将优先于更新权限。

## <a name="system-settings"></a>系统设置  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中有一个设置影响在暂存记录时是否记录事务。 该设置只影响 SQL Server 2008 R2。 可以在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中或直接在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库的“系统设置”表中调整此设置。 有关详细信息，请参阅[系统设置 (Master Data Services)](system-settings-master-data-services.md)。  
  
 在将数据导入此版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中时，您可以指定是否在启动存储过程时记录事务。 有关详细信息，请参阅[临时存储过程 (Master Data Services)](../../2014/master-data-services/staging-stored-procedure-master-data-services.md)。  
  
## <a name="concurrency"></a>并发  
 如果某个实体值在多个资源管理器会话中同时显示，则可能对同一个值进行并发编辑。 MDS 不会自动检测并发编辑。 当多个用户从多个会话（例如从多个计算机、多个浏览器选项卡或窗口，或多个用户帐户）使用 Web 浏览器中的 MDS 资源管理器时，就会出现这种情况。  
  
 多个用户可以更新相同的实体值而不会出错（即便启用了事务记录也不影响）。 一段时间内针对该值的最后一次编辑通常优先级最高。 可以在事务历史记录中手工检测到重复编辑冲突，并可由管理员手动解决。 事务历史记录将为每个会话的相关属性的 **“旧值”** 和 **“新值”** 显示各个事务，但不会在同一个旧值存在多个 **“新值”** 时自动解决冲突。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|通过撤消事务来撤消操作（仅限管理员）。|[撤消事务 (Master Data Services)](../../2014/master-data-services/reverse-a-transaction-master-data-services.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [管理员 (Master Data Services)](../../2014/master-data-services/administrators-master-data-services.md)  
  
-   [批注 (Master Data Services)](../../2014/master-data-services/annotations-master-data-services.md)  
  
  
