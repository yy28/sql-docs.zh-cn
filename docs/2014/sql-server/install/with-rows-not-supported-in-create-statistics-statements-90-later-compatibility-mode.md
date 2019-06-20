---
title: 使用行不支持在 CREATE STATISTICS 语句中的兼容性模式为 90 或更高版本 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e48602f61c09a8de76e2894a4fa808b2f39f4cbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090970"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>在 90 或更高的兼容模式下，CREATE STATISTICS 语句中不支持 WITH ROWS
  当运行兼容模式设置为 90 或更高的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，不支持在 CREATE STATISTICS 语句中指定 WITH ROWS。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 修改通过指定 WITH SAMPLE 包含 WITH ROWS 的 CREATE STATISTICS 语句*数*行，或使用有案可稽的语法指定符合其他选项。 有关详细信息，请参阅主题"CREATE STATISTICS (Transact SQL) 中 SQL Server 联机丛书。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
