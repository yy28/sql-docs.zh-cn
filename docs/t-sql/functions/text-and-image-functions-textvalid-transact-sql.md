---
title: "TEXTVALID (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTVALID_TSQL
- TEXTVALID
dev_langs:
- TSQL
helpviewer_keywords:
- invalid text pointers [SQL Server]
- valid text pointers [SQL Server]
- TEXTVALID function
- checking text pointers
- text-pointer values
- verifying text pointers
ms.assetid: 9411c349-b59b-4740-a270-92f91d81ad23
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d64916b441c65dc00e0e387e08c2967124721514
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="text-and-image-functions---textvalid-transact-sql"></a>文本和图像函数-TEXTVALID (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A**文本**， **ntext**，或**映像**检查特定的文本指针是否为有效的函数。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]没有可用的替代功能。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
TEXTVALID ( 'table.column' ,text_ ptr )  
```  
  
## <a name="arguments"></a>参数  
 *table*  
 要使用的表的名称。  
  
 *列*  
 要使用的列的名称。  
  
 *text_ptr*  
 要检查的文本指针。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>注释  
 如果指针有效则返回 1，无效则返回 0。 请注意，标识符**文本**列必须包含表名。 在没有有效的文本指针的情况下，不能使用 UPDATETEXT、WRITETEXT 或 READTEXT。  
  
 以下函数和语句也是有用当您使用时**文本**， **ntext**，和**映像**数据。  
  
|函数或语句|Description|  
|---------------------------|-----------------|  
|PATINDEX**(***%模式 %***，** *表达式***)**|返回指定的字符串的字符位置**文本**和**ntext**列。|  
|Datalength 之外**(***表达式***)**|返回中的数据长度**文本**， **ntext**，和**映像**列。|  
|SET TEXTSIZE|返回的限制，以字节为单位，**文本**， **ntext**，或**映像**与 SELECT 语句返回的数据。|  
  
## <a name="examples"></a>示例  
 以下示例报告是否存在用于 `logo` 表的 `pub_info` 列中的各个值的有效文本指针。  
  
> [!NOTE]  
>  若要运行此示例，你必须安装**pubs**数据库。  
  
```  
USE pubs;  
GO  
SELECT pub_id, 'Valid (if 1) Text data'   
   = TEXTVALID ('pub_info.logo', TEXTPTR(logo))   
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id Valid (if 1) Text data   
------ ----------------------   
0736   1                        
0877   1                        
1389   1                        
1622   1                        
1756   1                        
9901   1                        
9952   1                        
9999   1                        
  
(8 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [Datalength 之外 &#40;Transact SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40;Transact SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [设置 TEXTSIZE &#40;Transact SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [文本和图像函数 &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [TEXTPTR &#40;Transact SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)  
  
  
