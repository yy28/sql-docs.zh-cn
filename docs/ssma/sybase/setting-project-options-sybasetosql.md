---
title: "设置项目选项 (SybaseToSQL) |Microsoft 文档"
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
helpviewer_keywords:
- Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 40c2bffdb58fadfa3a9c7da58cf68b8c4390cd16
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="setting-project-options-sybasetosql"></a>设置项目选项 (SybaseToSQL)
对于每个 SSMA 项目，你可以设置项目级别选项。 这些选项用于指定对象转换、 对象加载、 SQL azure、 用户界面和数据迁移设置。 在转换到的对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 或将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，验证是否适用于项目的配置选项。  
  
SSMA 允许您配置的所有项目的默认选项。 这些选项将应用于你创建任何新项目。 然后，你可以自定义每个项目的选项。  
  
## <a name="configuration-options-and-modes"></a>配置选项和模式  
SSMA 有五个集的项目设置：  
  
1.  项目信息  
  
2.  常规 （转换、 迁移和收集数据）  
  
3.  Synchronization  
  
4.  GUI  
  
5.  类型映射  
  
它还具有用于配置这些设置的四种模式：  
  
1.  默认  
  
2.  Optimistic  
  
3.  “完全”  
  
4.  自定义  
  
建议大多数用户使用的默认模式。 开放式模式保留多个当前 Sybase 自适应 Server Enterprise (ASE) 语法，并且可以更轻松地读取。 但是，保持当前语法可能不准确。 如果 ASE 语法必须转换为等效[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 语法中，完全模式执行完成转换，但生成的代码可能会更加难以读取。 在自定义模式中，你可以设置选项。  
  
本文档的用户界面参考部分中介绍了设置。 有关设置以及如何在每个模式下应用的设置的详细信息，请参阅以下主题：  
  
-   [项目设置 &#40;转换 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [项目设置 &#40;迁移 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [项目设置 &#40;同步 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [项目设置 &#40;GUI &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [项目设置 &#40;类型映射 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [项目设置 &#40;Azure SQL DB &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>设置项目选项  
在 SSMA，你可以配置所有项目的默认的设置。 这些设置将保存到 SSMA 配置文件，并应用到你创建任何新项目。  
  
**若要设置默认项目选项**  
  
1.  上**工具**菜单上，选择**默认项目设置**。  
  
2.  在**默认项目设置**对话框，请使用以下过程之一：  
  
    -   选择迁移项目类型的设置为需要查看或更改，不再是**迁移目标版本**删除向下单击底部的左窗格中，常规，然后选择转换或迁移或 SQL Azure。  
  
    -   若要选择预定义的模式下，在**模式**下拉列表框中，选择**默认**， **Optimistic**，或**完整**。  
  
    -   若要指定自定义设置，只需选择或输入新的设置或值。  
  
3.  单击 **确定** 以保存设置。  
  
你还可以自定义当前项目的设置。 这些设置将保存到当前的项目文件。  
  
**若要自定义为当前项目的设置**  
  
1.  上**工具**菜单上，选择**项目设置**。  
  
2.  在**项目设置**对话框，请使用以下过程之一：  
  
    -   若要选择预定义的模式下，在**模式**下拉列表框中，选择**默认**， **Optimistic**，或**完整**。  
  
    -   若要指定自定义模式，在**模式**下拉列表框中，选择**自定义**、 的左窗格中选择一个选项，单击的设置或值在右窗格中，然后选择或输入新的设置或值。  
  
3.  单击 **确定** 以保存设置。  
  
## <a name="next-steps"></a>后续步骤  
迁移的下一步取决于您的项目需求：  
  
-   如果你希望的自定义的源和目标数据类型映射，请参阅[映射 Sybase ASE 和 SQL Server 数据类型 &#40;SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   否则，将转换到的 Sybase 数据库对象定义[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象定义。 有关详细信息，请参阅[转换 Sybase ASE 数据库对象 &#40;SybaseToSQL &#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>另請參閱  
[Sybase ASE 将数据库迁移到 SQL Server 的 Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

