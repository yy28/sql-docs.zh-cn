---
title: 在对象资源管理器中隐藏系统对象
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- hiding system objects
- system objects [SQL Server]
- objects [SQL Server], hiding
- Object Explorer, hiding objects
ms.assetid: c01d8804-838c-4f75-b78c-80e41e4fffdc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 05864efb35ecd5fcd49e8f8b90cd8093984a9f78
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001958"
---
# <a name="hide-system-objects-in-object-explorer"></a>在对象资源管理器中隐藏系统对象
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的对象资源管理器中隐藏系统对象。 对象资源管理器的“数据库”  节点包含系统对象，如系统数据库。 使用“工具”  /“选项”  页可以隐藏系统对象。 某些系统对象（如系统函数和系统数据类型）并不受此设置的影响。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-hide-system-objects-in-object-explorer"></a>在对象资源管理器中隐藏系统对象  
  
1.  在“工具”  菜单上，单击“选项”  。  
  
2.  在“环境”/“启动”  页上，选中“在对象资源管理器中隐藏系统对象”  ，再单击“确定”  。  
  
3.  在“SQL Server Management Studio”  对话框中，单击“确定”  ，确认必须重启 SQL Server Management Studio，以便此更改生效。  
  
4.  关闭并重新打开 SQL Server Management Studio。  
  
