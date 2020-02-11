---
title: 编辑操作员 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- modifying operators
- jobs [SQL Server Agent], operators
- operators (users) [Database Engine], modifying with Management Studio
ms.assetid: b2ba2168-ca0b-4b59-9007-4e1e4c30679e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9ee3228eea9970563540be9bc6a4c3b9a3677112
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68189330"
---
# <a name="edit-an-operator"></a>编辑运算符
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中对操作员能否接收通知进行编辑，并编辑他们的电子邮件地址、寻呼地址和 net send 地址。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要编辑操作员，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   在未来版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，将从代理中删除寻呼程序和**net send**选项。 请避免在新的开发工作中使用这些功能，并考虑修改当前使用这些功能的应用程序。  
  
-   请注意，若要向操作员发送电子邮件和寻呼通知，必须将 SQL Server 代理配置为使用数据库邮件。 有关详细信息，请参阅 [向操作员分配警报](assign-alerts-to-an-operator.md)。  
  
-   
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 为管理作业提供了一种图形化的简便方法，建议使用此方法来创建和管理作业基础结构。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 只有 **sysadmin** 固定服务器角色的成员才能编辑操作员。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-edit-an-operator"></a>编辑操作员  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开包含要编辑的操作员的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以展开 **“操作员”** 文件夹。  
  
4.  右键单击要编辑的操作员，然后选择“属性”****。  
  
     有关 " _operator_name_**属性**" 对话框中包含的可用选项的详细信息，请参阅：  
  
    -   [操作员属性和新操作员 &#40;常规 "页面&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
    -   [操作员属性：新建操作员 &#40;通知页面&#41;](operator-properties-new-operator-notifications-page.md)  
  
    -   ["操作员属性" &#40;"历史记录" 页&#41;](operator-properties-history-page.md)  
  
5.  完成后，单击 **“确定”** 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-edit-an-operator"></a>编辑操作员  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    -- updates the operator status to enabled, and sets the days   
    -- (from Monday through Friday, from 8 A.M. through 5 P.M.) when the operator can be paged.   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_operator   
        @name = N'Fran??ois Ajenstat',  
        @enabled = 1,  
        @email_address = N'fran??oisa',  
        @pager_address = N'5551290AW@pager.Adventure-Works.com',  
        @weekday_pager_start_time = 080000,  
        @weekday_pager_end_time = 170000,  
        @pager_days = 64 ;  
    GO  
    ```  
  
 有关详细信息，请参阅[&#40;transact-sql&#41;sp_update_operator ](/sql/relational-databases/system-stored-procedures/sp-update-operator-transact-sql)。  
  
  
