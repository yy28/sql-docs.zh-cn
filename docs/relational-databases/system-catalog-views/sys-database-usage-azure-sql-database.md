---
title: sys.database_usage （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_usage
- database_usage_TSQL
- sys.database_usage_TSQL
- sys.database_usage
dev_langs:
- TSQL
helpviewer_keywords:
- database_usage
- sys.database_usage
ms.assetid: be6820de-60bf-4ddd-ace7-4077893d630f
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: f17e34de7c230b111652ea57a3baa072a442a6a5
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51656736"
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **注意： 这仅适用于 Azure SQL 数据库 V11。**  
  
 列出在数量、 类型和持续时间的数据库[!INCLUDE[ssSDS](../../includes/sssds-md.md)]服务器。  
  
 **Sys.database_usage**视图包含以下各列。  
  
|列名|Description|  
|-----------------|-----------------|  
|time|使用事件发生的日期。|  
|sku|数据库服务层的类型： **Web**，**业务**，**基本**，**标准**，**高级**|  
|quantity|指定当天存在的 SKU 类型的数据库的最大数量。|  
  
## <a name="permissions"></a>Permissions  
 对此视图的只读访问可供有权连接到的所有用户**主**数据库。  
  
## <a name="remarks"></a>备注  
 **Sys.database_usage**视图的每一天的你的订阅返回一行。  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据库定价详细信息](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [帐户和 Windows Azure SQL Database 中的计费](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
