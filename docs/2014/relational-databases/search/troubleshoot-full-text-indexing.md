---
title: 排除全文索引故障 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- indexes [full-text search]
- troubleshooting [SQL Server], full-text search
- troubleshooting [full-text search]
ms.assetid: 964c43a8-5019-4179-82aa-63cd0ef592ef
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cd7ce157e831d32272f6ff2531c39f789a01e901
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66015093"
---
# <a name="troubleshoot-full-text-indexing"></a>排除全文索引故障
     
##  <a name="troubleshoot-full-text-indexing-failures"></a><a name="failure"></a> 排除全文索引故障  
 填充或维护全文索引时，由于下面描述的原因，全文索引器可能无法对一个或多个行编制索引。 这些行级别的错误不会干扰填充的进行。 索引器会跳过这些行，这意味着您无法查询这些行中包含的内容。  
  
 在以下情况下，可能会发生索引失败：  
  
-   索引器找不到或无法加载筛选器或断字符组件。 如果表中的行所包含的文档格式或内容使用了尚未注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的语言，则这样的索引失败可能会发生。 如果在加载时已注册的断字符或筛选器组件未经过签名或签名验证失败，则这样的索引失败也可能会发生。  
  
-   诸如断字符或筛选器这样的组件失败，并向索引器返回错误。 如果所索引的文档已损坏，并且筛选器无法从该文档提取文本，则这样的索引失败可能会发生。 由于全文筛选器后台程序宿主 (fdhost.exe) 受到的内存限制，当组件无法处理超过某个大小的单行中的内容时，这样的索引失败也可能会发生。  
  
 对于每个行级别的失败，爬网日志将包含有关失败原因的详细信息。 将在完整或增量填充的末尾总计错误计数。  
  
 还有其他失败会影响索引进程本身，使填充无法完成：  
  
-   全文索引超过了全文目录中可以包含的行数限制。  
  
-   索引的表的聚集索引或全文键索引已更改、删除或重新生成。  
  
-   硬件故障或磁盘损坏导致全文目录遭到破坏。  
  
-   全文索引的表所在的文件组转到脱机状态，或已设为只读。  
  
 在任何重要的全文索引填充操作结束时，或在发现填充未完成时，应当查看爬网日志。  
  
### <a name="unsigned-components"></a>未签名的组件  
 默认情况下，全文索引器要求它所加载的筛选器和断字符经过签名。 如果它们未经过签名（这种情况有时是在安装自定义组件时造成的），则必须将全文索引器配置为忽略签名验证。  
  
> [!IMPORTANT]  
>  忽略签名验证将降低 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的安全性。 我们建议您对所实现的所有组件进行签名，或确保您获得的所有组件都经过签名。 有关对组件进行签名的信息，请参阅 [sp_fulltext_service (Transact SQL)](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)。  
  

  
##  <a name="full-text-index-in-inconsistent-state-after-transaction-log-restored"></a><a name="state"></a> 对事务日志进行还原后全文索引处于不一致状态  
 还原数据库的事务日志时可能会看到一条警告，指示全文索引处于不一致状态。 导致不一致的原因是在备份数据库之后，针对表的全文索引被修改了。 若要使全文索引处于一致状态，必须对表执行完全填充（爬网）。 有关详细信息，请参阅 [填充全文索引](../indexes/indexes.md)。  
  

  
## <a name="see-also"></a>另请参阅  
 [ALTER FULLTEXT CATALOG (Transact-SQL)](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)   
 [填充全文索引](../indexes/indexes.md)  
  
  
