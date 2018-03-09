---
title: "加载"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "你可以加载或使用数据插入到 SQL Server 并行数据仓库 (PDW) Integration Services、 bcp 实用工具、 dwloader 或 SQL INSERT 语句。"
ms.date: 10/20/2016
ms.topic: article
ms.assetid: c7292108-4a48-409e-b0f4-e4ba84dce26f
caps.latest.revision: "22"
ms.openlocfilehash: be5ea7c2b939b58c7dfd826965f1568431cb1bff
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="load-sql-server-pdw"></a>负载 (SQL Server PDW)
可以加载，也可以使用数据插入到 SQL Server 并行数据仓库 (PDW) Integration Services， [bcp 实用工具](../tools/bcp-utility.md)， **dwloader**命令行加载程序或 SQL INSERT 语句。  

## <a name="loading-environment"></a>加载环境  
若要加载数据，你需要一个或多个加载服务器。 你可以使用你自己现有 ETL 或其他服务器，或者，你可以购买新的服务器。 有关详细信息，请参阅[获取和配置加载服务器](acquire-and-configure-loading-server.md)。 这些说明包括[加载服务器容量规划工作表](loading-server-capacity-planning-worksheet.md)来帮助你规划加载的理想解决方案。  
  
## <a name="load-with-dwloader"></a>使用 dwloader 的加载  
使用[dwloader 命令行加载程序](dwloader.md)是将数据加载到 PDW 的最快方法。  
  
![加载过程](media/loading-process.png "加载过程")  
  
dwloader 加载直接到计算节点的数据，而无需通过管理节点的数据。 若要加载数据，dwloader 首先与之通信的控件节点，以获取有关计算节点的联系人信息。 dwloader 将具有每个计算节点的通信通道设置，然后将数据 256 KB 块以轮循机制方式发送到计算节点。  
  
在每个计算节点上，数据移动服务 (DMS) 接收和处理的数据块。 处理的数据包括将每一行转换为 SQL Server 本机格式，并计算分发哈希，以确定每个行所属于的计算节点。  
  
在处理这些行后, DMS 使用随机排布移动传输到正确的计算节点和 SQL Server 实例的每一行。 SQL Server 收到行时，它可以将它们根据批处理**– b** dwloader，在设置批大小参数，然后大容量加载批处理。  

## <a name="load-with-prepared-statements"></a>加载与已准备的语句

已准备的语句可用于将数据加载到分布式和复制的表。 当输入的数据与目标数据类型不匹配时，将执行隐式转换。 准备的语句的 PDW 支持的隐式转换是所支持的 SQL Server 转换的子集。 也就是说，支持转换的一个子集，但支持的转换与匹配的 SQL Server 隐式转换。 无论是否要加载的目标表定义为分布式或复制的表，隐式转换将应用 （如果需要），到目标表中存在的所有列。 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务|Description|  
|--------|---------------|  
|创建临时数据库。|[创建临时数据库](staging-database.md)|  
|加载带有 Integration Services。|[使用 Integration Services 加载](load-with-ssis.md)|  
|了解 dwloader 的类型转换。|[适用于 dwloader 的数据类型转换规则](dwloader-data-type-conversion-rules.md)|  
|加载数据时的 dwloader。|[dwloader 命令行加载程序](dwloader.md)|  
|了解有关插入的类型转换。|[使用 INSERT 加载数据](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
