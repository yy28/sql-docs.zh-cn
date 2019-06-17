---
title: sp_cursorclose (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 56ff3e67c51be8618f0254298a7d8707e18884ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62724223"
---
# <a name="spcursorclose-transact-sql"></a>sp_cursorclose (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  关闭和取消游标分配，以及释放所有关联的资源;即，它删除用于支持 KEYSET 或 STATIC 的临时表**游标**。 通过指定 ID 来调用 sp_cursorclose = 9 在表格格式数据流 (TDS) 包中的。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>参数  
 *cursor*  
 是游标*处理*生成的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并由 sp_cursoropen 过程返回。 *游标*是一个必需的参数，为调用**int**输入值。  
  
> [!NOTE]  
>  输入值 -1 将应用于当前连接上的所有游标。  
  
## <a name="remarks"></a>备注  
 *游标*将返回错误消息，如果关闭游标之后运行了该过程或指定无效的句柄。  
  
 RPC 状态指示总体成功或失败。  
  
 DONE 行计数始终为 0。  
  
## <a name="see-also"></a>请参阅  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
