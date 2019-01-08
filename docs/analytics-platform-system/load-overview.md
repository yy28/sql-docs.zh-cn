---
title: 将数据加载到并行数据仓库 |Microsoft Docs
description: 可以加载，也可以通过使用 Integration Services、 bcp 实用工具、 dwloader 或 SQL INSERT 语句将数据插入到 SQL Server 并行数据仓库 (PDW)。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f4551f77b1348ece34dc87dc8abeb91e27290d00
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502137"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>将数据加载到并行数据仓库
可以加载，也可以通过使用 Integration Services 将数据插入到 SQL Server 并行数据仓库 (PDW) [bcp 实用工具](../tools/bcp-utility.md)， **dwloader**命令行加载程序，或者 SQL INSERT 语句。  

## <a name="loading-environment"></a>正在加载环境  
若要加载数据，您需要一个或多个加载服务器。 可以使用自己现有的 ETL 或其他服务器，或可以购买新的服务器。 有关详细信息，请参阅[获取和配置加载服务器](acquire-and-configure-loading-server.md)。 这些说明包括[加载服务器容量规划工作表](loading-server-capacity-planning-worksheet.md)来帮助你规划用于加载的正确解决方案。  
  
## <a name="load-with-dwloader"></a>使用 dwloader 加载数据  
使用[dwloader 命令行加载程序](dwloader.md)是最快的方法将数据加载到 PDW。  
  
![加载过程](media/loading-process.png "加载过程")  
  
dwloader 加载直接向计算节点的数据而无需传递到控制节点的数据。 若要加载数据，dwloader 首先与之通信控制节点，以获取联系信息为计算节点。 dwloader 将设置与每个计算节点的通信通道，然后将 256 KB 的数据块以轮循机制的方式发送到计算节点。  
  
在每个计算节点上，数据移动服务 (DMS) 接收和处理的数据块。 处理的数据包括的每一行转换为 SQL Server 本机格式，并计算分发哈希值来确定每个行所属的计算节点。  
  
在处理行之后, DMS 使用 shuffle 移动将传输到正确的计算节点和 SQL Server 实例的每个行。 由于 SQL Server 收到的行，它根据其批处理 **-b**中 dwloader，设置批大小参数，然后大容量加载批。  

## <a name="load-with-prepared-statements"></a>使用预定义语句加载数据

可以使用预定义的语句将数据加载到分布式和复制表。 当输入的数据与目标数据类型不匹配时，将执行的隐式转换。 隐式转换受 PDW 准备的语句是所支持的 SQL Server 转换的子集。 即，支持仅子网的转换，但支持的转换与匹配的 SQL Server 隐式转换。 而不考虑是否要加载的目标表定义为分布式或复制表，隐式转换将应用 （如果需要），到目标表中存在的所有列。 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务|Description|  
|--------|---------------|  
|创建临时数据库。|[创建临时数据库](staging-database.md)|  
|加载带有 Integration Services。|[使用 Integration Services 加载](load-with-ssis.md)|  
|了解适用于 dwloader 的类型转换。|[适用于 dwloader 的数据类型转换规则](dwloader-data-type-conversion-rules.md)|  
|加载与 dwloader 的数据。|[dwloader 命令行加载程序](dwloader.md)|  
|了解插入的类型转换。|[使用 INSERT 加载数据](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
