---
title: 查看筛选器信息 (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: 8d002dea-376a-452c-b3ca-3e93656ed75f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e194fa956ba1f43ae53ee37f3be15af2dfa7d4a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600395"
---
# <a name="view-filter-information-sql-server-profiler"></a>查看筛选器信息 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题介绍了如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]查看数据列的事件类筛选器。  
  
### <a name="to-view-filter-information"></a>查看筛选器信息  
  
1.  打开跟踪文件、跟踪表或 SQL 脚本，在 **“文件”** 菜单上，单击 **“属性”**。 如果要编辑跟踪模板或创建新跟踪，请跳过此步骤。  
  
2.  在“事件选择”选项卡上，右键单击要查看的筛选器的数据列名称，然后单击“编辑列筛选器”。  
  
3.  在 **“编辑筛选器”** 对话框中，展开筛选器比较运算符以查看为指定的标准分配的值。 对要查看筛选器信息的所有列，重复步骤 2 和步骤 3。  
  
> [!NOTE]  
>  具有分配值的比较运算符显示为粗体格式。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
