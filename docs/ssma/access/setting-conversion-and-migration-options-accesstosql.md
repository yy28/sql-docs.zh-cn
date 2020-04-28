---
title: 设置转换和迁移选项（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3e89cfd6768aeedd970889cbaea46bb3e1ceae4f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68051506"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>设置转换和迁移选项（AccessToSQL）
对于每个 SSMA 项目，可以设置项目级别的选项。 这些选项指定如何转换对象、迁移数据的方式以及源数据类型映射到目标数据类型的方式。 在将对象转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 或将数据迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到或 SQL Azure 之前，请验证配置选项是否适用于项目。  
  
## <a name="configuration-options-and-modes"></a>配置选项和模式  
SSMA 有四组配置设置和四种配置这些设置的模式：默认、乐观、完整和自定义。 对于大多数用户，建议使用默认模式。 将乐观模式用于简单转换。 如果要查看所有消息，请使用完全模式。 在 "自定义" 模式下，设置选项。  
  
此文档的 "用户界面参考" 部分介绍了这些设置。 有关设置以及如何在每个模式下应用这些设置的详细信息，请参阅以下主题：  
  
-   [项目设置（转换）](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [项目设置（迁移）](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [项目设置 (GUI)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [项目设置（类型映射）](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [项目设置（SQL Azure）](https://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>设置项目选项  
在 SSMA 中，可以配置所有项目的默认设置。 这些设置将保存到 SSMA 配置文件，并应用于你创建的任何新项目。  
  
**设置默认项目选项**  
  
1.  在 "**工具**" 菜单上，选择 "**默认项目设置**"。  
  
2.  在 "**默认项目设置**" 对话框中，执行下列操作之一：  
  
    -   从 "**迁移目标版本**" 下拉框中选择 "需要查看或更改其设置" 的 "迁移项目类型"，单击左侧窗格底部的 "**常规**"，然后选择 "**转换" 或 "迁移" 或 SQL Azure**。  
  
        > [!NOTE]  
        > 仅当创建的项目类型为 SQL Azure 时，SQL Azure 选项才会出现在 "**常规**" 选项卡中。  
  
    -   若要选择预定义模式，请在 "**模式**" 下拉框中选择 "**默认**"、"**乐观**" 或 "**完全**"。  
  
    -   若要指定自定义模式，请在 "**模式**" 框中选择 "**自定义**"，在左窗格中选择一个选项，单击右窗格中的 "设置" 或 "值"，然后选择或输入新的设置或值。  
  
3.  单击“确定”保存设置。****  
  
你还可以自定义当前项目的设置。 这些设置保存到当前项目文件中。  
  
**为当前项目自定义设置**  
  
1.  在 "**工具**" 菜单上，选择 "**项目设置**"。  
  
2.  在 "**项目设置**" 对话框中，执行下列操作之一：  
  
    -   若要选择预定义模式，请在 "**模式**" 下拉框中选择 "**默认**"、"**乐观**" 或 "**完全**"。  
  
    -   若要指定自定义模式，请在 "**模式**" 框中选择 "**自定义**"，在左窗格中选择一个选项，单击右窗格中的 "设置" 或 "值"，然后选择或输入新的设置或值。  
  
3.  单击“确定”保存设置。****  
  
## <a name="next-steps"></a>后续步骤  
迁移的下一步取决于你的项目需求：  
  
-   若要自定义源和目标数据类型的映射，请参阅[映射源和目标数据类型](mapping-source-and-target-data-types-accesstosql.md)  
  
-   若要自定义源和目标数据库的映射，请参阅[映射源和目标数据库](mapping-source-and-target-databases-accesstosql.md)  
  
-   否则，你可以将 Access 数据库对象定义转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象定义。 有关详细信息，请参阅[转换 Access 数据库对象](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>另请参阅  
[将 Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
