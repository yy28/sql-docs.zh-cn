---
title: 使用浏览器查找和查看报表（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: edf4843a-2a0a-486f-be25-14a3c1c6bc72
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f8e7d1aa634b124c009d899af6405f5343e99d8
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59955103"
---
# <a name="finding-and-viewing-reports-with-a-browser-report-builder-and-ssrs"></a>使用浏览器查找和查看报表（报表生成器和 SSRS）
  通过与报表服务器直接连接，您可以使用支持的任何 Web 浏览器查看报表。 每个报表在报表服务器上都有一个 URL 地址。 无需使用 Web 应用程序，输入报表的 Web 地址即可在浏览器窗口中打开相应报表。 相应的报表会以 HTML 格式打开，并且包含报表工具栏，这样在此报表中您就可以在各页间导航或按数据值进行搜索。 您可以在 URL 中设置参数以隐藏报表工具栏或选择报表的输出格式。  
  
 这种通过报表的 Web 地址打开报表的方法适合查看报表，但不适合管理报表。 通过这种方法，无法访问项的属性页或订阅定义页。 必须使用报表管理器或 SharePoint 站点来完成这些任务。  
  
 如果不知道某一报表的 Web 地址，则可以打开相应报表服务器的 Web 地址，然后浏览报表服务器文件夹层次结构以选择要查看的报表。 下图显示了在浏览器窗口中显示的文件夹层次结构。  
  
 ![浏览器中的文件夹](../media/rs-browserfolder.GIF "Folders in a browser")  
浏览器中的文件夹  
  
> [!NOTE]  
>  如果是通过手持设备访问报表，则必须使用浏览器打开报表。 报表管理器界面的大小不适于在手持设备上显示。  
  
 有关可以使用的浏览器类型的详细信息，请参阅 SQL Server 联机丛书中 [Reporting Services 文档](https://go.microsoft.com/fwlink/?linkid=121312) 中的“Reporting Services 支持的浏览器类型”。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="navigating-report-server-folders-in-a-web-browser"></a>在 Web 浏览器中定位报表服务器文件夹  
 您可以使用 Web 浏览器定位报表服务器文件夹并运行报表。 报表和项在文件夹层次结构中以链接的形式显示。 您可以单击链接打开报表、资源或文件夹，或者查看共享数据源的内容。 如果不知道报表的 URL，则可以浏览文件夹层次结构。 您可以指定报表服务器的 Web 地址，以在文件夹层次结构的根节点处打开浏览器连接，然后单击文件夹链接以在此层次结构中导航。  
  
 在访问报表服务器虚拟目录时，您只能查看文件夹、报表以及您可以访问的上载项。 该用户界面只显示文件夹层次结构和基本信息，如创建日期或修改日期、文件大小以及各项的项类型：  
  
-   不带任何其他指示符的链接指向的是报表或模型。  
  
-   标记 \<ds> 表示共享数据源。  
  
-   标记 \<dir> 表示文件夹项。  
  
-   一种文件扩展名表示一种资源。 文件扩展名用于标识资源的 MIME 类型。 例如，.jpg 表示 JPEG 格式的图像。  
  
## <a name="typing-the-url-address-of-a-report"></a>键入报表的 URL 地址  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支持通过 URL 访问报表服务器上的特定项。 相应的 URL 必须包含报表的完全限定路径以及用来呈现报表的命令。 如果相应报表包含参数，您还必须指定打开此报表所需的所有值。 如果您键入的报表 URL 在路径、参数值或呈现扩展插件中包含空格，则必须在该 URL 中加入 URL 编码字符才能获得预期的结果。 下例是一个在路径名称、参数和呈现扩展插件中包含空格编码的报表 URL：  
  
 `http://<Webservername>/reportserver?/<reportfolder>/employee+sales+summary&ReportYear=2004&ReportMonth=06&EmpID=24&rs:Command=Render&rs:Format=HTML4.0`  
  
 在 Internet Explorer 中对 URL 的最大长度限制为 2,083 个字符。 有关详细信息，请参阅 [Internet Explorer 中的最大 URL 长度](https://support.microsoft.com/kb/208427)。  
  
 有关通过 URL 访问报表的详细信息，包括有关 URL 构造方式的信息，请参阅 SQL Server 联机丛书中 [Reporting Services 文档](https://go.microsoft.com/fwlink/?linkid=121312) 中的“URL 访问”。  
  
## <a name="see-also"></a>请参阅  
 [查找和查看报表在报表管理器&#40;报表生成器和 SSRS&#41;](finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)  
  
  
