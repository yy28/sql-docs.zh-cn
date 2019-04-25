---
title: 有关在 90 或更高兼容模式下的视图中不允许浏览 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], FOR BROWSE clause
- FOR BROWSE clause
ms.assetid: 8f49b1c1-d877-4c46-b988-f8cdd8ac0925
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 360208afdc5dddbd1795ba7aa47c2c05b7006b64
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62506919"
---
# <a name="for-browse-is-not-allowed-in-views-in-90-or-later-compatibility-modes"></a>在 90 或更高的兼容模式下，视图中不允许 FOR BROWSE
  升级顾问检测到视图中使用了 FOR BROWSE 子句。 当数据库兼容性模式设置为 80 时，视图中允许(并忽略) FOR BROWSE 语句。 当数据库兼容模式设置为 90 或更高时，视图中不允许使用 FOR BROWSE 子句。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 升级时，用户数据库将保持其兼容模式。 将数据库兼容模式更改为 90 或更高的兼容模式之前，请从视图定义中删除 FOR BROWSE 子句。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“sp_dbcmptlevel”。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
