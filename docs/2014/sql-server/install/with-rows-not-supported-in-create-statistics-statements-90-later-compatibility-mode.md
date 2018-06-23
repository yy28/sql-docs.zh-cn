---
title: 包含行中不支持 CREATE STATISTICS 语句中的兼容性模式 90 或更高版本 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9d509352d99cab9359e7ea222f5fb2d5d7e28075
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123530"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>在 90 或更高的兼容模式下，CREATE STATISTICS 语句中不支持 WITH ROWS
  当运行兼容模式设置为 90 或更高的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，不支持在 CREATE STATISTICS 语句中指定 WITH ROWS。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 修改通过指定 WITH SAMPLE 包含 WITH ROWS 的 CREATE STATISTICS 语句*数*行，或使用有案可稽的语法指定符合其他选项。 有关详细信息，请参阅主题"CREATE STATISTICS (Transact SQL) 中 SQL Server 联机丛书。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
