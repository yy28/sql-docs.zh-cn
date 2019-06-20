---
title: 测试迁移的数据库对象 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 771e9a4553679ae2afa0dd58d83b1d15ccf0fd62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62626054"
---
# <a name="testing-migrated-database-objects-oracletosql"></a>测试迁移的数据库对象 (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle 测试人员 （SSMA 测试程序） 的迁移助手自动测试的数据库对象转换和数据迁移所做的 SSMA。 在完成所有的 SSMA 迁移步骤后，使用 SSMA 测试人员验证已转换的对象相同的方式工作，所有数据已正确都传输。  
  
使用 SSMA 测试人员，你可以测试以下对象类型：  
  
-   表  
  
-   存储的过程，包括打包过程。  
  
-   用户定义函数，包括打包的函数。  
  
-   视图。  
  
-   独立的语句。  
  
SSMA 测试人员执行选定的测试上 Oracle 和中的其匹配对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 之后，它将进行比较的结果根据以下条件：  
  
-   位于所做的更改表的数据完全相同？  
  
-   过程和函数的输出参数的值是否相同？  
  
-   函数将返回相同的结果？  
  
-   是否在结果集完全相同？  
  
> [!NOTE]  
> 注意 ！ 永远不会在生产系统上使用 SSMA 测试人员。 在测试人员执行期间修改的源架构和数据。 同时，原始状态的完整还原可能对于某些类型的测试的代码不可能。  
  
## <a name="prerequisites"></a>先决条件  
如果你想要使用 SSMA 测试人员，安装 SSMA Oracle 扩展包**安装的测试人员数据库**选项已打开。  
  
若要启用的生成的表数据比较，请设置**生成的行 ID 列**选项设为**是**架构转换开始之前。 SSMA 将执行期间向所有表中添加行 ID 列**转换架构**命令。  
  
此外，验证以下各项：  
  
-   在计算机上安装 oracle 客户端工具其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]运行。  
  
-   已在上启用公共语言运行时 (CLR) 集成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎。  
  
请注意 SSMA 测试人员的当前版本不支持在相同的源或目标服务器上并行执行通过不同的用户。  
  
## <a name="getting-started"></a>入门  
[创建测试用例&#40;OracleToSQL&#41;](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>请参阅  
[SQL Server 上安装 SSMA 组件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[项目设置&#40;转换&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
