---
title: "设置项目选项 (MySQLToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
caps.latest.revision: "12"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 16d9b108e62772093379c46bcbf2bd171d069618
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="setting-project-options-mysqltosql"></a>设置项目选项 (MySQLToSQL)
对于每个 SSMA 项目，你可以设置项目级别选项。 这些选项用于指定如何转换对象、 如何迁移数据，以及如何源数据类型映射到目标数据类型。  在将对象转换为 SQL Server 或 SQL Azure，或将数据迁移到 SQL Server 或 SQL Azure 之前，验证的配置选项适用于项目。  
  
SSMA 允许您配置的所有项目的默认选项。 这些选项将应用于你创建的任何新项目。 然后，你可以自定义每个项目的选项。  
  
## <a name="configuration-options-and-modes"></a>配置选项和模式  
SSMA 有五个集的项目设置：  
  
-   项目信息  
  
-   常规 （转换、 迁移和 SQL Azure）  
  
-   Synchronization  
  
-   GUI  
  
-   类型映射  
  
可以四种方法配置项目设置：  
  
-   默认  
  
-   Optimistic  
  
-   完全  
  
-   自定义  
  
建议大多数用户使用的默认模式。 开放式模式保留多个当前 MySQL 语法，并且可以更轻松地读取。 但是，保持当前语法可能不准确。 如果 MySQL 语法必须转换为等效的 SQL Server 或 SQL Azure 语法，完全模式执行的最完整的转换。 生成的代码，但是，可能会更加难以读取。 在自定义模式中，你可以设置选项。  
  
有关设置以及如何在每个模式下应用的设置的详细信息，请参阅以下主题：  
  
-   [项目设置 &#40;转换 &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [项目设置 &#40;迁移 &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [项目设置 (GUI) （SSMA 通用）](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [项目设置 &#40;类型映射 &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [项目设置 &#40;同步 &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [项目设置 &#40;Azure SQL DB &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>设置项目选项  
在 SSMA，你可以配置所有项目的默认的设置。 这些设置将保存到 SSMA 配置文件，并应用到你创建任何新项目。  
  
**若要设置默认项目选项**  
  
1.  上**工具**菜单上，单击**默认项目设置**。  
  
2.  在**默认项目设置**对话框，请使用以下过程之一：  
  
    1.  选择为其设置所需查看 / 更改，不再是迁移项目类型**迁移目标版本**下拉列表中，单击**常规**底部的左窗格中，，然后选择**转换、 迁移或 SQL Azure**选项。  
  
    2.  若要选择预定义的模式下，选择**默认**， **Optimistic**，或**完整**从**模式**下拉框。  
  
    3.  若要指定自定义设置，选择或输入新的设置或值。  
  
3.  单击**确定**以保存设置。  
  
你还可以自定义当前项目的设置。 设置保存到当前的项目文件。  
  
**若要自定义为当前项目的设置**  
  
1.  上**工具**菜单上，单击**ProjectSettings**。  
  
2.  在**ProjectSettings**对话框，请使用以下过程之一：  
  
    1.  若要选择预定义的模式下，选择**默认**， **Optimistic**，或**完整**从**模式**下拉框。  
  
    2.  若要指定自定义模式，请选择**自定义**从**模式**下拉框。 然后选择相应的项目设置。  
  
3.  单击**确定**以保存设置。  
  
## <a name="next-step"></a>下一步  
迁移的下一步取决于您的项目需求：  
  
-   若要自定义的源和目标数据类型映射，请参阅[映射 MySQL 和 SQL Server 数据类型 &#40;MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   否则，你可以将 MySQL 数据库对象定义转换为 SQL Server 或 SQL Azure 对象定义。 有关详细信息，请参阅[转换 MySQL 数据库 &#40;MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>另请参阅  
[映射 MySQL 和 SQL Server 数据类型 &#40;MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
