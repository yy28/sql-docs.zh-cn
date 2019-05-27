---
title: 0xFFFF 字符不是有效的对象标识符 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- 0xFFFF character [SQL Server]
ms.assetid: b2c9c8cf-9194-45e0-be6b-2d5ec52e8153
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c35c7c65bc312cd20c057b5e2603e7a8f77ce8c8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096922"
---
# <a name="0xffff-character-is-not-valid-as-an-object-identifier"></a>0xFFFF 字符不能用作对象标识符
  升级顾问在对象标识符中检测到 0xFFFF 字符。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本中，当数据库兼容模式设置为 90 或更高时，不能引用或重命名标识符中包含该字符的对象（如数据库、表和列）。 升级到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 时，用户数据库将保持其兼容模式。 在将数据库兼容模式更改为 90 或更高之前，请重命名包含 0xFFFF 字符的对象。  
  
 有关标识符的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“标识符”。 有关数据库兼容模式的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“sp_dbcmptlevel”。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
