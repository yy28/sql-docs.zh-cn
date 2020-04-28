---
title: 加载数据
description: 您可以使用 Integration Services、bcp 实用工具、dwloader 或 SQL INSERT 语句将数据加载或插入 SQL Server 并行数据仓库（PDW）。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd161820fd53d45642848697bce9589a98dec4ca
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401041"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>将数据加载到并行数据仓库
您可以通过使用 Integration Services、 [Bcp 实用工具](../tools/bcp-utility.md)、 **Dwloader**命令行加载程序或 SQL insert 语句将数据加载到 SQL Server 并行数据仓库（PDW）。  

## <a name="loading-environment"></a>正在加载环境  
若要加载数据，需要一个或多个加载服务器。 你可以使用自己的现有 ETL 或其他服务器，也可以购买新服务器。 有关详细信息，请参阅[获取和配置加载服务器](acquire-and-configure-loading-server.md)。 这些说明包括[负载服务器容量规划工作表](loading-server-capacity-planning-worksheet.md)，可帮助你规划正确的加载解决方案。  
  
## <a name="load-with-dwloader"></a>用 dwloader 加载  
使用[Dwloader 命令行加载程序](dwloader.md)是将数据加载到 PDW 的最快方法。  
  
![正在加载进程](media/loading-process.png "加载进程")  
  
dwloader 将数据直接加载到计算节点，而无需通过控制节点传递数据。 若要加载数据，dwloader 首先与控制节点进行通信，以获取计算节点的联系信息。 dwloader 设置每个计算节点的通信通道，然后以循环方式将256KB 数据块发送到计算节点。  
  
在每个计算节点上，数据移动服务（DMS）接收并处理数据块。 处理数据时，将每行转换为 SQL Server 本机格式，并计算分发哈希，以确定每行所属的计算节点。  
  
处理行后，DMS 使用无序移动将每一行传输到正确的计算节点和 SQL Server 的实例。 当 SQL Server 收到行时，它会根据 dwloader 中设置的 **-b**批大小参数对它们进行批处理，然后大容量加载该批。  

## <a name="load-with-prepared-statements"></a>用预定义语句加载

您可以使用预定义的语句将数据加载到分布式表和复制表中。 如果输入数据与目标数据类型不匹配，则会执行隐式转换。 由 PDW 预定义语句支持的隐式转换是 SQL Server 支持的转换的子集。 也就是说，仅支持一个转换子集，但支持的转换与 SQL Server 隐式转换相匹配。 无论要加载的目标表是否定义为分布式表或复制表，都将对目标表中存在的所有列应用隐式转换（如果需要）。 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务|说明|  
|--------|---------------|  
|创建临时数据库。|[创建临时数据库](staging-database.md)|  
|Integration Services 负载。|[使用 Integration Services 加载](load-with-ssis.md)|  
|了解 dwloader 的类型转换。|[适用于 dwloader 的数据类型转换规则](dwloader-data-type-conversion-rules.md)|  
|将数据加载到 dwloader。|[dwloader 命令行加载器](dwloader.md)|  
|了解 INSERT 的类型转换。|[使用 INSERT 加载数据](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
