---
title: 测试迁移的数据库对象（OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 858c564c965fe7105c86a3087923887097e4ddac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266483"
---
# <a name="testing-migrated-database-objects-oracletosql"></a>测试迁移的数据库对象 (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Oracle 测试人员迁移助手（SSMA 测试人员）会自动测试数据库对象转换和 SSMA 创建的数据迁移。 完成所有 SSMA 迁移步骤后，使用 SSMA 测试人员验证转换后的对象是否以相同方式工作，并确保所有数据都已正确传输。  
  
可以通过 SSMA 测试人员测试以下对象类型：  
  
-   表  
  
-   存储过程，包括打包过程。  
  
-   用户定义的函数，包括打包的函数。  
  
-   视图。  
  
-   独立语句。  
  
SSMA 测试人员在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]执行选择用于测试的对象。 之后，它会根据以下条件比较结果：  
  
-   表数据中的更改是否相同？  
  
-   过程和函数的输出参数的值是否相同？  
  
-   函数是否返回相同的结果？  
  
-   结果集是否相同？  
  
> [!NOTE]  
> 注重! 切勿在生产系统上使用 SSMA 测试人员。 在测试执行过程中，将修改源架构和数据。 同时，对于某些类型的已测试代码，完全还原原始状态可能是不可能的。  
  
## <a name="prerequisites"></a>必备条件  
如果要使用 SSMA 测试器，请在打开 "**安装测试人员数据库**" 选项的情况下安装 SSMA Oracle 扩展包。  
  
若要对生成的表数据进行比较，请将 "**生成 ROWID 列**" 选项设置为 **"是"** ，然后将架构转换启动。 在执行**转换架构**命令的过程中，SSMA 会将 ROWID 列添加到所有表中。  
  
此外，请验证以下各项：  
  
-   Oracle 客户端工具安装在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]运行的计算机上。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎上已启用公共语言运行时（CLR）集成。  
  
请注意，当前版本的 SSMA 测试人员不支持同一源或目标服务器上的不同用户并行执行。  
  
## <a name="getting-started"></a>入门  
[&#40;OracleToSQL&#41;创建测试用例](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>另请参阅  
[在 SQL Server 上安装 SSMA 组件 &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[&#40;转换的项目设置&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
