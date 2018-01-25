---
title: "创建 Off By Default 策略 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 98fde3c5-297c-4d95-981e-95700bbf5ccd
caps.latest.revision: "28"
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a56e8861cd256421962ef1728caabc325c0940bf
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="lesson-1-1---create-the-off-by-default-policy"></a>第 1-1 课 - 创建 Off By Default 策略
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]此任务创建一个基于外围应用配置器方面的名为“Mail Off”的条件。 然后，创建一个名为 Off By Default 的条件。  
  
### <a name="to-create-the-mail-off-condition"></a>创建 Mail Off 条件  
  
1.  在对象资源管理器中，依次展开“管理”、“策略管理”和“方面”，右键单击“外围应用配置器”，然后单击“新建条件”。  
  
2.  在“创建新条件”对话框的“名称”框中，输入 **Mail Off**。  
  
3.  在“方面”框中，确认选择了“外围应用配置器”方面。  
  
4.  在“表达式”区域中，在“字段”框中选择 **@DatabaseMailEnabled**，在“运算符”框中选择 **=**，然后在“值”中选择“False”。  
  
5.  在“说明”页上输入条件说明，然后单击“确定”以创建条件。  
  
### <a name="to-create-the-off-by-default-policy"></a>创建 Off By Default 策略  
  
1.  在对象资源管理器中，右键单击“外围应用配置器”，然后单击“新建策略”。  
  
2.  在“创建新策略”对话框的“名称”框中，输入 **Off By Default**。  
  
3.  取消选中“已启用”复选框。 “已启用”复选框适用于自动策略，而此策略是按需执行的。  
  
4.  在“检查条件”复选框中，向下滚动到“外围应用配置器”区域，然后选择“Mail Off”作为要检查的条件。  
  
5.  “针对目标”框为空，因为这是一个服务器范围内的策略。  
  
6.  在“评估模式”复选框中，选择“按需”作为评估模式。  
  
7.  在“服务器限制”复选框中，选择“无”。  
  
8.  在“说明”页上，输入策略的说明。  
  
9. 可以在“更多帮助超链接”区域中提供策略网页的超链接。 请在“要显示的文本”框中，输入为超链接显示的文本。  
  
10. 在“地址”框中输入“帮助”页的超链接，例如，公司 IT 部门的主页。  
  
11. 若要通过打开网页来确认地址是否正确，请单击“测试链接”。  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[将服务器配置为运行 Off By Default 策略](../../relational-databases/policy-based-management/lesson-1-2-configure-a-server-to-run-the-off-by-default-policy.md)  
  
  
  
