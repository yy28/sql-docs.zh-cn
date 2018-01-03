---
title: "测试迁移的数据库对象 (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 0b20c1f5d47388a92e92402faa9017dc6b042a1c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="testing-migrated-database-objects-oracletosql"></a>测试迁移的数据库对象 (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Oracle 测试人员 （SSMA 测试人员） 的迁移助手将自动测试数据库对象转换和所做的 SSMA 数据迁移。 已完成所有 SSMA 迁移步骤后，使用 SSMA 测试人员来验证已转换的对象相同的方式工作，所有数据已正确都传输。  
  
你可以使用 SSMA Tester 测试下列对象类型：  
  
-   表  
  
-   存储的过程，包括打包过程。  
  
-   用户定义函数，包括打包的函数。  
  
-   视图。  
  
-   独立语句。  
  
SSMA 测试人员执行测试 Oracle 和中的对应项为所选对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 之后，它的结果进行比较根据以下条件：  
  
-   是表数据中的更改相同？  
  
-   有关过程和函数的输出参数的值是否相同？  
  
-   函数将返回相同的结果？  
  
-   是否在结果集相同？  
  
> [!NOTE]  
> 注意 ！ 永远不会在生产系统上使用 SSMA 测试人员。 在测试人员执行过程中修改的源架构和数据。 同时，原始状态完成还原可能无法为某些类型的测试代码。  
  
## <a name="prerequisites"></a>必备条件  
如果你想要使用 SSMA 测试人员，安装与 SSMA Oracle 扩展包**安装测试人员数据库**选项处于打开状态。  
  
要使生成的表数据的比较，设置**生成 ROWID 列**选项设为**是**架构转换开始之前。 SSMA 将执行期间向所有表中添加 ROWID 列**转换架构**命令。  
  
此外，验证以下各项：  
  
-   在计算机上安装 oracle 客户端工具其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]运行。  
  
-   在上启用公共语言运行时 (CLR) 集成了[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库引擎。  
  
请注意 SSMA 测试人员的当前版本不支持在相同的源或目标服务器上由不同用户的并行执行。  
  
## <a name="getting-started"></a>入门  
[创建测试用例 &#40; OracleToSQL &#41;](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>另请参阅  
[在 SQL Server &#40; OracleToSQL &#41; 上安装 SSMA 组件](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[项目设置 &#40;转换 &#41;&#40; OracleToSQL &#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
