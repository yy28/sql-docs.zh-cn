---
title: sys.fulltext_languages (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fulltext_languages
- sys.fulltext_languages_TSQL
- fulltext_languages
- fulltext_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- languages [full-text search]
- sys.fulltext_languages catalog view
ms.assetid: 2ed6b53d-1cf2-4763-9d58-36ea24a610ef
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: dabc9334091b5b545c78b069b3e9f31a5a68a1bd
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysfulltextlanguages-transact-sql"></a>sys.fulltext_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册了断字符的每种语言在此目录视图中均存在对应的一行。 每行显示的 LCID 和的语言名称。 注册了某种语言的断字符后，可在全文索引/查询操作中使用它的其他语言资源：词干分析器、干扰词（非索引字）和同义词库文件。 值**名称**或**lcid**的全文查询和全文索引中只能指定[!INCLUDE[tsql](../../includes/tsql-md.md)]语句。  
   
|列|数据类型|Description|  
|------------|---------------|-----------------|  
|**lcid**|**int**|语言的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 区域设置标识符 (LCID)。|  
|**名称**|**sysname**|是中的别名值[sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)对应的值**lcid**或的字符串表示形式的数字的 LCID。|  
  
## <a name="values-returned-for-default-languages"></a>针对默认语言返回的值  
 下表显示在默认情况下为其注册了断字符的语言的值。  
  
|语言|LCID|  
|--------------|----------|  
|阿拉伯语|1025|  
|孟加拉语（印度）|1093|  
|英国英语|2057|  
|保加利亚语|1026|  
|加泰罗尼亚语|1027|  
|中文（中华人民共和国香港特别行政区）|3076|  
|中文（中国澳门特别行政区）|5124|  
|中文（新加坡）|4100|  
|克罗地亚语|1050|  
|捷克语|1029|  
|丹麦语|1030|  
|荷兰语|1043|  
|英语|2052|  
|法语|1036|  
|德语|1031|  
|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 希腊语|1032|  
|古吉拉特语|1095|  
|Hebrew|1037|  
|Hindi|1081|  
|冰岛语|1039|  
|印度尼西亚语|1057|  
|意大利语|1040|  
|日语|1041|  
|卡纳达语|1099|  
|朝鲜语|1042|  
|拉脱维亚语|1062|  
|立陶宛语|1063|  
|马来语 - 马来西亚|1086|  
|马拉雅拉姆语|1100|  
|马拉地语|1102|  
|非特定语言|0|  
|挪威语（博克马尔语）|1044|  
|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 波兰语|1045|  
|葡萄牙语（巴西）|1046|  
|葡萄牙语（葡萄牙）|2070|  
|旁遮普语|1094|  
|罗马尼亚语|1048|  
|俄语|1049|  
|塞尔维亚语（西里尔）|3098|  
|塞尔维亚语（拉丁）|2074|  
|简体中文|2052|  
|斯洛伐克语|1051|  
|斯洛文尼亚语|1060|  
|西班牙语|3082|  
|瑞典语|1053|  
|泰米尔语|1097|  
|泰卢固语|1098|  
|泰国语|1054|  
|繁体中文|1028|  
|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 土耳其语|1055|  
|乌克兰语|1058|  
|乌尔都语|1056|  
|越南语|1066|  
  
## <a name="remarks"></a>注释  
 若要更新使用的全文搜索已注册的语言列表，请使用[sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)**update_languages**。  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [sp_fulltext_load_thesaurus_file &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)   
 [sp_fulltext_service (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [配置和管理断字符和词干分析器以便搜索](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [为配置和管理同义词库文件的全文搜索](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [为配置和管理非索引字和非索引字表的全文搜索](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [升级全文搜索](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
