---
title: 更改扩展事件会话 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0046e1f188bb415371ca37ce96bf67438e36cf7
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="alter-an-extended-events-session"></a>更改扩展事件会话
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  在创建扩展事件会话后，可以使用 **“SQL Server 扩展事件向导”**根据需要更改它。  
  
## <a name="before-you-begin"></a>开始之前  
 不能更改活动和不活动会话的目标，不能更改活动会话的高级属性配置。  
  
 可以对活动和不活动事件会话进行以下更改：  
  
-   在会话中添加或删除事件，更改事件配置（如事件字段、筛选器和操作）。  
  
-   添加或删除事件会话的目标。  
  
-   启用 **“在服务器启动时启动事件会话”** 选项。  
  
 可以对不活动的事件会话进行以下其他更改：  
  
-   启用 **“跟踪事件之间的关系”** 选项。  
  
-   更改高级属性配置。  
  
> [!NOTE]  
>  “SQL Server 扩展事件向导”不支持事件会话修改。  
  
## <a name="how-to-alter-an-extended-events-session-using-the-sql-server-extended-events-wizard"></a>如何使用 SQL Server 扩展事件向导更改扩展事件会话  
  
-   在对象资源管理器中，依次展开 **“管理”**、 **“扩展事件”**和 **“会话”**。  
  
-   右键单击要更改的会话，然后单击“属性”。  
  
-   在 **“属性”** 对话框中进行相应的更改，然后单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER EVENT SESSION (Transact-SQL)](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [使用查询编辑器创建扩展事件会话](http://msdn.microsoft.com/library/cba0e02b-b201-4863-bf1b-9164e68e5fa8)  
  
  
