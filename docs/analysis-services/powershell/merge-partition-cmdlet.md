---
title: 合并分区 cmdlet |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e5ca667b3172de982ea98a6d13c1fe6f810377b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="merge-partition-cmdlet"></a>Merge-Partition cmdlet
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  将一个或多个源分区的数据合并到目标分区中，然后删除源分区。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
## <a name="syntax"></a>语法  
 `Merge-ASDatabase [-Name] <string> [-SourcePartitions] <System.String[]> -Database <string> -Cube <string> -MeasureGroup <string> [-Server <string>] [-Credentials <PSCredential>] [<CommonParameters>]`  
  
 `Merge-ASDatabase -TargetPartition <Microsoft.AnalysisServices.Partition> [-SourcePartitions] <System.String[]> -Database <string> -Cube <string> -MeasureGroup <string> [-Server <string>] [-Credentials <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Merge-Partition cmdlet 将一个或多个源分区的数据合并到目标分区中，然后删除源分区。 只有符合下列所有条件的分区才能合并：  
  
-   这些分区位于同一度量值组中。  
  
-   这些分区位于同一台计算机中。  
  
-   这些分区共享相同的存储模式（针对多维数据库的 MOLAP、HOLAP 和 ROLAP）。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-name-string"></a>-Name \<string>  
 指定源分区数据将合并到其中的目标分区。 此分区必须已存在。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|0|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-sourcepartition-string"></a>-SourcePartition\<字符串 >  
 指定将合并到目标分区中的源分区。 可以创建要合并的分区的以逗号分隔的列表。 使用变量存储该列表。 例如，$Sources=“Sales_2008”、“Sales_2009”、“Sales_2010”。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|1|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-database-string"></a>-数据库\<字符串 >  
 指定分区属于的数据库。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-cube-string"></a>-多维数据集\<字符串 >  
 指定分区属于的多维数据集。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-measuregroup-string"></a>-MeasureGroup\<字符串 >  
 指定分区所属的度量值组。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-server-string"></a>-Server \<string>  
 指定 cmdlet 要连接和执行的 Analysis Services 实例。 如果未提供服务器名称，将连接到本地主机。 对于默认实例，仅指定服务器名称。 对于命名实例，请使用格式 servername\instancename。 对于 HTTP 连接，请使用格式 http[s]://server[:port]/virtualdirectory/msmdpump.dll。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|localhost|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 对于您已经配置了 HTTP 访问的实例，此参数用于在使用 HTTP 连接到 Analysis Service 实例时传入用户名和密码。 有关详细信息，请参阅[到在 Internet Information Services 上的 Analysis Services 配置 HTTP 访问&#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)为 HTTP 连接。  
  
 如果指定此参数，将使用用户名和密码连接到指定的 Analysis Server 实例。 如果未指定凭据，将使用正在运行该工具的用户的默认 Windows 帐户。  
  
 若要使用此参数，请首先使用 Get-Credential 创建一个 PSCredential 对象，以便指定用户名和密码（例如， `$Cred=Get-Credential “adventure-works\bobh”`。 然后，可以将此对象传送到 –Credential 参数 `(-Credential:$Cred`)。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|True (ByValue)|  
|接受通配符？|false|  
  
### <a name="-targetpartition-microsoftanalysisservicespartition"></a>-TargetPartition \<Microsoft.AnalysisServices.Partition >  
 指定源分区数据将合并到其中的目标分区。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|true|  
|接受通配符？|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 此 cmdlet 支持以下常用参数：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 有关详细信息，请参阅 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>输入和输出  
 输入类型是可以传送到 cmdlet 的对象的类型。 返回类型是 cmdlet 所返回的对象的类型。  
  
|||  
|-|-|  
|输入|System.string|  
|输出|InclusionThresholdSetting|  
  
## <a name="example-1"></a>示例 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\sales orders\partitions> $Source=”Total_Orders_2001”, “Total_Orders_2002”, “Total_Orders_2003”` `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\sales orders\partitions> Merge-Partition –Name “Total_Orders_2004” –SourcePartitions:$Source –database “AWTEST” –cube “Adventure Works” –MeasureGroup “Sales Orders”`  
  
 此命令将 2001、2002 和 2003 年的分区合并到 2004 年的分区中，然后删除前几年的分区。  
  

  
