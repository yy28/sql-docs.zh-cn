---
title: 设置项目选项 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e397bf4480dd7a9955fb8c7acbce0d11fd910893
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63215948"
---
# <a name="setting-project-options-mysqltosql"></a>设置项目选项 (MySQLToSQL)
对于每个 SSMA 项目，可以设置项目级别的选项。 这些选项用于指定如何转换对象、 如何迁移数据和源数据类型如何映射到目标数据类型。  在将对象转换为 SQL Server 或 SQL Azure 或将数据迁移到 SQL Server 或 SQL Azure 之前，验证配置选项适用于项目。  
  
SSMA 允许你配置的所有项目的默认选项。 这些选项不适用于您创建任何新项目。 然后可以自定义每个项目的选项。  
  
## <a name="configuration-options-and-modes"></a>配置选项和模式  
SSMA 具有五个集的项目设置：  
  
-   项目信息  
  
-   常规 （转换、 迁移和 SQL Azure）  
  
-   Synchronization  
  
-   GUI  
  
-   类型映射  
  
可以通过四种方法配置项目设置：  
  
-   默认  
  
-   乐观  
  
-   完全  
  
-   自定义  
  
建议大多数用户使用的默认模式。 乐观模式使多个当前 MySQL 语法，并易于阅读。 但是，保留当前的语法可能不会准确。 如果 MySQL 语法必须转换为等效的 SQL Server 或 SQL Azure 语法，完整模式中执行最完整的转换。 但是，生成的代码，可能更难以阅读。 在自定义模式下，可以设置选项。  
  
有关设置以及如何在每种模式中应用设置的详细信息，请参阅以下主题：  
  
-   [项目设置&#40;转换&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [项目设置&#40;迁移&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [项目设置 (GUI) （SSMA 通用）](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [项目设置&#40;类型映射&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [项目设置&#40;同步&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [项目设置&#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>设置项目选项  
在 SSMA 中，可以配置所有项目的默认的设置。 这些设置保存到 SSMA 配置文件，并应用于创建任何新项目。  
  
**若要设置项目选项的默认值**  
  
1.  上**工具**菜单上，单击**默认项目设置**。  
  
2.  在中**默认项目设置**对话框，请使用以下过程之一：  
  
    1.  选择迁移项目类型设置为其所需查看 / 更改从**迁移目标版本**下拉列表中，单击**常规**在左窗格中，并选择底部**转换或迁移或 SQL Azure**选项。  
  
    2.  若要选择预定义的模式，请选择**默认**， **Optimistic**，或**完整**从**模式**下拉列表框。  
  
    3.  若要指定自定义设置，选择或输入新的设置或值。  
  
3.  单击**确定**以保存设置。  
  
此外可以自定义当前项目的设置。 设置保存到当前项目文件。  
  
**若要自定义的当前项目设置**  
  
1.  上**工具**菜单上，单击**ProjectSettings**。  
  
2.  在中**ProjectSettings**对话框，请使用以下过程之一：  
  
    1.  若要选择预定义的模式，请选择**默认**， **Optimistic**，或**完整**从**模式**下拉列表框。  
  
    2.  若要指定自定义模式，请选择**自定义**从**模式**下拉列表框。 然后选择适当的项目设置。  
  
3.  单击**确定**以保存设置。  
  
## <a name="next-step"></a>下一步  
迁移的下一步取决于您的项目需求：  
  
-   若要自定义源和目标数据类型的映射，请参阅[映射 MySQL 和 SQL Server 数据类型&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   否则，可以将 MySQL 数据库对象定义转换到 SQL Server 或 SQL Azure 对象定义。 有关详细信息，请参阅[转换 MySQL 数据库&#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>请参阅  
[映射 MySQL 和 SQL Server 数据类型&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
