---
title: osql 不再支持 ED 和 !! 命令 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- ED command
- osql utility [SQL Server]
- '!! command'
ms.assetid: 7cc2852f-94e8-4292-9326-c3f1a1acd281
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1ad92a32c47002c8f56e56a5b3695d42d3bdd671
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012068"
---
# <a name="osql-no-longer-supports-the-ed-and--commands"></a>osql 不再支持 ED 和 !! commands
  **Osql**实用工具不支持**ED**和 **！！** 命令.  
  
## <a name="corrective-action"></a>纠正措施  
 删除对**ED**和 **！！** 的引用 命令的所有引用。  
  
 如果要使用**ED**和 **！！** 命令，请使用**sqlcmd**实用工具而不是**osql**。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
