---
title: "测试迁移的数据库对象 (SybaseToSQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: db60668fb90aec8b093938533487a6f0ff5bdf0f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="testing-migrated-database-objects-sybasetosql"></a>测试迁移的数据库对象 (SybaseToSQL)
Microsoft SQL Server Migration Assistant for Sybase 测试人员 （SSMA 测试人员） 自动测试的数据库对象转换和所做的 SSMA 数据迁移。 已完成所有 SSMA 迁移步骤后，使用 SSMA 测试人员来验证已转换的对象相同的方式工作，所有数据已正确都传输。  
  
> [!NOTE]  
> 在 Azure 的连接的情况下，测试人员组件已被禁用。  
  
你可以使用 SSMA Tester 测试下列对象类型：  
  
-   表  
  
-   存储过程  
  
-   视图。  
  
-   独立语句。  
  
SSMA 测试人员执行为 Sybase 和 SQL Server 中的对应测试所选对象。 之后，它的结果进行比较根据以下条件：  
  
-   是表数据中的更改相同？  
  
-   有关过程和函数的输出参数的值是否相同？  
  
-   函数将返回相同的结果？  
  
-   是否在结果集相同？  
  
> [!NOTE]  
> 注意 ！ 永远不会在生产系统上使用 SSMA 测试人员。 在测试人员执行过程中修改的源架构和数据。 同时，原始状态完成还原可能无法为某些类型的测试代码。  
  
## <a name="prerequisites"></a>必要條件  
如果你想要使用 SSMA 测试人员，安装与 SSMA Sybase 扩展包**安装测试人员数据库**选项处于打开状态。  
  
此外，验证以下各项：  
  
-   Sybase OLE DB 提供程序安装在计算机上其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]运行。  
  
-   在上启用公共语言运行时 (CLR) 集成了[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库引擎。  
  
请注意 SSMA 测试人员的当前版本不支持在相同的源或目标服务器上由不同用户的并行执行。  
  
## <a name="getting-started"></a>入门  
[创建测试用例 &#40;SybaseToSQL &#41;](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>另请参阅  
[在 SQL Server &#40; 上安装 SSMA 组件SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[项目设置 &#40;转换 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  

