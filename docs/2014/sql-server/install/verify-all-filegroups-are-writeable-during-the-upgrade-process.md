---
title: 确保在升级过程中的所有文件组均可写 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- filegroups [SQL Server], writeable
- writeable filegroups [SQL Server]
ms.assetid: 2985efc1-4b14-46c3-abbd-a656b159f23c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 98633674559feead48a5b1c3cbe997863ad0f18a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62985797"
---
# <a name="verify-all-filegroups-are-writeable-during-the-upgrade-process"></a>确保升级过程中所有文件组均可写
  升级顾问检测到其中包含一个或多个只读文件组的数据库。 必须在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的所有数据库的文件组都设置为 READ_WRITE 后，才能升级。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 使用 ALTER DATABASE 将文件组设置为 READ_WRITE。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
