---
title: 订阅和检查 Finance Name 策略 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 126b4c4c-2a1c-4701-a0ad-8de23fbd7306
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3bbf6c9640882ffca2bbdbf82b2ef2667c394096
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090687"
---
# <a name="subscribe-to-and-check-the-finance-name-policy"></a>订阅和检查 Finance Name 策略
  在本任务中，将 Finance 数据库配置为订阅 Finance 策略类别。 然后，测试 Finance Name 策略。  
  
### <a name="to-subscribe-to-the-finance-policy-category"></a>订阅 Finance 策略类别  
  
1.  在对象资源管理器，展开**数据库**，右键单击`Finance`，依次指向**策略**，然后单击**类别**。  
  
2.  选择**已订阅**对应的复选框`Finance`类别。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-test-the-enforcement-of-the-finance-name-policy"></a>测试 Finance Name 策略的实施情况  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，打开一个查询窗口。 执行下面的语句，以尝试创建一个违反 **Finance Name** 策略的表。 该表违反了此策略，因为表名没有以字母 **fintbl**开头。  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
     请注意，此策略禁止创建该表，并返回一条提供策略名称的信息性消息。  
  
2.  若要提供有效的名称，请按如下方式修改代码并重新运行语句。  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
     此时，将创建该表。  
  
### <a name="to-apply-the-policy-to-the-whole-server"></a>将策略应用于整个服务器  
  
1.  当前，仅 Finance 数据库订阅了 Finance 策略类别。 在很多情况下，将策略类别应用于整个服务器会更容易一些。 在对象资源管理器中，展开“管理”，右键单击“策略管理”，然后单击“管理类别”。  
  
2.  在“管理策略类别”对话框中，找到 Finance 类别，然后选中 Finance 类别的“托管数据库订阅”复选框。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 现在，Finance 类别会应用于所有数据库，但创建的条件会将 Finance Name 策略限定为 Finance 数据库。 这说明了如何使用复杂的条件组合限定策略目标，以便按适当的方式在多个服务器上正确应用策略。  
  
## <a name="summary"></a>总结  
 本教程说明了如何创建基于策略的管理条件、策略和策略组，以及如何应用筛选器并检查基于策略的管理目标是否符合策略。  
  
## <a name="next"></a>Next  
 现已学完了本教程。 若要返回到开始位置，请单击[教程：使用基于策略的管理来管理服务器](tutorial-administering-servers-by-using-policy-based-management.md)。  
  
 有关教程的列表，请参阅[有关 SQL Server 2014 教程](../../tutorials/tutorials-for-sql-server-2014.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来管理服务器](administer-servers-by-using-policy-based-management.md)  
  
  
