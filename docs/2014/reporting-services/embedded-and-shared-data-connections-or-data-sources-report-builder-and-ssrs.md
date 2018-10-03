---
title: 嵌入和共享的数据连接或数据源 （报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- embedded data sources
- shared data sources
- data sources
ms.assetid: f417782c-b85a-4c4d-8a40-839176daba56
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1862d4d8a1437f223e688b0b2b95ad5b5768e6a8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224429"
---
# <a name="embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs"></a>嵌入和共享的数据连接或数据源（报表生成器和 SSRS）
  当运行查询或处理报表时，报表使用数据连接来检索报表的数据。 您可以从内置数据连接类型的列表中进行选择，以连接到关系数据库、多维数据库、Web 服务或一些其他数据源。 当描述数据连接时，需要使用以下术语。  
  
-   **数据连接。** 也称为“数据源”。 数据连接包含名称和依赖于连接类型的连接属性。 根据设计，数据源连接不包含凭据。 数据连接不指定从外部数据源中检索哪些数据。 为此，请在创建数据集时指定查询。  
  
-   **数据源定义。** 包含报表数据源的 XML 表示形式的文件。 在发布报表之后，其数据源作为数据源定义（独立于报表定义）保存到报表服务器或 SharePoint 站点上。 例如，报表服务器管理员可以更新连接字符串或凭据。 在本机报表服务器上，文件类型为 .rds。 在 SharePoint 站点上，文件类型为 .rsds。  
  
-   **连接字符串。** 连接字符串是连接到数据源所需的连接属性的字符串版本。 连接属性根据数据连接类型不同而异。 有关示例，请参阅 [Data Connections, Data Sources, and Connection Strings in Report Builder](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)。  
  
-   **共享数据源。** 报表服务器或 SharePoint 站点上提供的可由多个报表使用的数据源。  
  
-   **嵌入数据源。** 也称为 *特定于报表的数据源*。 在报表中定义并只由该报表使用的数据源。  
  
-   **凭据。** 凭据是身份验证信息，你必须提供这些信息才能访问外部数据。  
  
 嵌入数据源和共享数据源的区别在于创建、存储和管理它们的方式不同。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="shared-data-sources"></a>共享数据源  
 如果您的数据源使用频率较高，就可以采用共享数据源。 建议尽量使用共享数据源。 使用共享数据源可便于对报表和报表访问进行管理，并有助于提高报表和报表所访问数据源的访问安全性。 如果需要共享数据源，可以请求系统管理员为您创建一个。  
  
 在报表生成器中，您不能创建共享数据源。 您可以浏览到报表服务器中的共享数据源并进行选择。 有关详细信息，请参阅[数据连接、 数据源和报表生成器中的连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)。  
  
 在报表设计器中，您不能浏览到报表服务器上的共享数据源。 在解决方案资源管理器中，您可以将共享数据源作为项目的一部分创建，并选择是否将它们部署到报表服务器。 您只能选择在本地使用它们，因为您的计算机或报表服务器要求的凭据存在差异。 有关详细信息，请参阅 [ Reporting Services 中的数据连接、数据源和连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
 下面的图标表示报表服务器文件夹层次结构中的共享的数据源项：![共享数据源图标](media/hlp-16datasource.png "共享数据源图标")  
  
## <a name="embedded-data-sources"></a>嵌入数据源  
 嵌入数据源是保存在报表定义中的数据连接。 只有嵌入数据源连接信息所嵌入的报表才能使用这些信息。 若要定义并管理嵌入数据源，请使用 **“数据源属性”** 对话框。  
  
##  <a name="Comparing"></a> 比较嵌入和共享数据源  
 下表总结了嵌入数据源和共享数据源之间的差异：  
  
|Description|嵌入<br /><br /> 数据源|共享<br /><br /> 数据源|  
|-----------------|------------------------------|----------------------------|  
|数据连接嵌入在报表定义中。|![可用](media/greencheck.gif "Available")||  
|指向报表服务器上的数据连接的指针嵌入在报表定义中。||![可用](media/greencheck.gif "Available")|  
|在报表服务器上管理|![可用](media/greencheck.gif "Available")|![可用](media/greencheck.gif "Available")|  
|对于共享数据集，要求这么做||![可用](media/greencheck.gif "Available")|  
|对于组件，要求这么做||![可用](media/greencheck.gif "Available")|  
  
## <a name="data-source-credentials"></a>数据源凭据  
 凭据用于创建嵌入数据源、运行查询或在报表处理过程中检索数据。 数据源所有者确定您在访问数据时必须使用的凭据。 凭据在报表服务器、SharePoint 站点或报表创作环境中的本地计算机上独立于数据连接进行管理。 根据数据源的类型，可以保存凭据以避免提醒，也可以将其设置为提醒每个用户。 根据您是从计算机连接到数据源，还是从报表服务器连接到数据源，您需要的凭据可能不同。 有关详细信息，请参阅[在报表生成器中指定凭据](../../2014/reporting-services/specify-credentials-in-report-builder.md)并[数据连接、 数据源和 Reporting Services 中的连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [向报表添加数据&#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [报表创作概念&#40;报表生成器和 SSRS&#41;](report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [Reporting Services 支持的数据源&#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [添加和验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [嵌入数据集和共享数据集（报表生成器和 SSRS）](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
