---
title: "设置转换和迁移选项 (AccessToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
caps.latest.revision: "20"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5cea7c02271cdf7acabb585e4be51f404f658a62
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>设置转换和迁移选项 (AccessToSQL)
对于每个 SSMA 项目，你可以设置项目级别选项。 这些选项用于指定如何转换对象、 如何迁移数据，以及如何源数据类型映射到目标数据类型。 在转换到的对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 或将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，验证是否适用于项目的配置选项。  
  
## <a name="configuration-options-and-modes"></a>配置选项和模式  
SSMA 有四个集的配置设置和配置这些设置的四种模式： 默认、 Optimistic、 完整、 和自定义。 建议大多数用户使用的默认模式。 使用开放式模式进行简单转换。 如果你想要查看所有消息，请使用完整的模式。 在自定义模式中，你可以设置选项。  
  
本文档的"用户界面参考"部分中介绍了设置。 有关设置以及如何在每个模式下应用的设置的详细信息，请参阅以下主题：  
  
-   [项目设置（转换）](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [项目设置（迁移）](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [项目设置 (GUI)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [项目设置（类型映射）](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [项目设置 (SQL Azure)](http://msdn.microsoft.com/en-us/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>设置项目选项  
在 SSMA，你可以配置所有项目的默认的设置。 这些设置将保存到 SSMA 配置文件，并应用到你创建任何新项目。  
  
**若要设置默认项目选项**  
  
1.  上**工具**菜单上，选择**默认项目设置**。  
  
2.  在**默认项目设置**对话框中，执行下列操作之一：  
  
    -   选择为其设置所需查看 / 更改，不再是迁移项目类型**迁移目标版本**下拉列表中，单击**常规**底部的左窗格中，，然后选择**转换、 迁移或 SQL Azure**。  
  
        > [!NOTE]  
        > SQL Azure 选项位于**常规**选项卡仅当创建的项目类型为 SQL Azure。  
  
    -   若要选择预定义的模式下，选择**默认**， **Optimistic**，或**完整**中**模式**下拉框。  
  
    -   若要指定自定义模式，请选择**自定义**中**模式**框中，在左窗格中选择一个选项，单击设置或在右窗格中，值，然后选择或输入新的设置或值。  
  
3.  单击**确定**以保存设置。  
  
你还可以自定义当前项目的设置。 这些设置将保存到当前的项目文件。  
  
**若要自定义为当前项目的设置**  
  
1.  上**工具**菜单上，选择**项目设置**。  
  
2.  在**项目设置**对话框中，执行下列操作之一：  
  
    -   若要选择预定义的模式下，选择**默认**， **Optimistic**，或**完整**中**模式**下拉框。  
  
    -   若要指定自定义模式，请选择**自定义**中**模式**框中，在左窗格中选择一个选项，单击设置或在右窗格中，值，然后选择或输入新的设置或值。  
  
3.  单击**确定**以保存设置。  
  
## <a name="next-steps"></a>后续步骤  
迁移的下一步取决于您的项目需求：  
  
-   若要自定义的源和目标数据类型映射，请参阅[映射源和目标数据类型](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)  
  
-   若要自定义数据库源和目标数据库的映射，请参阅[映射源和目标数据库](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
-   否则，将转换到的访问数据库对象定义[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象定义。 有关详细信息，请参阅[转换访问数据库对象](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>另请参阅  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
