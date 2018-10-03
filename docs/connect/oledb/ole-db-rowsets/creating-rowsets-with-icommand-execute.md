---
title: '使用 icommand:: Execute 创建行集 |Microsoft Docs'
description: 使用 ICommand::Execute 创建行集
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
- Execute method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 86de5c5e985d038ec4e2640fcd9d4d87b56546d5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773817"
---
# <a name="creating-rowsets-with-icommandexecute"></a>使用 ICommand::Execute 创建行集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  对于使用 ICommand::Execute 方法创建的行集，生成的行集中所需的属性可以限制命令的文本。 这对于支持动态命令文本的使用者尤其重要。  
  
 适用于 SQL Server 的 OLE DB 驱动程序无法使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 游标以支持由许多命令生成的多行集结果。 如果使用者请求需要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 游标支持的行集，则当命令文本生成多个行集作为其结果时，将出现错误。 有关详细信息，请参阅[命令生成多个行集结果](../../oledb/ole-db-commands/commands-generating-multiple-rowset-results.md)。  
  
 可滚动 OLE DB 驱动程序为 SQL Server 行集支持的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]游标。 针对对于由数据库的其他用户所做更改敏感的游标，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将强加相关的限制。 具体而言，就是无法对某些游标中的行进行排序，并且尝试通过包含 SQL ORDER BY 子句的命令创建行集可能会失败。 有关详细信息，请参阅[行集和 SQL Server 游标](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)。  
  
## <a name="see-also"></a>另请参阅  
 [行集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
