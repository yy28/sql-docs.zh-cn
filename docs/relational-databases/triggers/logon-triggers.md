---
title: 登录触发器 | Microsoft Docs
ms.custom: ''
ms.date: 03/19/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- logon triggers
- login triggers
helpviewer_keywords:
- triggers [SQL Server], logon
ms.assetid: 2f0ebb2f-de10-482d-9806-1a5de5b312b8
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ebc4f10802f7a90dc828bab4b6f2aa1d01d6ccd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68058621"
---
# <a name="logon-triggers"></a>登录触发器
[!INCLUDE[tsql-appliesto-ss2008-appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
  登录触发器将为响应 LOGON 事件而激发存储过程。 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例建立用户会话时将引发此事件。 登录触发器将在登录的身份验证阶段完成之后且用户会话实际建立之前激发。 因此，来自触发器内部且通常将到达用户的所有消息（例如错误消息和来自 PRINT 语句的消息）会传送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志。 如果身份验证失败，将不激发登录触发器。  
  
 可以使用登录触发器来审核和控制服务器会话，例如通过跟踪登录活动、限制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的登录名或限制特定登录名的会话数。 例如，在以下代码中，如果登录名 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login_test *已经创建了三个用户会话，登录触发器将拒绝由该登录名启动的* 登录尝试。  
  
```  
USE master;  
GO  
CREATE LOGIN login_test WITH PASSWORD = '3KHJ6dhx(0xVYsdf' MUST_CHANGE,  
    CHECK_EXPIRATION = ON;  
GO  
GRANT VIEW SERVER STATE TO login_test;  
GO  
CREATE TRIGGER connection_limit_trigger  
ON ALL SERVER WITH EXECUTE AS 'login_test'  
FOR LOGON  
AS  
BEGIN  
IF ORIGINAL_LOGIN()= 'login_test' AND  
    (SELECT COUNT(*) FROM sys.dm_exec_sessions  
            WHERE is_user_process = 1 AND  
                original_login_name = 'login_test') > 3  
    ROLLBACK;  
END;  
```  
  
 请注意，LOGON 事件对应于 AUDIT_LOGIN SQL Trace 事件，该事件可在 [事件通知](../../relational-databases/service-broker/event-notifications.md)中使用。 触发器与事件通知的主要区别在于触发器随事件同步引发，而事件通知是异步的。 也就是说，例如，如果要停止建立会话，则必须使用登录触发器。 AUDIT_LOGIN 事件的事件通知不能用于此目的。  
  
## <a name="specifying-first-and-last-trigger"></a>指定第一个和最后一个触发器  
 可以对 LOGON 事件定义多个触发器。 通过使用 [sp_settriggerorder](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md) 系统存储过程，可以将这些触发器中的任何一个指定为针对某事件激发的第一个或最后一个触发器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不保证其余触发器的执行顺序。  
  
## <a name="managing-transactions"></a>管理事务  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 激发登录触发器之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会创建独立于任何用户事务的隐式事务。 因此，第一个登录触发器开始激发时，事务计数为 1。 所有登录触发器完成执行后，将提交事务。 与其他类型的触发器一样，如果登录触发器完成执行后事务计数为 0， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回错误。 ROLLBACK TRANSACTION 语句将事务计数重置为 0，即使该语句在嵌套事务中执行也会如此。 COMMIT TRANSACTION 可能将事务计数递减到 0。 因此，建议不要在登录触发器中发出 COMMIT TRANSACTION 语句。  
  
 如果要在登录触发器中使用 ROLLBACK TRANSACTION 语句，请注意以下事项：  
  
-   将回滚对 ROLLBACK TRANSACTION 点所做的任何数据修改。 这些修改包括当前触发器所做的修改以及对同一事件执行的先前触发器所做的修改。 此特定事件的任何其余触发器将不会执行。  
  
-   当前触发器继续执行显示在 ROLLBACK 语句之后的所有剩余语句。 如果这些语句中的任意语句修改数据，则不回滚这些修改。  
  
 如果在针对 LOGON 事件执行触发器的过程中满足下列任何一个条件，将不会建立用户会话：  
  
-   原始隐式事务回滚或失败。  
  
-   触发器正文中出现严重级别大于 20 的错误。  
  
## <a name="disabling-a-logon-trigger"></a>禁用登录触发器  
 登录触发器可以有效地阻止所有用户（包括 [!INCLUDE[ssDE](../../includes/ssde-md.md)] sysadmin **固定服务器角色的成员）与** 的成功连接。 在登录触发器正在阻止连接时， **sysadmin** 固定服务器角色的成员可通过使用专用管理员连接，或者通过以最小配置模式 (-f) 启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，来进行连接。 有关详细信息，请参阅 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务|主题|  
|----------|-----------|  
|说明如何创建登录触发器。 登录触发器可从任何数据库创建，但在服务器级注册，并驻留在 **master** 数据库中。|[CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)|  
|说明如何修改登录触发器。|[ALTER TRIGGER (Transact-SQL)](../../t-sql/statements/alter-trigger-transact-sql.md)|  
|说明如何删除登录触发器。|[DROP TRIGGER (Transact-SQL)](../../t-sql/statements/drop-trigger-transact-sql.md)|  
|说明如何返回有关登录触发器的信息。|[sys.server_triggers (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)<br /><br /> [sys.server_trigger_events (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)|  
|说明如何捕获登录触发器事件数据。||  
  
## <a name="see-also"></a>另请参阅  
 [DDL 触发器](../../relational-databases/triggers/ddl-triggers.md)  
  
  
