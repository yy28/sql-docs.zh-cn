---
title: 0xFFFF 字符对于对象标识符无效 |Microsoft Docs
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
ms.openlocfilehash: 4594c1cca0fc183100d927842cc2b533694bf90e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85046155"
---
# <a name="0xffff-character-is-not-valid-as-an-object-identifier"></a>0xFFFF 字符不能用作对象标识符
  升级顾问在对象标识符中检测到 0xFFFF 字符。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本中，当数据库兼容模式设置为 90 或更高时，不能引用或重命名标识符中包含该字符的对象（如数据库、表和列）。 升级到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 时，用户数据库将保持其兼容模式。 在将数据库兼容模式更改为 90 或更高之前，请重命名包含 0xFFFF 字符的对象。  
  
 有关标识符的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“标识符”。 有关数据库兼容模式的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“sp_dbcmptlevel”。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
