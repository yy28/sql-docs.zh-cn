---
title: 测试迁移的数据库对象 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e29fac8b9cdb955ddaff6643eacae352e9c39bf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63214318"
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>测试迁移的数据库对象 (SybaseToSQL)
Microsoft SQL Server Migration Assistant for Sybase 测试人员 （SSMA 测试程序） 自动测试的数据库对象转换和数据迁移所做的 SSMA。 在完成所有的 SSMA 迁移步骤后，使用 SSMA 测试人员验证已转换的对象相同的方式工作，所有数据已正确都传输。  
  
> [!NOTE]  
> 在 Azure 连接性的情况下，测试人员组件已被禁用。  
  
使用 SSMA 测试人员，你可以测试以下对象类型：  
  
-   表  
  
-   存储过程  
  
-   视图。  
  
-   独立的语句。  
  
SSMA 测试人员执行测试上 Sybase 和其对应的 SQL Server 中为所选对象。 之后，它将进行比较的结果根据以下条件：  
  
-   位于所做的更改表的数据完全相同？  
  
-   过程和函数的输出参数的值是否相同？  
  
-   函数将返回相同的结果？  
  
-   是否在结果集完全相同？  
  
> [!NOTE]  
> 注意 ！ 永远不会在生产系统上使用 SSMA 测试人员。 在测试人员执行期间修改的源架构和数据。 同时，原始状态的完整还原可能对于某些类型的测试的代码不可能。  
  
## <a name="prerequisites"></a>先决条件  
如果你想要使用 SSMA 测试人员，安装 SSMA Sybase 扩展包**安装的测试人员数据库**选项已打开。  
  
此外，验证以下各项：  
  
-   Sybase OLE DB 访问接口安装在计算机上其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]运行。  
  
-   已在上启用公共语言运行时 (CLR) 集成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎。  
  
请注意 SSMA 测试人员的当前版本不支持在相同的源或目标服务器上并行执行通过不同的用户。  
  
## <a name="getting-started"></a>入门  
[创建测试用例&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>请参阅  
[SQL Server 上安装 SSMA 组件&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[项目设置&#40;转换&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
