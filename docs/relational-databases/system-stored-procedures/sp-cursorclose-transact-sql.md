---
title: sp_cursorclose (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1d1e6f96076b01b01464b40bc4e3d65f3e1e2c42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spcursorclose-transact-sql"></a>sp_cursorclose (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  关闭和取消分配游标，以及释放所有关联的资源;也就是说，它会删除临时表使用的支持的密钥集或静态**光标**。 通过指定 ID 调用 sp_cursorclose = 9 表格格式数据流 (TDS) 数据包中的。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>参数  
 *cursor*  
 是光标*处理*生成值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 sp_cursoropen 过程返回的。 *光标*是必需的参数来调用**int**输入值。  
  
> [!NOTE]  
>  输入值 -1 将应用于当前连接上的所有游标。  
  
## <a name="remarks"></a>注释  
 *光标*将返回错误消息，如果游标已关闭后运行该过程，或指定无效句柄。  
  
 RPC 状态指示总体成功或失败。  
  
 DONE 行计数始终为 0。  
  
## <a name="see-also"></a>另请参阅  
 [sp_cursoropen &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
