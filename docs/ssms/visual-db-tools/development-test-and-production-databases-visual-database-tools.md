---
title: 开发、测试和生产数据库 | Microsoft Docs
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
- production databases [SQL Server]
- testing databases
- database testing [SQL Server]
ms.assetid: cb403330-8cbe-41c6-bd23-bc432d50f173
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 072f7d671f12335928984d4cebfe57f5bbfe6468
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="development-test-and-production-databases-visual-database-tools"></a>开发、测试和生产数据库 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
如果您有结构相同的两个数据库，则可以在一个数据库中进行更改，再将更改传播到另一个数据库。 例如，如果您有一个个人开发数据库和一个工作组范围的测试数据库，则可以修改开发数据库，再将更改传播到测试数据库。  
  
为此，需要在单个会话中完成对开发数据库的所有修改，并创建该会话的更改脚本，在以后对测试数据库运行该脚本。  
  
## <a name="see-also"></a>另请参阅  
[多用户环境 (Visual Database Tools)](../../ssms/visual-db-tools/multiuser-environments-visual-database-tools.md)  
  
