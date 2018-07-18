---
title: 设置转换和迁移选项 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bf73284de3f23aa861c446e4a2ed67278f4a5ce5
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979699"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>设置转换和迁移选项 (AccessToSQL)
对于每个 SSMA 项目，可以设置项目级别的选项。 这些选项用于指定如何转换对象、 如何迁移数据和源数据类型如何映射到目标数据类型。 在转换到的对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 或将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，验证配置选项是否适用于该项目。  
  
## <a name="configuration-options-and-modes"></a>配置选项和模式  
SSMA 中有四个组配置设置和配置这些设置的四种模式： 默认、 Optimistic、 Full 和自定义。 建议大多数用户使用的默认模式。 使用乐观模式进行简单转换。 如果你想要查看所有消息，请使用完整模式。 在自定义模式下，您可以设置选项。  
  
本文档的"用户界面参考"部分中描述了这些设置。 有关设置以及如何在每种模式中应用设置的详细信息，请参阅以下主题：  
  
-   [项目设置（转换）](http://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [项目设置（迁移）](http://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [项目设置 (GUI)](http://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [项目设置（类型映射）](http://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [项目设置 (SQL Azure)](http://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>设置项目选项  
在 SSMA 中，可以配置所有项目的默认的设置。 这些设置保存到 SSMA 配置文件，并应用于创建任何新项目。  
  
**若要设置项目选项的默认值**  
  
1.  上**工具**菜单中，选择**默认项目设置**。  
  
2.  在中**默认项目设置**对话框中，执行下列任一操作：  
  
    -   选择迁移项目类型设置为其所需查看 / 更改从**迁移目标版本**下拉列表中，单击**常规**在左窗格中，并选择底部**转换或迁移或 SQL Azure**。  
  
        > [!NOTE]  
        > SQL Azure 选项现已推出**常规**选项卡仅当创建的项目类型为 SQL Azure。  
  
    -   若要选择预定义的模式，请选择**默认**， **Optimistic**，或**完整**中**模式**下拉列表框。  
  
    -   若要指定自定义模式，请选择**自定义**中**模式**框中，在左窗格中选择一个选项，单击设置或右窗格中的值，然后选择或输入新的设置或值。  
  
3.  单击**确定**以保存设置。  
  
此外可以自定义当前项目的设置。 这些设置保存到当前项目文件。  
  
**若要自定义的当前项目设置**  
  
1.  上**工具**菜单中，选择**项目设置**。  
  
2.  在中**项目设置**对话框中，执行下列任一操作：  
  
    -   若要选择预定义的模式，请选择**默认**， **Optimistic**，或**完整**中**模式**下拉列表框。  
  
    -   若要指定自定义模式，请选择**自定义**中**模式**框中，在左窗格中选择一个选项，单击设置或右窗格中的值，然后选择或输入新的设置或值。  
  
3.  单击**确定**以保存设置。  
  
## <a name="next-steps"></a>后续步骤  
迁移的下一步取决于您的项目需求：  
  
-   若要自定义源和目标数据类型的映射，请参阅[映射源和目标数据类型](http://msdn.microsoft.com/b362a075-16e7-423f-b63f-e1e9f02844a9)  
  
-   若要自定义源和目标数据库的映射，请参阅[映射源和目标数据库](http://msdn.microsoft.com/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
-   否则，将转换到访问数据库对象定义[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象定义。 有关详细信息，请参阅[转换访问数据库对象](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>请参阅  
[Access 数据库迁移到 SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
