---
title: sp_invalidate_textptr (Transact SQL) |Microsoft 文档
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
- sp_invalidate_textptr_TSQL
- sp_invalidate_textptr
dev_langs:
- TSQL
helpviewer_keywords:
- sp_invalidate_textptr
ms.assetid: dd9920e1-7064-4c05-93d8-9303103fa1d6
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 77b48427c017b543d73bf93e03a09fd7c4d50c78
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spinvalidatetextptr-transact-sql"></a>sp_invalidate_textptr (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使事务中指定的行内文本指针或所有行内文本指针失效。 **sp_invalidate_textptr**可仅在行内文本指针。 这些指针是从表具有**一行中的文本**选项处于启用状态。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_invalidate_textptr [ [ @TextPtrValue = ] textptr_value ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@TextPtrValue=** ] *textptr_value*  
 要失效的行内文本指针。 *textptr_value*是**varbinary (**16**)**，默认值为 NULL。 如果为 NULL， **sp_invalidate_textptr**失效在事务中的所有行内文本指针。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许每个数据库中的每个事务最多拥有 1,024 个活动的有效行内文本指针；而跨多个数据库的事务可在每个数据库中拥有 1,024 个行内文本指针。 **sp_invalidate_textptr**可用来使无效行内文本指针，并因此，可用空间的其他行内文本指针。  
  
 有关 text in row 选项的详细信息，请参阅[sp_tableoption &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_tableoption & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)   
 [TEXTPTR (Transact-SQL)](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [TEXTVALID (Transact-SQL)](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)  
  
  
