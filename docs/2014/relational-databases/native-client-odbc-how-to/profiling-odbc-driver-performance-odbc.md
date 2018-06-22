---
title: 分析 ODBC 驱动程序性能操作指南主题 (ODBC) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0e6d7aed-28d2-419e-be6a-f60d3729bfd0
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4fcd58b3c21b113a41c1e869fb1d22ed6c456c57
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015215"
---
# <a name="profiling-odbc-driver-performance-how-to-topics-odbc"></a>对 ODBC 驱动程序性能进行事件探查的操作指南主题 (ODBC)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驱动程序有两个特定于驱动程序的选项，用于对驱动程序的性能进行事件探查。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驱动程序可以在文件中记录性能统计信息。 日志文件是以制表符分隔的文件，它可以在支持以制表符分隔的文件（比如 Microsoft Excel）的任何电子表格中进行分析。  
  
 驱动程序也可以记录长时间运行的查询（在指定长度的时间内未从服务器获得响应的查询）。 这些查询可以随后由程序员和数据库管理员进行分析。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [配置文件驱动程序的性能数据&#40;ODBC&#41;](profiling-odbc-driver-performance-data.md)  
  
-   [记录长时间运行的查询&#40;ODBC&#41;](profiling-odbc-driver-performance-data-log-long-running-queries.md)  
  
## <a name="see-also"></a>请参阅  
 [ODBC 操作指南主题](odbc-how-to-topics.md)  
  
  