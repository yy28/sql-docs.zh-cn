---
title: DAC 对 SQL Server 对象和版本的支持 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- data-tier application [SQL Server], supported objects
- objects [SQL Server], data-tier applications
ms.assetid: b1b78ded-16c0-4d69-8657-ec57925e68fd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2c3cda314aacc2cc1f589fc762a21be411e16016
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62918432"
---
# <a name="dac-support-for-sql-server-objects-and-versions"></a>对 SQL Server 对象和版本的 DAC 支持
  数据层应用程序 (DAC) 支持最常用的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 对象。  
  
 **本主题内容**  
  
-   [支持的 SQL Server 对象](#SupportedObjects)  
  
-   [各 SQL Server 版本的数据层应用程序支持](#SupportByVersion)  
  
-   [数据部署限制](#DeploymentLimitations)  
  
-   [有关部署操作的其他注意事项](#Considerations)  
  
##  <a name="SupportedObjects"></a> 支持的 SQL Server 对象  
 当编写或编辑数据层应用程序时，只能在其中指定支持的对象。 对于包含在 DAC 中不支持的对象的现有数据库，无法从其提取、注册或导入 DAC。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持 DAC 中的以下对象。  
  
|||  
|-|-|  
|DATABASE ROLE|函数：内联表值|  
|函数：多语句表值|函数：Scalar|  
|索引：聚集|索引：非群集|  
|索引：特殊|索引：唯一|  
|Login|权限|  
|角色成员资格|SCHEMA|  
|统计信息|存储过程：Transact-SQL|  
|同义词|表：检查约束|  
|表：排序规则|表：列，包括计算列|  
|表：约束，默认值|表：约束，外键|  
|表：约束，索引|表：约束，主键|  
|表：约束，唯一|触发器：DML|  
|类型：HIERARCHYID、GEOMETRY、GEOGRAPHY|类型：用户定义数据类型|  
|类型：用户定义表类型|User|  
|VIEW||  
  
##  <a name="SupportByVersion"></a> 各 SQL Server 版本的数据层应用程序支持  
 各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本具有针对 DAC 操作的不同级别的支持。 某一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支持的所有 DAC 操作均受到该版本的所有次级版本的支持。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例支持以下 DAC 操作：  
  
-   所有支持的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本都支持导出和提取。  
  
-   [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 和所有版本的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]都支持所有操作。  
  
-   在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Service Pack 2 (SP2) 或更高版本以及 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 或更高版本上支持所有操作。  
  
 DAC Framework 包含用于生成和处理 DAC 包和导出文件的客户端工具。 以下产品包括 DAC Framework  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 包括 DAC Framework 3.0，它支持所有 DAC 操作。  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 和 Visual Studio 2010 SP1 包括了 DAC Framework 1.1，它支持除了导出和导入之外的所有 DAC 操作。  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 和 Visual Studio 2010 包括了 DAC Framework 1.0，它支持除了导出、导入和就地升级之外的所有 DAC 操作。  
  
-   来自 SQL Server 或 Visual Studio 的早期版本的客户端工具不支持 DAC 操作。  
  
 使用某一 DAC Framework 版本生成的 DAC 包或导出文件无法由早期版本的 DAC Framework 处理。 例如，使用 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 客户端工具提取的 DAC 包无法使用 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 客户端工具进行部署。  
  
 使用某一 DAC Framework 版本生成的 DAC 包或导出文件可由任何更高版本的 DAC Framework 处理。 例如，使用 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 客户端工具提取的 DAC 包可使用 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 或更高版本客户端工具进行部署。  
  
##  <a name="DeploymentLimitations"></a> 数据部署限制  
 请注意 SQL Server 2012 SP1 中 DAC Framework 数据部署引擎的以下这些保真度限制。 这些限制适用于以下 DAC Framework 操作：部署或发布 .dacpac 文件，以及导入 .bacpac 文件。  
  
1.  sql_variant 列中特定条件和基类型的元数据丢失。 在受影响的情况下，将会看到一条包含以下消息的警告：**由 DAC Framework 部署时不保留 sql_variant 列中使用的特定数据类型的特定属性。**  
  
    -   MONEY、SMALLMONEY、NUMERIC、DECIMAL 基类型：不保留精度。  
  
        -   精度为 38 的 DECIMAL/NUMERIC 基类型：“TotalBytes”sql_variant 元数据始终设置为 21。  
  
    -   所有文本基类型：对所有文本应用数据库的默认排序规则。  
  
    -   BINARY 基类型：不保留最大长度属性。  
  
    -   TIME、DATETIMEOFFSET 基类型：精度始终设置为 7。  
  
2.  sql_variant 列中的数据丢失。 在受影响的情况下，将会看到一条包含以下消息的警告：**当 DAC Framework 部署小数位数超过 3 的 sql_variant DATETIME2 中的值时，将会发生数据丢失。部署期间，将 DATETIME2 值限定为等于 3 的小数位数。**  
  
    -   小数位数大于 3 的 DATETIME2 基类型：小数位数限定为等于 3。  
  
3.  针对 sql_variant 列中以下条件的部署操作失败。 在受影响的情况下，将会看到一条包含以下消息的对话框：**由于 DAC Framework 中的数据限制，操作失败。**  
  
    -   DATETIME2、SMALLDATETIME 和 DATE 基类型：值超出 DATETIME 范围 - 例如，年份小于 1753。  
  
    -   DECIMAL、NUMERIC 基类型：值的精度大于 28。  
  
##  <a name="Considerations"></a> 有关部署操作的其他注意事项  
 请注意以下有关 DAC Framework 数据部署操作的注意事项：  
  
-   **提取/导出** - 对于使用 DAC Framework 从数据库创建包的操作（例如，提取 .dacpac 文件，导出 .bacpac 文件），这些限制不适用。 该包中的数据是源数据库中数据的完全保真表示形式。 如果该包中存在其中任意条件，则提取/导出日志将包含通过上述消息所提供问题的摘要。 这将向用户警告他们所创建的包存在潜在数据部署问题。 用户还将在日志中看到以下摘要消息：**这些限制不影响 DAC Framework 创建的 DAC 包中存储的数据类型和值的保真度；它们只适用于因将 DAC 包部署到数据库而产生的数据类型和值。有关受影响的数据以及如何解决此限制的详细信息，请参阅**[此主题](https://go.microsoft.com/fwlink/?LinkId=267086)。  
  
-   **部署/发布/导入** - 对于使用 DAC Framework 将包部署到数据库的操作（例如，部署或发布 .dacpac 文件，以及导入 .bacpac 文件），这些限制适用。 目标数据库中生成的数据不能包含包中数据的完全保真表示形式。 部署/导入日志将对出现问题的每个实例都显示一条上述消息。 操作将因错误而被阻止 - 请参阅上述类别 3 - 但将继续显示其他警告。  
  
     有关此情况下受影响的数据以及如何在部署/发布/导入操作中绕开此限制的详细信息，请参阅 [此主题](https://go.microsoft.com/fwlink/?LinkId=267087)。  
  
-   **解决方法** - 提取和导出操作将完全保真的 BCP 数据文件写入 .dacpac 或 .bacpac 文件。 若要避免限制，请使用 SQL Server BCP.exe 命令行实用工具将完全保真数据从 DAC 包部署到目标数据库。  
  
## <a name="see-also"></a>请参阅  
 [数据层应用程序](data-tier-applications.md)  
  
  
