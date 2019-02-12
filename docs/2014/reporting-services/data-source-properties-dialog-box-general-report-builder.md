---
title: 数据源属性对话框，常规 （报表生成器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10018"
ms.assetid: b956f43a-8426-4679-acc1-00f405d5ff5b
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: e64f98f376e704716a40eedcda8351331280fb9e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031848"
---
# <a name="data-source-properties-dialog-box-general-report-builder"></a>“数据源属性”对话框 -&gt;“常规”（报表生成器）
  在 **“数据源属性”** 对话框中选择 **“常规”** 可从报表服务器中选择共享数据源，或者创建或修改报表中嵌入的数据源的连接信息。  
  
 在数据源属性中可以指定连接到数据源时使用的凭据的类型。 在报表服务器中打开报表时，在数据源属性中指定的运行时凭据可能不适合创建查询和预览报表之类的设计时任务。 例如，数据源可能使用另一个 Windows 凭据（而不是您的凭据）或您不知道的用户名和密码。  
  
 如果使用数据源属性中提供的凭据无法连接到数据源，报表生成器会打开 **“输入数据源凭据”** 对话框。 通常在以下情况下会打开该对话框：  
  
-   数据源配置为提示输入凭据。  
  
-   数据源配置为使用存储的凭据。  为了将安全风险降到最低，报表生成器设计为不检索服务器上存储的凭据。  
  
 您可以使用 **“输入数据源凭据”** 对话框更改报表生成器在设计时使用的凭据，从而作为当前 Windows 用户连接到数据源，或者使用该对话框提供用户名和密码。 如果您提供用户名和密码，则可以指明它们是否用作 Windows 凭据。  
  
> [!NOTE]  
>  虽然使用查询设计器可以为设计时凭据指定其他凭据类型，但报表预览只允许输入在数据源中指定的现有凭据选项的用户名和密码。  
  
 单击 **“测试连接”** 时，将使用在数据源属性凭据页中指定的凭据测试与数据源的连接。 可以测试与嵌入数据源和共享数据源的连接。  
  
 如果指定的凭据不完整（例如需要密码），则报表生成器会在需要连接到数据源时再次提示您输入运行时凭据。 设计时凭据将存储起来，不再提示您进行输入。  
  
## <a name="options"></a>选项  
 **名称**  
 键入数据源的名称。 数据源名称在报表中必须是唯一的。 默认情况下，会为数据源分配一个常规名称，如 DataSource1 或 DataSource2。  
  
 **使用共享的连接**  
 选择此选项可浏览已发布到报表服务器的共享数据源。  
  
 从报表服务器选择数据源后，报表生成器会保持到此报表服务器的连接。  
  
 **使用我的报表中嵌入的连接**  
 选择此选项可创建仅供此报表使用的数据源。  
  
 **类型**  
 选择数据处理扩展插件。 该列表显示所有已注册的扩展插件。  
  
 **连接字符串**  
 输入数据源的连接字符串。 单击 **“生成”** 可使用 **“连接属性”** 对话框生成连接字符串。 单击“表达式” (*fx*) 按钮可编辑表达式。  
  
 **处理查询时使用单个事务**  
 选择此选项可指示使用此数据源的数据集在针对数据库的单个事务中运行。 若要将使用同一数据源的子报表的事务包括在内，请选择该子报表，然后在“属性”窗格中，将 **MergeTransactions** 设置为 **True**。  
  
 **测试连接**  
 单击以使用指定的凭据验证数据源连接是否正常工作。 如果不能建立连接，则需要验证您的凭据和服务器可用性。 可以为嵌入数据源和共享数据源测试数据源连接。  
  
## <a name="see-also"></a>请参阅  
 [向报表添加数据&#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [添加和验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [报表生成器中的数据连接、数据源和连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [数据源凭据-属性对话框&#40;报表生成器&#41;](../../2014/reporting-services/data-source-properties-dialog-box-credentials-report-builder.md)   
 [用于对话框、窗格和向导的报表生成器帮助](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
