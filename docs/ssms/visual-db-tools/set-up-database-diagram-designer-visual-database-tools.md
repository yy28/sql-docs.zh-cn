---
title: 设置数据库关系图设计器 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.InstallSqlDiagramSupport
helpviewer_keywords:
- Database Diagram Designer
- database diagrams [SQL Server], Database Diagram Designer
- diagrams [SQL Server], Database Diagram Designer
ms.assetid: 927321ee-b459-4f5b-9719-4a7a95639143
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e8236a18c715451ecb32c5fdcb890d5bf00901c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65099901"
---
# <a name="set-up-database-diagram-designer-visual-database-tools"></a>设置数据库关系图设计器 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
若要使用数据库关系图设计器，必须首先由 **db_owner** 角色的成员对其进行设置，以控制对关系图的访问。  
  
### <a name="to-set-up-database-diagramming"></a>设置数据库关系图创建功能  
  
1.  在对象资源管理器中，展开相应的数据库节点。  
  
2.  展开该数据库连接下的“数据库关系图”节点。  
  
3.  如果希望设置数据库关系图，请在出现提示时选择“是”  。  
  
    > [!NOTE]  
    > 这将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库上创建数据库关系图表、系统存储过程和一个系统函数。  
  
4.  Visual Studio 将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上创建以下对象：  
  
    1.  sysdiagrams 表  
  
    2.  sp_alterdiagram 存储过程  
  
    3.  sp_creatediagram 存储过程  
  
    4.  sp_dropdiagram 存储过程  
  
    5.  sp_renamediagram 存储过程  
  
    6.  fn_diagramobjects 函数  
  
    7.  sp_helpdiagrams 存储过程  
  
    8.  sp_helpdiagramsdefinition 存储过程  
  
    9. sp_upgraddiagrams 存储过程  
  
## <a name="see-also"></a>另请参阅  
[了解数据库关系图所有权 (Visual Database Tools)](../../ssms/visual-db-tools/understand-database-diagram-ownership-visual-database-tools.md)  
[从以前的版本升级数据库关系图 (Visual Database Tools)](../../ssms/visual-db-tools/upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
[ALTER AUTHORIZATION (Transact-SQL)](https://msdn.microsoft.com/8c805ae2-91ed-4133-96f6-9835c908f373)  
  
