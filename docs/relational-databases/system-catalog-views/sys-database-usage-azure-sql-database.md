---
title: "sys.database_usage （Azure SQL 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- database_usage
- database_usage_TSQL
- sys.database_usage_TSQL
- sys.database_usage
dev_langs: TSQL
helpviewer_keywords:
- database_usage
- sys.database_usage
ms.assetid: be6820de-60bf-4ddd-ace7-4077893d630f
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 670c1a9c7028d495141247b5f2b8b35f85142d6f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **注意： 这仅适用于 Azure SQL 数据库 V11。**  
  
 列出在数量、 类型和持续时间的数据库[!INCLUDE[ssSDS](../../includes/sssds-md.md)]服务器。  
  
 **Sys.database_usage**视图包含以下各列。  
  
|列名|Description|  
|-----------------|-----------------|  
|time|使用事件发生的日期。|  
|sku|为数据库服务层的类型： **Web**，**业务**，**基本**，**标准**，**高级**|  
|quantity|指定当天存在的 SKU 类型的数据库的最大数量。|  
  
## <a name="permissions"></a>Permissions  
 对此视图的只读访问可供所有用户有权连接到**master**数据库。  
  
## <a name="remarks"></a>注释  
 **Sys.database_usage**查看你的订阅的每一天返回一行。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据库定价详细信息](http://go.microsoft.com/fwlink/?LinkID=394978)   
 [帐户和 Windows Azure SQL Database 中的计费](http://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
