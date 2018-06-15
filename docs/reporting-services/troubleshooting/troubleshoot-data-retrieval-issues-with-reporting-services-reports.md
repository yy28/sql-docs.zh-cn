---
title: 与 Reporting Services 报表的数据检索问题疑难解答 |Microsoft 文档
ms.custom: ''
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: troubleshooting
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7680946a-1660-4b59-a03a-c4d474cd8ed3
caps.latest.revision: 4
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3503952eb791c4423826626b98e8f8feb2bce0c7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33032324"
---
# <a name="troubleshoot-data-retrieval-issues-with-reporting-services-reports"></a>Reporting Services 报表的数据检索问题疑难解答
报表处理的第一步是通过运行数据集查询检索每个数据集的报表数据。 本地预览报表时，数据源连接和凭据必须使用足够的权限才能检索计算机上的数据。 在报表服务器上运行报表时，数据源连接和凭据必须使用足够的权限才能检索报表服务器上的数据。 使用本主题可帮助解决有关报表数据检索的问题。   
  
## <a name="i-cannot-create-a-connection-to-a-data-source"></a>无法与数据源建立连接  
当您创建数据源、运行数据集查询或预览报表时，可能得到下面的消息：无法与数据源 `<data source name>`建立连接。   
    
### <a name="data-source-is-not-available"></a>数据源不可用。  
数据源由于其他某种原因脱机或不可用。   
  
请确认您有权访问该数据源，并且该数据源可用。 例如，使用 Sql Server Management Studio 连接数据源。 对于关系数据库和多维数据库，请使用“连接属性”  对话框中的“测试”  按钮来验证与数据源的连接和对数据源的权限。   
  
### <a name="data-source-credentials-are-not-valid"></a>数据源凭据无效。  
您用来连接数据源的凭据没有足够权限来检索查询中指定的数据。  
  
请确认使用的凭据正确。 例如，您可能有权从表或视图检索数据，但不能检索特定列的数据；或者您可能没有足够权限运行填充视图的存储过程。   
  
> [!NOTE]  
> 检索用于预览报表的数据所需的权限可能与将报表发布到报表服务器之后检索数据时所需的权限不同。   
  
### <a name="not-a-valid-password"></a>密码无效  
对于具有提示凭据或在连接字符串中指定的凭据的数据源，密码的字符会传递给基础数据源驱动程序。 如果密码或字符串包含特殊字符（如引号），则某些数据源驱动程序将无法验证这些特殊字符。   
  
确认密码不包含特殊字符。 如果不能更改密码，则可以请数据库管理员将相应的凭据作为系统 ODBC 数据源名称 (DSN) 的一部分存储在本地和服务器中。 有关详细信息，请参阅 MSDN 上的 .NET Framework SDK 文档中的“OdbcConnection.ConnectionString”。   
  
> [!NOTE]  
>建议您不要在连接字符串中添加登录信息（如密码）。 报表设计器在 [“数据源属性”](~/reporting-services/report-data/enter-data-source-credentials-dialog-box-report-builder.md) 或 [“共享数据源属性”](~/reporting-services/report-data/enter-data-source-credentials-dialog-box-report-builder.md) 对话框上提供 **“凭据”** 页，你可在其中输入凭据。 这些凭据安全地存储在报表创作计算机上。  
  
## <a name="why-do-i-see-no-data-when-i-run-my-query-in-the-query-designer"></a>在查询设计器中运行查询时为什么看不到数据？  
创建数据集时，数据集字段集合将显示在“报表数据”窗格中。 有时候，数据集字段集合不按预期的方式显示。   
  
### <a name="import-query-does-not-import-calculated-fields"></a>导入查询不导入计算字段  
  
尽管计算字段保存在报表定义中，但从其他报表中导入数据集查询时不会包含这些字段。 如果通过从其他报表导入查询来创建数据集，则仅该数据集查询指定的字段会显示在“报表数据”窗格中。   
  
若要在“报表数据”窗格中查看计算字段，必须为使用计算字段的每个报表定义计算字段。   
  
### <a name="some-data-providers-do-not-support-automatic-population-of-the-dataset-field-collection"></a>有些数据访问接口不支持自动填充数据集字段集合  
在“数据集属性”对话框中定义查询时，关闭该对话框后，数据集字段集合通常会显示在“报表数据”窗格中。 对于某些数据源，不会自动填充数据集字段集合。   
  
若要填充数据集字段集合，请执行以下操作：  
* 确保您具有从数据库中检索字段信息的权限。 对于某些数据源，您可能有权访问数据源，但无权访问表或列。 您可能有权访问视图，但无权运行创建视图的存储过程。 若要验证你是否具有访问数据库中特定表或列的权限，请使用用于报表的相同权限，在一个单独的应用程序（例如 SQL Server Management Studio）中验证查询结果。 如果看不到查询需要的结果，请与系统管理员联系调整您的数据访问权限。   
* 在“数据集属性”  对话框的查询窗格中运行该查询。 有关详细信息，请参阅 [报表数据集（Report Builder 3.0 和 SSRS）](../../reporting-services/report-data/report-datasets-ssrs.md)。  
* 手动添加字段。 有关详细信息，请参阅 [如何在“报表数据”窗格中添加、编辑或刷新字段（Report Builder 3.0 和 SSRS）](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)。   
  
## <a name="see-also"></a>另请参阅  
[错误和事件 (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]



