---
title: sys.bandwidth_usage （Azure SQL 数据库） |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- bandwidth_usage
- sys.bandwidth_usage
- bandwidth_usage_TSQL
- sys.bandwidth_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.bandwidth_usage
- bandwidth_usage
ms.assetid: 43ed8435-f059-4907-b5c0-193a258b394a
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a1bea0110a1e1b26862e9d2b76b6362b6aaf2a53
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="sysbandwidthusage-azure-sql-database"></a>sys.bandwidth_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **注意： 这仅适用于[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11。**  
  
 返回有关在每个数据库使用的网络带宽的信息 **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11 逻辑服务器**。 为给定数据库返回的每行总结在一小时内使用的单个方向和类别。  
  
 **中已弃用此[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V12 逻辑服务器。**  
  
 **Sys.bandwidth_usage**视图包含以下各列。  
  
|Column Name|Description|  
|-----------------|-----------------|  
|**time**|占用带宽的时间（小时）。 此视图中的各行以小时为单位。 例如，2009-09-19 02:00:00.000 表示占用带宽的时间是 2009 年 9 月 19 日的凌晨 2:00  到凌晨 3:00。|  
|**database_name**|占用带宽的数据库的名称。|  
|**方向**|占用带宽的类型，为以下选项之一：<br /><br /> 入口： 正在移入数据[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 出口： 正在移出数据[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|  
|class|占用带宽的类别，为以下选项之一：<br />正在移 Azure 平台中的内部： 数据。<br />正在移出 Azure 平台的外部： 数据。<br /><br /> 当数据库参与区域之间的连续复制关系后，才返回此类 ([!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)])。 If a given database does not participate in any continuous copy relationship, then “Interlink” rows are not returned. 有关详细信息，请参阅本主题后面的“备注”部分。|  
|**time_period**|使用情况的发生时的时间段是峰值或高峰。 The Peak time is based on the region in which the server was created. 例如，如果在“US_Northwest”地区创建了服务器，则高峰期时间定义为 PST 时间上午 10:00 点 到下午 6:00 太平洋标准时间。|  
|**数量**|占用的带宽量 (KB)。|  
  
## <a name="permissions"></a>权限  
 此视图选项仅适用于**master**与服务器级别主体登录名的数据库。  
  
## <a name="remarks"></a>注释  
  
### <a name="external-and-internal-classes"></a>External 和 Internal 类别  
 每个数据库的给定时间，使用**sys.bandwidth_usage**视图将返回显示的类和带宽使用方向的行。 下例列举给定数据库可能公开的数据。 在此示例中，时间为 2012-04-21 17:00: 00，即发生在高峰时段。 数据库名称为 Db1。 在此示例中， **sys.bandwidth_usage**已返回的入口和出口方向和外部和内部类的所有四个组合的行，如下所示：  
  
|time|database_name|direction|class|time_period|quantity|  
|----------|--------------------|---------------|-----------|------------------|--------------|  
|2012-04-21 17:00:00|Db1|Ingress|External|Peak|66|  
|2012-04-21 17:00:00|Db1|Egress|External|Peak|741|  
|2012-04-21 17:00:00|Db1|Ingress|Internal|Peak|1052|  
|2012-04-21 17:00:00|Db1|Egress|内部|Peak|3525|  
  
### <a name="interpreting-data-direction-for-includessgeodrincludesssgeodr-mdmd"></a>解释 [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] 的数据方向  
 对于 [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]，带宽使用情况数据在连续复制关系两侧的逻辑主数据库中可见。 因此必须从所查询的逻辑服务器的角度解释入口和出口方向指示器。 例如，考虑将 1 MB 的数据从源服务器传输到目标服务器的复制流。 在这种情况下，源服务器上 1 MB 计发送的总数据和在目标服务器上，1 MB 记录为收到的数据。  
  
> [!NOTE]  
>  这些数据按用户数据流的方向从源服务器传输到目标服务器。 但是，在另一方向也需要传输一些数据。  
  
  
