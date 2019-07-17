---
title: sp_altermessage (TRANSACT-SQL) |Microsoft Docs
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
ms.openlocfilehash: 0722bbc713804af6b2b97b5651df5b564d17a136
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117795"
---
# <a name="spaltermessage-transact-sql"></a>sp_altermessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例中用户定义消息或系统消息的状态。 可以使用查看用户定义的消息**sys.messages**目录视图。  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_altermessage [ @message_id = ] message_number   ,[ @parameter = ]'write_to_log'  
   ,[ @parameter_value = ]'value'   
```  
  
## <a name="arguments"></a>参数  
 [ **@message_id =** ] *message_number*  
 是从更改的消息的错误号**sys.messages**。 *message_number*是**int** ，无默认值。  
  
`[ @parameter = ] 'write\_to\_log_'` 与一起使用 **@parameter_value** 以指示该消息将写入到[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 应用程序日志。 *write_to_log*是**sysname** ，无默认值。 *write_to_log*必须设置为 WITH_LOG 或 NULL。 如果*write_to_log*设置为 WITH_LOG 或 NULL，并且的值 **@parameter_value** 是**true**，到 Windows 应用程序日志写入消息。 如果*write_to_log*设置为 WITH_LOG 或 NULL，并且的值 **@parameter_value** 是**false**，消息不始终写入 Windows 应用程序日志，但可能编写根据如何产生错误。 如果*write_to_log*指定的值 **@parameter_value** 还必须指定。  
  
> [!NOTE]  
>  如果消息写入了 Windows 应用程序日志，那么它也将被写入[!INCLUDE[ssDE](../../includes/ssde-md.md)]错误日志文件。  
  
`[ @parameter_value = ]'value_'` 与一起使用 **@parameter** 以指示要写入到错误[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 应用程序日志。 *值*是**varchar(5)** ，无默认值。 如果 **，则返回 true**，此错误始终写入 Windows 应用程序日志。 如果**false**，该错误不始终写入 Windows 应用程序日志，但可能会根据如何产生此错误将写入。 如果*值*指定，则*write_to_log*有关 **@parameter** 还必须指定。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 效果**sp_altermessage** WITH_LOG 选项是类似于 RAISERROR WITH LOG 参数，不同之处在于**sp_altermessage**更改现有的消息的日志记录行为。 如果消息已更改为 WITH_LOG，则总是将其写入 Windows 应用程序日志，而不管这一错误是怎样造成的。 即使执行 RAISERROR 时不含 WITH_LOG 选项，也会将错误写入 Windows 应用程序日志。  
  
 可以通过修改系统消息**sp_altermessage**。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**serveradmin**固定的服务器角色。  
  
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
  
  
