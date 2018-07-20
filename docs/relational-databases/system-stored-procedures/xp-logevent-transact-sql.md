---
title: xp_logevent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_logevent
- xp_logevent_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logevent
ms.assetid: 7b379ad0-5b12-4d2e-9c52-62465df1fdbd
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ddec196efe5022e0cfbbdf13c117a35beeba29ed
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102835"
---
# <a name="xplogevent-transact-sql"></a>xp_logevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  登录的用户定义的消息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日志文件和 Windows 事件查看器中。 可以使用 xp_logevent 发送警报，而无需向客户端发送一条消息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xp_logevent { error_number , 'message' } [ , 'severity' ]  
```  
  
## <a name="arguments"></a>参数  
 *error_number*  
 用户定义错误号，该值大于 50,000。 最大值为 2147483647 (2^31 - 1)。  
  
 **'** *消息*   
 最多 2048 个字符的字符串。  
  
 **'** *严重性*   
 以下三个字符串之一：INFORMATIONAL、WARNING 或 ERROR。 *严重性*是可选的默认值为 INFORMATIONAL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 对于所包含的代码示例，xp_logevent 返回下列错误消息：  
  
 `The command(s) completed successfully.`  
  
## <a name="remarks"></a>Remarks  
 当发送邮件[!INCLUDE[tsql](../../includes/tsql-md.md)]过程、 触发器、 批处理等，而不是 xp_logevent 使用 RAISERROR 语句。 xp_logevent 不调用客户端的消息处理程序也不设置@ERROR。 若要将消息写入 Windows 事件查看器以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志文件中，请执行 RAISERROR 语句。  
  
## <a name="permissions"></a>Permissions  
 需要 master 数据库中的 db_owner 固定数据库角色的成员身份，或者 sysadmin 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 以下示例将消息以及传递给消息的变量记录到 Windows 事件查看器中。  
  
```  
DECLARE @@TABNAME varchar(30), @@USERNAME varchar(30), @@MESSAGE varchar(255);  
SET @@TABNAME = 'customers';  
SET @@USERNAME = USER_NAME();  
SELECT @@MESSAGE = 'The table ' + @@TABNAME + ' is not owned by the user   
   ' + @@USERNAME + '.';  
  
USE master;  
EXEC xp_logevent 60000, @@MESSAGE, informational;  
```  
  
## <a name="see-also"></a>请参阅  
 [PRINT (Transact-SQL)](../../t-sql/language-elements/print-transact-sql.md)   
 [RAISERROR (Transact-SQL)](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [常规扩展存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
