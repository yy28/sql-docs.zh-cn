---
title: 设置项目选项 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 08b1084f2f54a204f82bc0d1a0ee4096d207d835
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773975"
---
# <a name="setting-project-options-sybasetosql"></a>设置项目选项 (SybaseToSQL)
对于每个 SSMA 项目，可以设置项目级别选项。 这些选项指定对象转换、 对象加载、 SQL azure、 用户界面和数据迁移设置。 在转换到的对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 或将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，验证配置选项是否适用于该项目。  
  
SSMA 允许你配置的所有项目的默认选项。 这些选项不适用于您创建任何新项目。 然后可以自定义每个项目的选项。  
  
## <a name="configuration-options-and-modes"></a>配置选项和模式  
SSMA 具有五个集的项目设置：  
  
1.  项目信息  
  
2.  常规 （转换、 迁移和收集数据）  
  
3.  Synchronization  
  
4.  GUI  
  
5.  类型映射  
  
它还具有四种模式来配置这些设置：  
  
1.  ，则“默认”  
  
2.  Optimistic  
  
3.  完全  
  
4.  自定义  
  
建议大多数用户使用的默认模式。 乐观模式使多个当前 Sybase Adaptive Server Enterprise (ASE) 语法，并易于阅读。 但是，保留当前的语法可能不会准确。 如果 ASE 语法必须转换为等效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的语法中，完整模式下执行完整的转换，但生成的代码可能更难以阅读。 在自定义模式下，您可以设置选项。  
  
本文档的用户界面参考部分中描述了这些设置。 有关设置以及如何在每种模式中应用设置的详细信息，请参阅以下主题：  
  
-   [项目设置&#40;转换&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [项目设置&#40;迁移&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [项目设置&#40;同步&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [项目设置&#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [项目设置&#40;类型映射&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [项目设置&#40;Azure SQL DB &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>设置项目选项  
在 SSMA 中，可以配置所有项目的默认的设置。 这些设置保存到 SSMA 配置文件，并应用于创建任何新项目。  
  
**若要设置项目选项的默认值**  
  
1.  上**工具**菜单中，选择**默认项目设置**。  
  
2.  在中**默认项目设置**对话框，请使用以下过程之一：  
  
    -   选择迁移项目类型设置为其所需查看或更改从**迁移目标版本**删除向下单击底部的左窗格中，常规，然后选择转换或迁移或 SQL Azure。  
  
    -   若要选择预定义的模式，在**模式下**下拉列表框中，选择**默认**， **Optimistic**，或**完整**。  
  
    -   若要指定自定义设置，只需选择或输入新的设置或值。  
  
3.  单击**确定**以保存设置。  
  
此外可以自定义当前项目的设置。 这些设置保存到当前项目文件。  
  
**若要自定义的当前项目设置**  
  
1.  上**工具**菜单中，选择**项目设置**。  
  
2.  在中**项目设置**对话框，请使用以下过程之一：  
  
    -   若要选择预定义的模式，在**模式下**下拉列表框中，选择**默认**， **Optimistic**，或**完整**。  
  
    -   若要在中指定自定义模式，**模式下**下拉列表框中，选择**自定义**，在左窗格中选择一个选项，单击设置或右窗格中的值，然后选择或输入新设置或值。  
  
3.  单击**确定**以保存设置。  
  
## <a name="next-steps"></a>后续步骤  
迁移的下一步取决于您的项目需求：  
  
-   如果您希望为自定义源和目标数据类型的映射，请参阅[映射 Sybase ASE 和 SQL Server 数据类型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
-   否则，将转换到 Sybase 数据库对象定义[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象定义。 有关详细信息，请参阅[转换 Sybase ASE 数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)。  
  
## <a name="see-also"></a>请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
