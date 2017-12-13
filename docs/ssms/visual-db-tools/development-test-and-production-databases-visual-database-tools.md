---
title: "开发、测试和生产数据库 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- production databases [SQL Server]
- testing databases
- database testing [SQL Server]
ms.assetid: cb403330-8cbe-41c6-bd23-bc432d50f173
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a5742f5c71b5e68a87a7394e157ba9ecb7c07e09
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="development-test-and-production-databases-visual-database-tools"></a>开发、测试和生产数据库 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 如果有结构相同的两个数据库，则可以在一个数据库中进行更改，再将更改传播到另一个数据库。 例如，如果您有一个个人开发数据库和一个工作组范围的测试数据库，则可以修改开发数据库，再将更改传播到测试数据库。  
  
为此，需要在单个会话中完成对开发数据库的所有修改，并创建该会话的更改脚本，在以后对测试数据库运行该脚本。  
  
## <a name="see-also"></a>另请参阅  
[多用户环境 (Visual Database Tools)](../../ssms/visual-db-tools/multiuser-environments-visual-database-tools.md)  
  
