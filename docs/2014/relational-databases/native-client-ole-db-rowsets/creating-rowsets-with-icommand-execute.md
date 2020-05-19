---
title: 使用 ICommand::Execute 创建行集 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
- Execute method
ms.assetid: 9b530b7d-8165-49d4-a978-5ced17c6705e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 50981c958e65dcb26f78980d91efae672ff6d39f
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82694810"
---
# <a name="creating-rowsets-with-icommandexecute"></a>使用 ICommand::Execute 创建行集
  对于使用 ICommand::Execute 方法创建的行集，生成的行集中所需的属性可以限制命令的文本****。 这对于支持动态命令文本的使用者尤其重要。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序不能使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 游标来支持许多命令生成的多行集结果。 如果使用者请求需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 游标支持的行集，则当命令文本生成多个行集作为其结果时，将出现错误。 有关详细信息，请参阅[生成多个行集结果的命令](../native-client-ole-db-commands/commands-generating-multiple-rowset-results.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标支持可滚动的 Native Client OLE DB 提供程序行集 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 针对对于由数据库的其他用户所做更改敏感的游标，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将强加相关的限制。 具体而言，就是无法对某些游标中的行进行排序，并且尝试通过包含 SQL ORDER BY 子句的命令创建行集可能会失败。 有关详细信息，请参阅[行集和 SQL Server 游标](rowsets-and-sql-server-cursors.md)。  
  
## <a name="see-also"></a>另请参阅  
 [行集](rowsets.md)  
  
  
