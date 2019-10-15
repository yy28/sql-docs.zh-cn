---
title: sp_altermessage （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_altermessage_TSQL
- sp_altermessage
dev_langs:
- TSQL
helpviewer_keywords:
- sp_altermessage
ms.assetid: 1b28f280-8ef9-48e9-bd99-ec14d79abaca
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4949307cdaf2cc712e56525e872381c2af8256fd
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304791"
---
# <a name="sp_altermessage-transact-sql"></a>sp_altermessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例中用户定义消息或系统消息的状态。 可以使用**sys.databases**目录视图查看用户定义的消息。  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_altermessage [ @message_id = ] message_number   ,[ @parameter = ]'write_to_log'  
   ,[ @parameter_value = ]'value'   
```  
  
## <a name="arguments"></a>参数  
 [ **@message_id =** ] *message_number*  
 要从**sys.databases**更改的消息的错误号。 *message_number*的值为**int** ，没有默认值。  
  
`[ @parameter = ] 'write\_to\_log_'` 用于 **@no__t 2parameter_value** ，以指示要将消息写入到 @no__t Windows 应用程序日志中。 *write_to_log*的值为**sysname** ，无默认值。 *write_to_log*必须设置为 WITH_LOG 或 NULL。 如果*write_to_log*设置为 WITH_LOG 或 NULL，并且 **@no__t**的值为**true**，则会将消息写入 Windows 应用程序日志。 如果*write_to_log*设置为 WITH_LOG 或 NULL，并且的值 **@no__t**为**false**，则不会始终将消息写入 Windows 应用程序日志，而是根据错误的引发方式写入消息。 如果指定了*write_to_log* ，则还必须指定 **\@parameter_value**的值。  
  
> [!NOTE]  
>  如果消息写入了 Windows 应用程序日志，那么它也将被写入[!INCLUDE[ssDE](../../includes/ssde-md.md)]错误日志文件。  
  
`[ @parameter_value = ]'value_'` 用于 **@no__t 2parameter** ，以指示将错误写入到 @no__t Windows 应用程序日志。 *值*为**varchar （5）** ，无默认值。 如果**为 true**，则始终将错误写入 Windows 应用程序日志。 如果**为 false**，则不会始终将错误写入 Windows 应用程序日志，而是根据错误的引发方式写入。 如果指定*value* ，则还必须指定*write_to_log* for **3parameter @no__t** 。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 **Sp_altermessage**与 WITH_LOG 选项的影响与 RAISERROR with LOG 参数的影响相似，不同之处在于**sp_altermessage**更改现有消息的日志记录行为。 如果消息已更改为 WITH_LOG，则总是将其写入 Windows 应用程序日志，而不管这一错误是怎样造成的。 即使执行 RAISERROR 时不含 WITH_LOG 选项，也会将错误写入 Windows 应用程序日志。  
  
 可以使用**sp_altermessage**修改系统消息。  
  
## <a name="permissions"></a>权限  
 要求具有**serveradmin**固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 以下示例将使现有消息 `55001` 记录到 Windows 应用程序日志中。  
  
```  
EXECUTE sp_altermessage 55001, 'WITH_LOG', 'true';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [RAISERROR (Transact-SQL)](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_addmessage (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
