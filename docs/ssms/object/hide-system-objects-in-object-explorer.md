---
title: "在对象资源管理器中隐藏系统对象 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-objects
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hiding system objects
- system objects [SQL Server]
- objects [SQL Server], hiding
- Object Explorer, hiding objects
ms.assetid: c01d8804-838c-4f75-b78c-80e41e4fffdc
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 73a97e78886138d5461dcff102750e255f752037
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="hide-system-objects-in-object-explorer"></a>在对象资源管理器中隐藏系统对象
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中的对象资源管理器中隐藏系统对象。 对象资源管理器的“数据库”节点包含系统对象，如系统数据库。 使用“工具”/“选项”页可以隐藏系统对象。 某些系统对象（如系统函数和系统数据类型）并不受此设置的影响。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-hide-system-objects-in-object-explorer"></a>在对象资源管理器中隐藏系统对象  
  
1.  在“工具”  菜单上，单击“选项” 。  
  
2.  在“环境”/“启动”页上，选中“在对象资源管理器中隐藏系统对象”，再单击“确定”。  
  
3.  在“SQL Server Management Studio”对话框中，单击“确定”，确认必须重启 SQL Server Management Studio，以便此更改生效。  
  
4.  关闭并重新打开 SQL Server Management Studio。  
  
