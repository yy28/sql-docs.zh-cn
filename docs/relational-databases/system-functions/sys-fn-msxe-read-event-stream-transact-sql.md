---
title: sys.fn_MSxe_read_event_stream (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_MSxe_read_event_stream_TSQL
- sys.fn_MSxe_read_event_stream_TSQL
- sys.fn_MSxe_read_event_stream
- fn_MSxe_read_event_stream
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_MSxe_read_event_stream
- fn_MSxe_read_event_stream
ms.assetid: 5edb1162-625a-41e0-8ec9-1edc8ab9a74a
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 874378f4737e908bde380df4e426c4fea89badbd
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysfnmsxereadeventstream-transact-sql"></a>sys.fn_MSxe_read_event_stream (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  扩展事件提供表值函数 (TVF)，供扩展事件用户界面 (UI) 内部使用。 表本身不提供客户可以使用的数据。  
  
 若要查看事件数据，请使用以下项之一：  
  
-   扩展事件的新会话 UI。  
  
-   fn_xe_file_target_read_file TVF。 有关详细信息，请参阅 [sys.fn_xe_file_target_read_file (Transact SQL)](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.fn_MSxe_read_event_stream ( session_name)  
```  
  
## <a name="arguments"></a>参数  
 *Session_name*  
 服务器上运行的会话的名称。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|type|**整数 (4)**|事件类型。 不可为 null。|  
|data|**映像 (16)**|事件图像数据。 可以为 Null。|  
  
## <a name="see-also"></a>另请参阅  
 [扩展事件动态管理视图](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [扩展事件目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
  
