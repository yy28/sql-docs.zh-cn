---
title: 设置项目选项 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Configuration Options and Modes
ms.assetid: a324d07d-cfdf-43bd-98a0-acf332c5a4db
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 7760a893082f7b4a8899e00480fc43914b1c12ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62625911"
---
# <a name="setting-project-options-oracletosql"></a>设置项目选项 (OracleToSQL)
对于每个 SSMA 项目可以设置项目级别选项。 这些选项用于指定对象转换、 对象加载、 用户界面和数据迁移设置。 在转换到的对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，验证配置选项是否适用于该项目。  
  
SSMA 允许你配置的所有项目的默认选项。 这些选项不适用于您创建任何新项目。 然后可以自定义每个项目的选项。  
  
## <a name="configuration-options-and-modes"></a>配置选项和模式  
SSMA 具有五个集的项目设置：  
  
-   项目信息  
  
-   常规 （转换、 迁移，加载对象）  
  
-   Synchronization  
  
-   GUI  
  
-   类型映射  
  
它还具有四种模式来配置这些设置：  
  
-   默认  
  
-   乐观  
  
-   完全  
  
-   自定义  
  
建议大多数用户使用的默认模式。 乐观模式使多个当前 Oracle 语法，并易于阅读。 但是，保留当前的语法可能不会准确。 如果 Oracle 语法必须转换为等效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法中，完整模式中执行的最完整的转换，但生成的代码可能更难以阅读。 在自定义模式下，您可以设置选项。  
  
有关设置以及如何在每种模式中应用设置的详细信息，请参阅以下主题：  
  
-   [项目设置&#40;转换&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
-   [Project Settings &#40;Migration&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md)  
  
-   [项目设置&#40;同步&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)  
  
-   [Project Settings &#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)  
  
-   [项目设置&#40;类型映射&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)  
  
## <a name="setting-project-options"></a>设置项目选项  
在 SSMA 中，可以配置所有项目的默认的设置。 这些设置保存到 SSMA 配置文件，并应用于创建任何新项目。  
  
**若要设置项目选项的默认值**  
  
1.  上**工具**菜单上，单击**默认项目设置**。  
  
2.  在中**默认项目设置**对话框，请使用以下过程之一：  
  
    -   选择迁移项目类型设置为其所需查看或更改从**迁移目标版本**下拉列表单击**常规**底部的左窗格中，并选择转换或迁移。  
  
    -   若要选择预定义的模式，在**模式下**下拉列表框中，选择**默认**， **Optimistic**，或**完整**。  
  
    -   若要指定自定义设置，选择或输入新的设置或值。  
  
3.  单击**确定**以保存设置。  
  
此外可以自定义当前项目的设置。 这些设置保存到当前项目文件。  
  
**若要自定义的当前项目设置**  
  
1.  上**工具**菜单上，单击**项目设置**。  
  
2.  在中**项目设置**对话框，请使用以下过程之一：  
  
    -   若要选择预定义的模式，在**模式下**下拉列表框中，选择**默认**， **Optimistic**，或**完整**。  
  
    -   若要在中指定自定义模式，**模式下**框中，选择**自定义**，然后选择相应的项目设置。  
  
3.  单击**确定**以保存设置。  
  
## <a name="next-steps"></a>后续步骤  
迁移的下一步取决于您的项目需求：  
  
-   若要自定义源和目标数据类型的映射，请参阅[映射 Oracle 和 SQL Server 数据类型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
-   否则，将转换到的 Oracle 数据库对象定义[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象定义。 有关详细信息，请参阅[转换 Oracle 架构&#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)。  
  
## <a name="see-also"></a>请参阅  
[映射 Oracle 和 SQL Server 数据类型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)  
  
