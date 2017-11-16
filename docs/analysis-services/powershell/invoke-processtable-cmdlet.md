---
title: "调用 ProcessTable cmdlet |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 865e6d06-b99a-41f3-9d6f-c3c97b529b23
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d2298c9e882f3f754b16ce33bf6bc72dfc6d80ff
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="invoke-processtable-cmdlet"></a>Invoke-ProcessTable cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  在具有特定 **RefreshType** 的 **Table** 上执行 **Process**操作。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
## <a name="syntax"></a>语法  
 `Invoke-ProcessTable [-DatabaseName] <string> [-TableName] <string> [-RefreshType] <RefreshType> {Full |     ClearValues | Calculate | DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>     [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
 `Invoke-ProcessTable -RefreshType <RefreshType> {Full | ClearValues | Calculate | DataOnly | Automatic | Add |     Defragment} -Table <Table> [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-tablename-string"></a>-TableName\<字符串 >  
 必须处理分区所属的表的名称。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|0|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-databasename-string"></a>-DatabaseName\<字符串 >  
 指定角色所属的数据库。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|0|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-servermicrosoftanalysissevicesserver"></a>服务器\<Microsoft.AnalysisSevices.Server >  
 如果你未在使用上下文的 **SQLAS** 提供程序目录，则可以选择性地指定要连接到的服务器实例。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-refreshtype-microsoftanalysisservicesrefreshtype"></a>-RefreshType \<Microsoft.AnalysisServices.RefreshType >  
 指定的表格数据库的进程类型。  有效值为 Full、ClearValues、Calculate、DataOnly、Automatic、Add 和 Defragment。 有关说明和指南，请参阅[处理数据库、表或分区 (Analysis Services)](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|1|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-credential"></a>-Credential  
 如果指定此参数，将使用传递的用户名和密码连接到 Analysis Services 实例。 如果未指定凭据，将使用正在运行该脚本的用户的默认 Windows 帐户。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-whatif"></a>-Whatif  
 包括此参数以在操作执行前获取关于操作的影响的信息。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-confirm"></a>-Confirm  
 包括此参数以在操作执行前用“是”或“否”响应来交互确认操作。  
  
|||  
|-|-|  
|必需？|false|  
|位置？||  
|默认值||  
|接受管道输入？||  
|接受通配符？|false|  
  
## <a name="example-1"></a>示例 1  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType "Full"`  
  
 此命令通过管道传入要处理的表的标识。  
  
## <a name="example-2"></a>示例 2  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType [Microsoft.AnalysisServices.Tabular.RefreshType]::Full`  
  
 此命令使用 **enum** 刷新类型处理表格元数据表。  
  
  

