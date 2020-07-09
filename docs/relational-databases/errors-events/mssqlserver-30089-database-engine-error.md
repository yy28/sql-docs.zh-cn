---
title: MSSQLSERVER_30089 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9992 (Database Engine error)
ms.assetid: 188e5bde-6865-4740-a2b2-582be8f55c77
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b08f229cd4afa3196f50af39a569072a562b3765
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723750"
---
# <a name="mssqlserver_30089"></a>MSSQLSERVER_30089
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|30089|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|IFTS_FDHOST_TERMINATEDABNORMAL|  
|消息正文|全文筛选器后台程序宿主(FDHost)进程已异常停止。 如果在执行全文检索或查询处理期间配置错误或工作不正常的语言组件(如断字器、词干分析器或筛选器)造成了无法恢复的错误，则会出现这种情况。 该进程将自动重新启动。|  
  
## <a name="explanation"></a>说明  
全文筛选器后台程序宿主遇到了某个强制其异常停止的问题。 该问题可能是由格式不正确的文档、筛选器或断字器中的错误或者筛选器后台程序中的问题引起的。  
  
## <a name="user-action"></a>用户操作  
通常，该后台程序将能够从错误中恢复。 如果它仍旧失败，则有必要排除故障。 请尝试执行下列操作来隔离此问题：  
  
1.  如果最近安装过新的语言组件，请将它从系统中删除。  
  
2.  查看爬网日志，找出无法对其建立全文检索的任何新文档并将其删除。  
  
## <a name="see-also"></a>另请参阅  
[sp_help_fulltext_system_components (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
[配置和管理断字符和词干分析器以便搜索](~/relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
[配置和管理搜索筛选器](~/relational-databases/search/configure-and-manage-filters-for-search.md)  
  
