---
title: 错误消息
description: 并行数据仓库（PDW）错误消息会报告 PDW 组件遇到的错误和问题，还可能包括通过 PDW 出现 SQL Server 错误。 这些错误消息使用一致的语法来显示信息。 了解此语法将允许您确定并更正问题。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2d89e80a89df53e85ef8d2bf53c369d9e4dc0d49
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401165"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>并行数据仓库中的错误消息

并行数据仓库（PDW）错误消息会报告 PDW 组件遇到的错误和问题，还可能包括通过 PDW 出现 SQL Server 错误。 这些错误消息使用一致的语法来显示信息。 了解此语法将允许您确定并更正 SQL Server PDW 上的问题。  
  
## <a name="Basics"></a>错误消息基础  
返回的错误消息遵循相同的语法。  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
以下是每个字段的可能值：  
  
|字段|说明|示例|  
|---------|---------------|-----------|  
|*Error_Indicator*|单词 "错误" 或其他文本会提醒用户出现问题。|ERROR|  
|*SQL_State_Code*|SQL 状态代码（按照 ODBC 规范）。 驱动程序在将消息返回到应用程序时，会生成相应的 SQL 状态代码。 文本 "Microsoft" 指示错误的源。|42000|  
|*Driver_Details*|与驱动程序相关的详细信息，如使用的驱动程序类型。|ODBC SQL Server 2008 R2 并行数据仓库驱动程序|  
|*QueryID*|查询的唯一标识符。 使用此值可查找与查询处理相关的其他信息。 例如，可以在管理控制台中使用查询 ID 查找查询执行详细信息。 有关详细信息，请参阅[使用管理控制台监视设备](monitor-the-appliance-by-using-the-admin-console.md)。<br /><br />如果 QueryID 不适用，则向用户返回文本 "Internal"。|QID2377|  
|*Message_String*|用户可读的错误或问题的说明。 返回 SQL Server 错误时，这是 SQL Server 消息文本。|UPDATE 语句的设置列表中只能出现等于赋值。|  
  
这些示例值会显示给用户，如下所示：  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[了解管理控制台警报](understanding-admin-console-alerts.md)  
  
