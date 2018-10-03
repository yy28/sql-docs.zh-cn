---
title: 大的常量被类型化为大值类型在 90 或更高兼容模式下 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- binary constants
- CHARINDEX function
- constants
- character string constants
- PATINDEX function
ms.assetid: 6e309fa0-5fb9-45a1-9739-f13fae525bfe
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a12a0972ee754c8f9070122902a64c3e92eb05f2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185277"
---
# <a name="large-constants-are-typed-as-large-value-types-in-90-or-later-compatibility-modes"></a>在 90 或更高的兼容模式下，大的常量作为大值类型键入
  升级顾问检测到有大的常量存在。 大小大于 8,000 个字节的字符串常量和二进制常量在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中被视为大型对象数据类型。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本中，大型字符、Unicode 和二进制常量作为大值类型键入。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 当字符串函数（如 CHARINDEX 和 PATINDEX）与超过 8,000 个字节的字符串常量或二进制常量一起使用时，[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 将返回错误号 8116，而 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本将返回错误号 8152。  
  
 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，当字符串函数与 `text`、`ntext` 和 `image` 数据类型一起使用时，将返回错误 8116。  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本中，大的常量被分别视为 `varchar(max)`、`nvarchar(max)` 和 `varbinary(max)` 数据类型。 这些数据类型均与字符串函数兼容。  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本中，字符串函数（如 CHARINDEX 和 PATINDEX）假定包含要查找的字符序列的字符串少于 8,000 个字节。 因此，对于 CHARINDEX 和 PATINDEX，将引发错误 8152。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
