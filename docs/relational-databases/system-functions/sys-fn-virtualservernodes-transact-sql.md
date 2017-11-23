---
title: "sys.fn_virtualservernodes (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_virtualservernodes
- fn_virtualservernodes_TSQL
dev_langs: TSQL
helpviewer_keywords:
- nodes [Faillover Clustering], virtual servers
- nodes [Faillover Clustering]
- virtual servers [Faillover Clustering]
- failover clustering [SQL Server], nodes
- fn_virtualservernodes function
- sys.fn_virtualservernodes function
ms.assetid: 257f3b8d-93c0-4444-87f1-ea211bd8cad0
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 404c45f4aa245d6aeba40ee11bdb6cf4ad98576e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysfnvirtualservernodes-transact-sql"></a>sys.fn_virtualservernodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  返回可运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的故障转移群集实例节点的列表。 此信息在故障转移群集环境中很有用。  
  
> [!IMPORTANT]  
>  这[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]系统函数是用于向后兼容。 我们建议你使用[sys.dm_os_cluster_nodes &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)相反。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
fn_virtualservernodes()  
```  
  
## <a name="tables-returned"></a>返回的表  
 如果当前服务器是群集的服务器， **fn_virtualservernodes**故障转移群集实例节点的列表返回此实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已定义。  
  
 如果当前服务器实例不是群集的服务器， **fn_virtualservernodes**返回行集为空。  
  
## <a name="permissions"></a>Permissions  
 用户必须具有的实例的 VIEW SERVER STATE 权限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `fn_virtualservernodes` 对群集服务器实例进行查询：  
  
```  
SELECT * FROM fn_virtualservernodes();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 NodeName  
  
 -------\-  
  
 SS3-CLUSN1  
  
 SS3-CLUSN2  
  
## <a name="see-also"></a>另请参阅  
 [sys.dm_os_cluster_nodes &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys.fn_servershareddrives &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)  
  
  
