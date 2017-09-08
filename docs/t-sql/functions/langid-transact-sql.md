---
title: "@@LANGID (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@LANGID'
- '@@LANGID_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- languages [SQL Server], current in use
- '@@LANGID function'
- current language in use
- ID for language in use
- local language IDs [SQL Server]
ms.assetid: 7a0fc089-2a48-4a81-9d78-2aaedb540d37
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4e27e2678cd5c54f44711ecd3d5d1d75a85f1a16
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="langid-transact-sql"></a>@@LANGID (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回当前使用的语言的本地语言标识符 (ID)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
@@LANGID  
```  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>注释  
 若要查看有关语言设置，包括语言 ID 号的信息运行**sp_helplanguage**而无需指定的参数。  
  
## <a name="examples"></a>示例  
 以下示例将当前会话的语言设置为 `Italian`，然后使用 `@@LANGID` 返回意大利语的 ID。  
  
```  
SET LANGUAGE 'Italian'  
SELECT @@LANGID AS 'Language ID'  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Changed language setting to Italiano.  
Language ID  
-----------  
6            
```  
  
## <a name="see-also"></a>另请参阅  
 [配置函数 (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [设置语言 &#40;Transact SQL &#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [sp_helplanguage &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)  
  
  
