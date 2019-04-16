---
title: INFORMATION_SCHEMA。在数据库中，架构返回的架构名称不数据库实例中 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
ms.assetid: 4337b643-910d-47d7-bea8-f4052066b9a2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c13ce7b709356e958d50271ea928f9b8464fb986
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582306"
---
# <a name="informationschemaschemata-returns-schema-names-in-a-database-not-databases-in-an-instance"></a>INFORMATION_SCHEMA.SCHEMATA 返回数据库中的架构名称，而不是实例中的数据库
  升级顾问检测到了引用 INFORMATION_SCHEMA.SCHEMATA 视图的语句。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本中，此视图返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的所有数据库。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本中，该视图返回数据库中的所有架构。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本中，INFORMATION_SCHEMA.SCHEMATA 视图返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的所有数据库。 现在，该视图返回数据库中的所有架构，这是符合 SQL 标准的。  
  
## <a name="corrective-action"></a>纠正措施  
 应用程序修改为引用**sys.databases**目录视图以返回所有数据库的实例中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
