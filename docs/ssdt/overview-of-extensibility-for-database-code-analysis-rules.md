---
title: 数据库代码分析规则的扩展性概述 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 62f5c980-18d5-43fe-b443-c9e149d01fc7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 32462daf6d747b278be788d2364e01c2e8912114
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65101930"
---
# <a name="overview-of-extensibility-for-database-code-analysis-rules"></a>数据库代码分析规则的扩展性概述
包含 SQL Server Data Tools 的 Visual Studio 版本在数据库代码中包括要报告的有关 Transact\-SQL 设计、命名和性能警告的代码分析规则。 有关详细信息，请参阅[分析数据库代码以改进代码质量](https://msdn.microsoft.com/library/dd172133(v=vs.100).aspx)。  
  
如果内置代码分析规则未涵盖你希望包含的特定 Transact\-SQL 问题，你可以创建自定义数据库代码分析规则。 例如，你可能想要创建避免使用 WAITFOR DELAY 语句的自定义规则，如[创作 SQL Server 的自定义静态代码分析规则程序集演练](../ssdt/walkthrough-author-custom-static-code-analysis-rule-assembly.md)中所述。 若要创建自定义数据库代码分析规则，请使用 [CodeAnalysis](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.aspx) 命名空间中的类。  
  
在创建自定义代码分析规则前，你应该了解数据库代码分析规则的各种组件之间的基本体系结构。  
  
## <a name="database-code-analysis-rules-components"></a>数据库代码分析规则组件  
下图说明数据库代码分析规则组件的交互方式：  
  
![数据库代码分析规则组件](../ssdt/media/ssdt-database-code-analysis-rules-components.jpg "数据库代码分析规则组件")  
  
使用数据库代码分析规则功能时，可以通过直接运行静态代码分析（有关详细信息，请参阅[如何：分析 Transact-SQL 代码以查找缺陷](https://msdn.microsoft.com/library/dd172119(v=vs.100).aspx)）或执行生成，所有规则都根据在项目中的配置方式进行加载和使用。 有关详细信息，请参阅[如何：为数据库代码的静态分析启用和禁用特定规则](https://msdn.microsoft.com/library/dd172131(v=vs.100).aspx)。 扩展管理器还将加载你已创建和注册的任何自定义规则程序集。 有关详细信息，请参阅[如何：安装和管理功能扩展](../ssdt/how-to-install-and-manage-feature-extensions.md)。  
  
自定义代码分析规则类继承自 [SqlCodeAnalysisRule](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.sqlcodeanalysisrule.aspx)。 自定义规则类可通过其规则执行上下文访问多个有用的对象。 其中包括：  
  
-   有关规则本身的元数据。  
  
-   Dac.Model.TSqlModel 表示数据库的架构，包括所有模型元素、这些元素与其任何属性之间的关系。  
  
-   对于检查特定元素的规则，Dac.Model.TSqlObject 表示模型中的架构元素包含在上下文中。  
  
-   许多架构对象还具有 [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) 表示形式，该表示形式可通过此上下文访问 - 这是基于 AST 的元素表示形式，在尝试查看潜在语法问题（例如存在 [SelectStarExpression](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.selectstarexpression.aspx)）时可能会很有用。  
  
Dac.CodeAnalysis.SqlRuleProblem 由规则创建，用于表示任何由其发现的问题。 在创建它时，相关的 Dac.Model.TSqlObject 以及可能的 [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) 表示形式元素将传递到构造函数中，并且它们将用于确定问题在源代码文件中的位置。 在分析结束时，所有这些问题将传递到错误管理器并在错误列表中显示。  
  
## <a name="see-also"></a>另请参阅  
[扩展数据库功能](../ssdt/extending-the-database-features.md)  
  
