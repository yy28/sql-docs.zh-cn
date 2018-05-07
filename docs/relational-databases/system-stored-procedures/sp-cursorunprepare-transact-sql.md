---
title: sp_cursorunprepare (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursorunprepare_TSQL
- sp_cursorunprepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorunprepare
ms.assetid: b46d4813-c4a9-4f9d-9979-2b5082ecf06a
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4e20d5669a7879584cd0c7dc1c26726a6ba12643
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spcursorunprepare-transact-sql"></a>sp_cursorunprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  放弃执行计划在 sp_cursorprepare 中开发存储过程。 通过指定 ID 调用 sp_cursorunprepare = 6 表格格式数据流 (TDS) 数据包中的。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cursorunprepare handle  
```  
  
## <a name="arguments"></a>参数  
 *句柄*  
 是*处理*sp_cursorprepare 当准备该语句返回的值。  
  
## <a name="see-also"></a>另请参阅  
 [sp_cursorprepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
