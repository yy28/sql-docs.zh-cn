---
title: sp_prepexecrpc (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexecrpc
- sp_cursor_prepexecrpc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexecrpc
ms.assetid: 35d686f2-ef31-4eaa-baa9-9cef5d6c87c2
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab11cbca7177408ed94e79967ab55bad9fbc50b1
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43027951"
---
# <a name="spprepexecrpc-transact-sql"></a>sp_prepexecrpc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  准备和执行已使用 RPC 标识符指定的参数化存储过程调用。 sp_prepexecrpc 通过在表格格式数据流 (TDS) 包中指定 ID = 14 来调用。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_prepexecrpc handle OUTPUT, RPCCall  
    [ , bound_param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>参数  
 *句柄*  
 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成的已准备的句柄标识符。 *处理*为必需的参数且具有**int**返回值。  
  
 *RPCCall*  
 使用 ODBC 规范语法定义存储过程调用。 *RPCCall*是一个必需的参数，为调用**ntext**字符串输入值。  
  
 *bound_param*  
 指示可选使用其他参数。 *bound_param*需要输入任何数据类型来指定中使用的其他参数的值。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
