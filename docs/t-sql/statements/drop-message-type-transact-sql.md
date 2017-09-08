---
title: "删除消息类型 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_MESSAGE_TYPE_TSQL
- DROP MESSAGE TYPE
dev_langs:
- TSQL
helpviewer_keywords:
- message types [Service Broker], removing
- deleting message types
- dropping message types
- DROP MESSAGE TYPE statement
- removing message types
ms.assetid: 805e8ad5-8a93-49f0-88e5-e6fca8814dd5
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 859419b6809d1c44486130eadaf30c1411a03b97
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-message-type-transact-sql"></a>DROP MESSAGE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除一个现有消息类型。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP MESSAGE TYPE message_type_name  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *message_type_name*  
 要删除的消息类型的名称。 不能指定服务器、数据库和架构名称。  
  
## <a name="permissions"></a>Permissions  
 默认情况下，消息类型的所有者、db_ddladmin 或 db_owner 固定数据库角色的成员以及 sysadmin 固定服务器角色的成员拥有删除消息类型的权限。  
  
## <a name="remarks"></a>注释  
 如果有任何约定引用了某个消息类型，则无法删除该消息类型。  
  
## <a name="examples"></a>示例  
 下例从数据库中删除 `//Adventure-Works.com/Expenses/SubmitExpense` 消息类型。  
  
```  
DROP MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense] ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER 消息类型 &#40;Transact SQL &#41;](../../t-sql/statements/alter-message-type-transact-sql.md)   
 [创建消息类型 &#40;Transact SQL &#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
