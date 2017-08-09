---
title: "扩展插件 (SSRS) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2bb0fdca-1837-49f5-b542-61826bab0b46
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d8ec3b39a36a6020a6655e7c7e7c2a589266f3fc
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="extensions-ssrs"></a>扩展插件 (SSRS)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的报表服务器使用扩展插件来模块化其为身份验证、数据处理、报表呈现和报表传递接受的输入或输出的类型。 这便于现有 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 安装利用行业中的新的软件标准，例如新的身份验证架构或自定义数据源类型。 报表服务器支持自定义的身份验证扩展插件、数据处理扩展插件、报表处理扩展插件、呈现扩展插件和传递扩展插件，并且支持在 RSReportServer.config 配置文件中向用户提供的可配置的扩展插件。 例如，您可以限制报表查看器允许使用的导出格式。 报表服务器至少分别需要一个身份验证扩展插件、数据处理扩展插件和呈现扩展插件。 传递扩展插件和报表处理扩展插件是可选的，但如果希望支持报表分发或自定义控件，则是必需的。  
  
 本主题介绍在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中可方便地使用的扩展插件。  
  
## <a name="security-extensions"></a>安全扩展插件  
 安全扩展插件用于对用户和组进行身份验证和授权，以便其能够访问报表服务器。 默认的安全扩展插件是基于 Windows 身份验证的。 如果您的部署模型需要其他身份验证方法（例如，如果您的 Internet 或 Extranet 部署需要基于窗体的身份验证），则您还可以创建自定义安全扩展插件来替换默认的安全扩展插件。 单个 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 安装中只能使用一个安全扩展插件。 您可以替换默认的 Windows 身份验证安全扩展插件，但不能将它与自定义安全扩展插件一起使用。  
  
## <a name="data-processing-extensions"></a>数据处理扩展插件  
 数据处理扩展插件用于查询数据源和返回平展行集。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 使用不同的扩展插件与不同类型的数据源交互。 您可以使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]随附的扩展插件，也可以开发自己的扩展插件。 提供用于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、Oracle、 [!INCLUDE[SAP_DPE_BW_1](../includes/sap-dpe-bw-1-md.md)]、Hyperion Essbase、Teradata、OLE DB 和 ODBC 数据源的数据处理扩展插件。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 还可以使用任何 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 数据访问接口。 数据处理扩展插件通过执行以下任务来处理来自报表处理器组件的查询请求：  
  
-   打开与数据源之间的连接。  
  
-   分析查询，并返回字段名称列表。  
  
-   对数据源运行查询，并返回行集。  
  
-   如果需要，还会向查询传递参数。  
  
-   遍历返回的行集，并检索数据。  
  
 某些扩展插件还可以执行以下任务：  
  
-   分析某一查询，并返回该查询中所使用的参数名称的列表。  
  
-   分析查询，并返回分组所使用的字段的列表。  
  
-   分析查询，并返回排序所使用的字段的列表。  
  
-   提供用户名和密码以连接到数据源。  
  
-   向查询传递具有多个值的参数。  
  
-   循环访问行并检索辅助元数据。  
  
## <a name="rendering-extensions"></a>呈现扩展插件  
 呈现扩展插件将来自报表处理器的数据和布局信息转换为设备特定的格式。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 包括七种呈现扩展插件：HTML、Excel、CSV、XML、Image、PDF 和 [!INCLUDE[msCoName](../includes/msconame-md.md)] Word。  
  
-   **HTML 呈现扩展插件** 通过 Web 浏览器向报表服务器请求报表时，报表服务器将使用 HTML 呈现扩展插件来呈现报表。 HTML 呈现扩展插件使用 UTF-8 编码生成所有的 HTML。 有关详细信息，请参阅[呈现到 HTML（报表生成器和 SSRS）](../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md)和 [Reporting Services 和 Power View 的浏览器支持](../reporting-services/browser-support-for-reporting-services-and-power-view.md)。  
  
-   **Excel 呈现扩展插件** Excel 呈现扩展插件呈现可在 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 97 或更高版本中查看和修改的报表。 此呈现扩展插件会创建二进制交换文件格式 (BIFF) 的文件。 BIFF 是 Excel 数据的本机文件格式。 在 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 中呈现的报表支持适用于任何电子表格的所有功能。 有关详细信息，请参阅[导出到 Microsoft Excel（报表生成器和 SSRS）](../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)。  
  
-   “CSV 呈现扩展插件” 逗号分隔值 (CSV) 呈现扩展插件通过不带任何格式的以逗号分隔的纯文本文件形式呈现报表。 用户随后可使用电子表格应用程序（如 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]）或任何其他可读取文本文件的程序打开这些文件。 有关详细信息，请参阅[导出到 CSV 文件（报表生成器和 SSRS）](../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)。  
  
-   **XML 呈现扩展插件** XML 呈现扩展插件以 XML 文件形式呈现报表。 随后可通过其他程序存储或读取这些 XML 文件。 您还可以使用 XSLT 转换将报表转换为另一种 XML 架构，供其他应用程序使用。 XML 呈现扩展插件生成的 XML 文件是 UTF-8 编码文件。 有关详细信息，请参阅[导出到 XML（报表生成器和 SSRS）](../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md)。  
  
-   **图像呈现扩展插件** 图像呈现扩展插件会将报表呈现为位图或图元文件。 该扩展插件可使用以下格式呈现报表：BMP、EMF、GIF、JPEG、PNG、TIFF 和 WMF。 默认情况下，将使用 TIFF 格式呈现图像，这种格式的图像可以通过您的操作系统的默认图像查看器（例如，Windows 图片和传真查看器）进行显示。 您可以从查看器中将图像发送到打印机。 使用图像呈现扩展插件呈现报表可确保报表在每个客户端上的显示都相同。 （用户查看 HTML 格式的报表时，该报表的外观会因用户浏览器的版本、用户浏览器设置以及可用字体而异。）图像呈现扩展插件在服务器上呈现报表，因此所有用户看到的都是相同的图像。 由于是在服务器上呈现报表，因此服务器上必须安装了报表中使用的所有字体。 有关详细信息，请参阅[导出到图像文件（报表生成器和 SSRS）](../reporting-services/report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md)。  
  
-   **PDF 呈现扩展插件** PDF 呈现扩展插件以 PDF 文件形式呈现报表，可以使用 Adobe Acrobat 6.0 或更高版本打开和查看这些文件。 有关详细信息，请参阅[导出到 PDF 文件（报表生成器和 SSRS）](../reporting-services/report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md)。  
  
-   **Word 呈现扩展插件**   [!INCLUDE[msCoName](../includes/msconame-md.md)] Word 呈现扩展插件可将报表呈现为与 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Word 2000 或更高版本兼容的 Word 文档。 有关详细信息，请参阅[导出到 Microsoft Word（报表生成器和 SSRS）](../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)。  
  
## <a name="report-processing-extensions"></a>报表处理扩展插件  
 可以添加报表处理扩展插件，以便为 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]未随附的报表项提供自定义报表处理。 默认情况下，报表服务器可以处理表、图表、矩阵、列表、文本框、图像以及所有其他报表项。 如果希望向在报表执行期间需要自定义处理的报表添加特殊功能（例如，如果希望嵌入 [!INCLUDE[msCoName](../includes/msconame-md.md)] MapPoint 地图），则可以创建相应的报表处理扩展插件来执行此操作。  
  
## <a name="delivery-extensions"></a>传递扩展插件  
 后台处理应用程序使用传递扩展插件将报表传递到各个位置。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 包括电子邮件传递扩展插件和文件共享传递扩展插件。 电子邮件传递扩展插件可以通过简单邮件传输协议 (SMTP) 发送电子邮件，并在其中包含报表本身或指向报表的 URL 链接。 还可以向寻呼程序、电话或其他设备发送没有 URL 链接或报表的简短通知。 文件共享传递扩展插件可以将报表保存到网络上的共享文件夹中。 您可以指定位置、呈现格式和文件名，并覆盖所创建的文件的选项。 可以使用文件共享传递插件来存档所呈现的报表，并将其作为处理特大型报表的策略的一部分。 传递扩展插件可以与订阅协同工作。 用户创建订阅时，可以选择一个可用的传递扩展插件，以确定如何传递报表。  
  
  
