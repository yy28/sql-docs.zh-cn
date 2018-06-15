---
title: 向主体授予权限 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Grant permission to a principal
ms.assetid: 4107389d-05b6-4aa3-9fa8-95b40cdf05dc
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e7d8c1990cb43aa5398a179bb00c053afe98f651
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32966542"
---
# <a name="grant-a-permission-to-a-principal"></a>向主体授予权限
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中对主体授予权限。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要向主体授予权限，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 请考虑以下可以使管理权限更简单的最佳做法。  
  
-   将权限授予角色，而不是单独的登录名或用户。 当某个用户由其他人取代时，可从角色中删除离开的用户，并向角色中添加新用户。 与该角色关联的许多权限都将自动应用于新用户。 如果组织中的多个用户需要相同的权限，将他们都添加到角色即可为他们授予相同的权限。  
  
-   对类似的安全对象（表、视图和过程）进行配置，使它们属于同一个架构，然后向架构授予权限。 例如，工资架构可能拥有多个表、视图和存储过程。 通过授予针对该架构的访问权限，可以同时授予执行工资功能所需的所有权限。 有关可向哪些安全对象授予权限的详细信息，请参阅 [Securables](../../../relational-databases/security/securables.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 授权者（或使用 AS 选项指定的主体）必须具有使用 GRANT OPTION 授予的权限本身，或具有隐含授予该权限的更高权限。 **sysadmin** 固定服务器角色成员可以授予任何权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-grant-permission-to-a-principal"></a>向主体授予权限  
  
1.  在“对象资源管理器”中，展开包含您要授予权限的对象的数据库。  
  
    > [!NOTE]  
    >  这些步骤仅针对向存储过程授予权限，但您可以使用类似的步骤向表、视图、函数和程序集以及其他安全对象添加权限。 有关详细信息，请参阅 [GRANT (Transact-SQL)](../../../t-sql/statements/grant-transact-sql.md)  
  
2.  展开 **“可编程性”** 文件夹。  
  
3.  展开 **“存储过程”** 文件夹。  
  
4.  右键单击某一存储过程，然后选择“属性”。  
  
5.  在“存储过程属性 – stored_procedure_name”对话框中选择某页面，然后选择“权限”。 使用此页可以将用户或角色添加到存储过程以及指定这些用户或角色所具有的权限。  
  
6.  完成后，单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-grant-permission-to-a-principal"></a>向主体授予权限  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- Grants EXECUTE permission on stored procedure HumanResources.uspUpdateEmployeeHireInfo to an application role called Recruiting11.   
    USE AdventureWorks2012;  
    GO  
    GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
        TO Recruiting11;  
    GO  
    ```  
  
 有关详细信息，请参阅 [GRANT (Transact-SQL)](../../../t-sql/statements/grant-transact-sql.md) 和 [GRANT 对象权限 (Transact-SQL)](../../../t-sql/statements/grant-object-permissions-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [主体（数据库引擎）](../../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
