---
title: "使用 ICommand::Execute 创建行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
- Execute method
ms.assetid: 9b530b7d-8165-49d4-a978-5ced17c6705e
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 81b961bbaed06f776b8f3361ea6491d1cd6b8c6c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="creating-rowsets-with-icommandexecute"></a>使用 ICommand::Execute 创建行集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  通过使用创建的行集**ICommand::Execute**方法中生成的行集, 所需的属性可以将限制命令的文本。 这对于支持动态命令文本的使用者尤其重要。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不能使用[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标以支持通过很多命令生成的行集的多个结果。 如果使用者请求需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 游标支持的行集，则当命令文本生成多个行集作为其结果时，将出现错误。 有关详细信息，请参阅[命令生成多个行集结果](../../relational-databases/native-client-ole-db-commands/commands-generating-multiple-rowset-results.md)。  
  
 可滚动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序行集支持的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标。 针对对于由数据库的其他用户所做更改敏感的游标，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将强加相关的限制。 具体而言，就是无法对某些游标中的行进行排序，并且尝试通过包含 SQL ORDER BY 子句的命令创建行集可能会失败。 有关详细信息，请参阅[行集和 SQL Server 游标](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)。  
  
## <a name="see-also"></a>另请参阅  
 [行集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
