---
title: sp_prepexecrpc （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexecrpc
- sp_cursor_prepexecrpc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexecrpc
ms.assetid: 35d686f2-ef31-4eaa-baa9-9cef5d6c87c2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 26f298a102c69c8bc75721db531275379080005a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830963"
---
# <a name="sp_prepexecrpc-transact-sql"></a>sp_prepexecrpc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  准备和执行已使用 RPC 标识符指定的参数化存储过程调用。 sp_prepexecrpc 通过在表格格式数据流 (TDS) 包中指定 ID = 14 来调用。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_prepexecrpc handle OUTPUT, RPCCall  
    [ , bound_param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>参数  
 *柄*  
 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成的已准备的句柄标识符。 *句柄*是带有**int**返回值的必需参数。  
  
 *RPCCall*  
 使用 ODBC 规范语法定义存储过程调用。 *RPCCall*是用于调用**ntext**字符串输入值的必需参数。  
  
 *bound_param*  
 指示可选使用其他参数。 *bound_param*调用任何数据类型的输入值来指定要使用的其他参数。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
