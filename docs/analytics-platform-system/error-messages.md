---
title: 错误消息-并行数据仓库 |Microsoft Docs
description: 并行数据仓库 (PDW) 错误消息报告错误和问题遇到的 PDW 组件，还可以包括 SQL Server PDW 显示的错误。 这些错误消息使用一致的语法来显示信息。 了解此语法将允许你识别和更正问题。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3ffc7a097845f4652f56d82c572ecfab868d33f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042593"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>并行数据仓库中的错误消息

并行数据仓库 (PDW) 错误消息报告错误和问题遇到的 PDW 组件，还可以包括 SQL Server PDW 显示的错误。 这些错误消息使用一致的语法来显示信息。 了解此语法将允许你识别和更正 SQL Server PDW 上的问题。  
  
## <a name="Basics"></a>错误消息基础知识  
返回的错误消息遵循相同的语法。  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
以下是每个字段的潜在值：  
  
|字段|Description|示例|  
|---------|---------------|-----------|  
|*Error_Indicator*|单词"ERROR"或其他文本提醒用户出现问题。|error|  
|*SQL_State_Code*|SQL 状态代码，根据 ODBC 规范。 驱动程序将生成相应的 SQL 状态代码消息返回应用程序的任何时间。 "Microsoft"的文本指示错误的源。|42000|  
|*Driver_Details*|依赖于驱动程序的详细信息，如用驱动程序的类型。|ODBC SQL Server 2008 R2 并行数据仓库驱动程序|  
|*QueryID*|查询的的唯一标识符。 使用此值以查找与查询处理相关的其他信息。 例如，查询执行详细信息可在管理控制台中使用查询 id。 有关详细信息，请参阅[通过使用管理控制台监视设备](monitor-the-appliance-by-using-the-admin-console.md)。<br /><br />如果 QueryID 不适用，则向用户返回文本"内部"。|QID2377|  
|*Message_String*|用户可读的错误或问题说明。 当返回 SQL Server 错误，这是 SQL Server 消息文本。|只有等于赋值可以出现在 UPDATE 语句的集合列表。|  
  
将向此类用户看到这些示例值：  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>请参阅  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[了解管理控制台警报](understanding-admin-console-alerts.md)  
  
