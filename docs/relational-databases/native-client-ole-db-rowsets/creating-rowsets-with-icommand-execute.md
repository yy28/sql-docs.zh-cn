---
title: 使用 ICommand::Execute 创建行集 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
- Execute method
ms.assetid: 9b530b7d-8165-49d4-a978-5ced17c6705e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a251583af46da1b264c33909dcf2a7fe75bc2c3d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86005234"
---
# <a name="creating-rowsets-with-icommandexecute"></a>使用 ICommand::Execute 创建行集
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  对于使用 ICommand::Execute 方法创建的行集，生成的行集中所需的属性可以限制命令的文本****。 这对于支持动态命令文本的使用者尤其重要。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序不能使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 游标来支持许多命令生成的多行集结果。 如果使用者请求需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 游标支持的行集，则当命令文本生成多个行集作为其结果时，将出现错误。 有关详细信息，请参阅[生成多个行集结果的命令](../../relational-databases/native-client-ole-db-commands/commands-generating-multiple-rowset-results.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标支持可滚动的 Native Client OLE DB 提供程序行集 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 针对对于由数据库的其他用户所做更改敏感的游标，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将强加相关的限制。 具体而言，就是无法对某些游标中的行进行排序，并且尝试通过包含 SQL ORDER BY 子句的命令创建行集可能会失败。 有关详细信息，请参阅[行集和 SQL Server 游标](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)。  
  
## <a name="see-also"></a>另请参阅  
 [行集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
