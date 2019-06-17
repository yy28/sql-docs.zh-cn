---
title: 在 SQL Server 2005 中，SERVERPROPERTY 返回 LCID 属性的正确结果 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SERVERPROPERTY function
ms.assetid: 833a2fc9-b480-4697-aa7b-9677e78ee0b4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 24bb31759ba520f26b8e9af3a6533d8f0feebbe0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092241"
---
# <a name="serverproperty-returns-correct-result-for-lcid-property-in-sql-server-2005"></a>在 SQL Server 2005 中，SERVERPROPERTY 返回 LCID 属性的正确结果
  当在使用二进制排序规则的服务器上运行 SERVERPROPERTY('LCID') 时，该函数返回与服务器的排序规则相对应的 Windows 区域设置标识符 (LCID)。  
  
> [!NOTE]  
>  对于包含对 SERVERPROPERTY ('LCID') 的引用并且在其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上运行的批处理文件和跟踪文件，只有其他实例的排序规则与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]当前实例的排序规则相同时，升级顾问才会检测此行为更改。  
  
## <a name="corrective-action"></a>纠正措施  
 修改应用程序，使 SERVERPROPERTY('LCID') 返回与服务器排序规则对应的 Windows LCID。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
