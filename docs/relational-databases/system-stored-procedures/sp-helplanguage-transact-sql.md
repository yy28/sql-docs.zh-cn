---
title: "sp_helplanguage (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helplanguage
- sp_helplanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplanguage
- default languages
ms.assetid: 8c4651a5-7dbc-49c5-8691-dc72103c2dfa
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a94f66688ce53aef2dcf575d58e16ed6f2f1672b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sphelplanguage-transact-sql"></a>sp_helplanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  报告有关 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的某个特定的替代语言或所有语言的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helplanguage [ [ @language = ] 'language' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@language=** ] *语言*  
 要显示其信息的替代语言的名称。 *语言*是**sysname**，默认值为 NULL。 如果*语言*是指定，返回有关指定语言的信息。 如果未指定语言中的所有语言有关的信息**sys.syslanguages**返回兼容性视图。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**langid**|**int**|语言标识号。|  
|**dateformat**|**nchar(3)**|日期的格式。|  
|**datefirst**|**tinyint**|每周的第一天：1 代表星期一，2 代表星期二，依此类推，直到 7 代表星期日。|  
|**升级**|**int**|最后一次升级此语言的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。|  
|**名称**|**sysname**|语言名称。|  
|**别名**|**sysname**|语言的替代名称。|  
|**月**|**nvarchar(372)**|月份名称。|  
|**简写**|**nvarchar(132)**|月份简称。|  
|**天**|**nvarchar(217)**|日期名称。|  
|**lcid**|**int**|语言的 Windows 区域设置 ID。|  
|**msglangid**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]消息组 ID。|  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-information-about-a-single-language"></a>A. 返回有关单个语言的信息  
 以下示例显示有关替代语言 `French` 的信息。  
  
```  
sp_helplanguage French;  
```  
  
### <a name="b-returning-information-about-all-languages"></a>B. 返回有关所有语言的信息  
 以下示例显示有关所有安装的替代语言的信息。  
  
```  
sp_helplanguage;  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [@@LANGUAGE (Transact-SQL)](../../t-sql/functions/language-transact-sql.md)   
 [设置语言 &#40;Transact SQL &#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
