---
title: 多用户环境 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- users [SQL Server], multiuser environments
- conflict resolution [Visual Database Tools]
- multiple users making database changes
- multiuser environments [Visual Database Tools]
- database modifications [SQL Server]
- version control [Visual Database Tools]
- Visual Database Tools [SQL Server], multiuser environments
ms.assetid: 330bd48c-9427-4967-b58e-b7c492d5ee36
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 41d58d45e9411caa3734f95986f3d22a7cb77529
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33049494"
---
# <a name="multiuser-environments-visual-database-tools"></a>多用户环境 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
多用户环境是指如下环境：在该环境中，其他用户可以连接到您正在使用的同一数据库，并对其进行修改。 因此，多个用户可能同时对同一数据库对象进行操作。 这样，在多用户环境中，在您进行更改时，数据库可能会受到其他用户所做更改的影响；反之亦然。  
  
在多用户环境中使用数据库的关键问题是访问权限。 您所拥有的数据库权限决定了您可以对数据库执行的操作范围。 例如，若要对数据库中的对象进行更改，您必须对该数据库具有相应的写权限。 有关数据库中的权限的详细信息，请参阅数据库文档。 有关详细信息，请参阅[权限和 Visual Database Tools (Visual Database Tools)](../../ssms/visual-db-tools/permissions-and-visual-database-tools-visual-database-tools.md)  
  
在保存对表所做的更改时，表设计器将验证自您上次保存更改以来该数据库是否已修改。 如果另一个用户已进行了更改，则通知您数据库已修改。 您可能需要协调这些更改。 有关详细信息，请参阅[协调多个用户所做的更改 (Visual Database Tools)](../../ssms/visual-db-tools/reconcile-changes-made-by-multiple-users-visual-database-tools.md)  
  
在多用户环境中，应牢记一些特殊注意事项以避免发生更改冲突。 有关详细信息，请参阅[数据库演化问题 (Visual Database Tools)](../../ssms/visual-db-tools/issues-of-database-evolution-visual-database-tools.md)。  
  
避免问题的一种方法是在进行更改时在数据库的副本（如测试数据库）中工作，然后可以创建一个更改脚本，在脱机解决冲突之后，就可以运行该脚本在原始数据库上执行这些更改。 有关详细信息，请参阅[开发、测试和生产数据库 (Visual Database Tools)](../../ssms/visual-db-tools/development-test-and-production-databases-visual-database-tools.md)  
  
