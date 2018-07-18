---
title: 设置项目选项 (OracleToSQL) |Microsoft 文档
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Configuration Options and Modes
ms.assetid: a324d07d-cfdf-43bd-98a0-acf332c5a4db
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 5c606de3c03038f7e2fbb9f974ba96dd64bef779
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34777973"
---
# <a name="setting-project-options-oracletosql"></a>设置项目选项 (OracleToSQL)
为每个 SSMA 项目中，你可以设置项目级别选项。 这些选项用于指定对象转换、 对象加载、 用户界面和数据迁移设置。 在转换到的对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，验证是否适用于项目的配置选项。  
  
SSMA 允许您配置的所有项目的默认选项。 这些选项将应用于你创建的任何新项目。 然后，你可以自定义每个项目的选项。  
  
## <a name="configuration-options-and-modes"></a>配置选项和模式  
SSMA 有五个集的项目设置：  
  
-   项目信息  
  
-   常规 （迁移，加载对象中的转换）  
  
-   Synchronization  
  
-   GUI  
  
-   类型映射  
  
它还具有用于配置这些设置的四种模式：  
  
-   ，则“默认”  
  
-   Optimistic  
  
-   完全  
  
-   自定义  
  
建议大多数用户使用的默认模式。 开放式模式保留多个当前 Oracle 语法，并且可以更轻松地读取。 但是，保持当前语法可能不准确。 如果 Oracle 语法必须转换为等效[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法中，完全模式执行最完整的转换，但生成的代码可能会更加难以读取。 在自定义模式中，你可以设置选项。  
  
有关设置以及如何在每个模式下应用的设置的详细信息，请参阅以下主题：  
  
-   [项目设置&#40;转换&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
-   [项目设置&#40;迁移&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md)  
  
-   [项目设置&#40;同步&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)  
  
-   [项目设置&#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)  
  
-   [项目设置&#40;类型映射&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)  
  
## <a name="setting-project-options"></a>设置项目选项  
在 SSMA，你可以配置所有项目的默认的设置。 这些设置将保存到 SSMA 配置文件，并应用到你创建任何新项目。  
  
**若要设置默认项目选项**  
  
1.  上**工具**菜单上，单击**默认项目设置**。  
  
2.  在**默认项目设置**对话框，请使用以下过程之一：  
  
    -   选择迁移项目类型的设置为需要查看或更改，不再是**迁移目标版本**下拉单击**常规**底部的左窗格中，，然后选择转换或迁移。  
  
    -   若要选择预定义的模式下，在**模式**下拉列表框中，选择**默认**， **Optimistic**，或**完整**。  
  
    -   若要指定自定义设置，选择或输入新的设置或值。  
  
3.  单击**确定**以保存设置。  
  
你还可以自定义当前项目的设置。 这些设置将保存到当前的项目文件。  
  
**若要自定义为当前项目的设置**  
  
1.  上**工具**菜单上，单击**项目设置**。  
  
2.  在**项目设置**对话框，请使用以下过程之一：  
  
    -   若要选择预定义的模式下，在**模式**下拉列表框中，选择**默认**， **Optimistic**，或**完整**。  
  
    -   若要指定自定义模式，在**模式**框中，选择**自定义**，然后选择相应的项目设置。  
  
3.  单击**确定**以保存设置。  
  
## <a name="next-steps"></a>后续步骤  
迁移的下一步取决于您的项目需求：  
  
-   若要自定义的源和目标数据类型映射，请参阅[映射 Oracle 和 SQL Server 数据类型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
-   否则，将转换到的 Oracle 数据库对象定义[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象定义。 有关详细信息，请参阅[转换 Oracle 架构&#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)。  
  
## <a name="see-also"></a>请参阅  
[将 Oracle 和 SQL Server 数据类型映射&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)  
  
