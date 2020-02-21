---
title: 了解数据库关系图所有权
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.CannotOpenWithInvalidOwner
helpviewer_keywords:
- diagrams [SQL Server], ownership
- database diagrams [SQL Server], ownership
- owners [SQL Server], database diagrams
ms.assetid: 4a27a48e-c4ef-4017-82b8-0cac4d0bbcac
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: faebe8539698fbe605035dff737065864c70929b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75241835"
---
# <a name="understand-database-diagram-ownership-visual-database-tools"></a>了解数据库关系图所有权 (Visual Database Tools)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

若要使用数据库关系图设计器，必须先由 db_owne 角色（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的一个角色）的成员对其进行设置，以控制对关系图的访问。 每个关系图都有一个而且只有一个所有者，即创建该关系图的用户。 有关设置关系图的详细信息，请参阅[设置数据库关系图设计器(../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)。  
  
关于关系图所有权，需要记住以下几点：  
  
-   尽管任何可以访问数据库的用户都能够创建关系图，但在创建关系图之后，只有关系图的创建者和 db_owner 角色的所有成员才能查看该关系图。  
  
-   关系图的所有权只能转让给 db_owner 角色的成员。 只有当关系图的前一任拥有者已从数据库中移除时，才需要转让所有权。  
  
-   如果关系图的拥有者已从数据库中移除，该关系图将一直保留在数据库中，直到 db_owner 角色的成员试图打开该关系图。 此时，db_owner 成员可以选择接管关系图的所有权。  
  
## <a name="see-also"></a>另请参阅

[使用数据库关系图](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[设置数据库关系图设计器](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)