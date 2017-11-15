---
title: "查看收集组日志 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], viewing
- collection sets [SQL Server], viewing logs
ms.assetid: 428908b8-fb6a-4d0c-8339-ee133e23aad2
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 454f913984690220807497b608e6f81114f981c5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="view-collection-set-logs-sql-server-management-studio"></a>查看收集日志 (SQL Server Management Studio)
  您可以从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]查看所有收集组日志或单个收集组日志。  
  
### <a name="to-view-collection-set-logs"></a>查看收集组日志  
  
1.  在对象资源管理器中，展开 **“管理”** 文件夹。  
  
2.  右键单击“数据收集”，然后单击“查看日志”。  
  
     将会打开“日志文件查看器”。每个收集组的所有日志文件都会在该查看器的“数据收集”节点下列出并预先选中。  
  
3.  若要查看特定的收集组日志，请清除您不希望查看其日志的各收集组旁边的复选框。 针对该收集组的日志信息将会从 **“日志文件查看器”** 的详细信息窗格中删除。  
  
### <a name="to-view-a-specific-collection-set-log-file"></a>查看特定的收集组日志文件  
  
1.  在对象资源管理器中，展开 **“管理”** 文件夹，然后展开 **“数据收集”**。  
  
2.  右键单击要查看其日志的收集组，然后单击“查看日志”。  
  
     将打开 **“日志文件查看器”** ，其中仅显示所选收集组的日志文件。  
  
## <a name="see-also"></a>另请参阅  
 [“数据收集”](../../relational-databases/data-collection/data-collection.md)   
 [管理数据收集](../../relational-databases/data-collection/manage-data-collection.md)  
  
  
