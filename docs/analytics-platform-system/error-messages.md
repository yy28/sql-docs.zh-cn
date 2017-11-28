---
title: "错误消息 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6223cba-2dec-4b8a-bc10-e2ef6a821fe0
caps.latest.revision: "9"
ms.openlocfilehash: 7c7d453bc2ac68db724734d7db7cf58e35611ba8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="error-messages"></a>错误消息
SQL Server PDW 错误消息中报告的错误和问题遇到的 SQL Server PDW 组件，还可以包括通过 SQL Server PDW 中加以表示的 SQL Server 错误。 这些错误消息使用一致的语法来显示信息。 了解此语法将允许你识别和更正 SQL Server PDW 上的问题。  
  
## <a name="Basics"></a>错误消息基础知识  
返回的错误消息遵循相同的语法。  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
这些是每个字段的可能值：  
  
|字段|Description|示例|  
|---------|---------------|-----------|  
|*Error_Indicator*|单词"ERROR"或其他警报问题用户的文本。|ERROR|  
|*SQL_State_Code*|SQL 状态代码，根据 ODBC 规范。 驱动程序会产生相应的 SQL 状态代码消息返回应用程序的任何时间。 "Microsoft"的文本指示错误的源。|42000|  
|*Driver_Details*|依赖于驱动程序的详细信息，例如使用驱动程序的类型。|ODBC SQL Server 2008 R2 并行数据仓库驱动程序|  
|*QueryID*|查询的的唯一标识符。 使用此值可找到与查询处理相关的其他信息。 例如，查询执行详细信息可在管理控制台使用查询 id。 有关详细信息，请参阅[通过使用管理控制台监视设备](monitor-the-appliance-by-using-the-admin-console.md)。<br /><br />如果 QueryID 不适用，向用户返回文本"内部"。|QID2377|  
|*Message_String*|用户可读错误或问题的说明。 返回 SQL Server 错误，这是 SQL Server 消息文本。|仅相等分配可以出现在 UPDATE 语句的设置列表。|  
  
这些示例值将向如下用户显示：  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[了解管理控制台警报](understanding-admin-console-alerts.md)  
  
