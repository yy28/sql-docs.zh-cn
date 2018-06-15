---
title: 在对象资源管理器中隐藏系统对象 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hiding system objects
- system objects [SQL Server]
- objects [SQL Server], hiding
- Object Explorer, hiding objects
ms.assetid: c01d8804-838c-4f75-b78c-80e41e4fffdc
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 106c73db70f12616f85920067863a25c529810a2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33040504"
---
# <a name="hide-system-objects-in-object-explorer"></a>在对象资源管理器中隐藏系统对象
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]中的对象资源管理器中隐藏系统对象。 对象资源管理器的“数据库”节点包含系统对象，如系统数据库。 使用“工具”/“选项”页可以隐藏系统对象。 某些系统对象（如系统函数和系统数据类型）并不受此设置的影响。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-hide-system-objects-in-object-explorer"></a>在对象资源管理器中隐藏系统对象  
  
1.  在“工具”  菜单上，单击“选项” 。  
  
2.  在“环境”/“启动”页上，选中“在对象资源管理器中隐藏系统对象”，再单击“确定”。  
  
3.  在“SQL Server Management Studio”对话框中，单击“确定”，确认必须重启 SQL Server Management Studio，以便此更改生效。  
  
4.  关闭并重新打开 SQL Server Management Studio。  
  
