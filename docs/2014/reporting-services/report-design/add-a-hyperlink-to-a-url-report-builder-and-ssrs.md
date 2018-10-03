---
title: 向 URL 添加超链接（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b29f10762f421c76dd7adbbd341038771f135a04
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086607"
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>向 URL 添加超链接（报表生成器和 SSRS）
  如果您希望用户能在报表中单击链接即可打开浏览器浏览您指定的 URL，则可向报表项添加一个超链接。 超链接既可以是静态 URL，也可以是计算结果为 URL 的表达式。 如果数据库中的某个字段包含 URL，则表达式可以包含该字段，从而为报表提供超链接的动态列表。 您可以向文本框、图像、图表和仪表添加超链接。 必须确保该用户对您提供的 URL 具有访问权限。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 如果您和您的用户有权使用对报表服务器的 URL 请求来查看某一报表服务器上的报表，则您还可以指定指向这些报表的 URL。 例如，可以指定一个报表，并在用户首次查看该报表时隐藏文档结构图。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中 [Reporting Services 文档](http://go.microsoft.com/fwlink/?linkid=121312)中的 [URL 访问 (SSRS)](../url-access-ssrs.md)。  
  
 还可以向具有 **“操作”** 属性的任何项的 URL 添加超链接，例如图表中的文本框、图像或计算序列。 用户单击该报表项时，将执行您所定义的操作。 有关详细信息，请参阅[“操作属性”对话框（报表生成器和 SSRS）](../action-properties-dialog-box-report-builder-and-ssrs.md)和[指定外部项的路径（报表生成器和 SSRS）](specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
 若要快速开始使用，请参阅[教程：设置文本格式（报表生成器）](../tutorial-format-text-report-builder.md)。  
  
> [!NOTE]  
>  绑定到数据集字段的链接容易被篡改。 有关详细信息，请参阅 msdn.microsoft.com 上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][联机丛书](http://go.microsoft.com/fwlink/?LinkId=154888)中的[保护报表和资源](../security/secure-reports-and-resources.md)。  
  
### <a name="to-add-a-hyperlink"></a>添加超链接  
  
1.  在报表设计视图中，右键单击要添加链接的文本框、图像或图表，然后单击 **“属性”**。  
  
2.  在“属性”对话框中，单击 **“操作”**。  
  
3.  选择 **“转到 URL”**。 其他部分将显示在此选项的对话框中。  
  
4.  在 **“选择 URL”** 中，键入或选择某一 URL 或者计算结果为某一 URL 的表达式，或者单击下拉箭头并单击包含 URL 的字段的名称。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  （可选）文本的格式不会自动设置为链接。 对于文本，很有必要更改文本的颜色和效果以指示该文本是一个链接。 例如，在功能区的“主页”选项卡中的 **“字体”** 部分中，将颜色更改为蓝色，并将效果更改为下划线。  
  
7.  若要测试该链接，请单击 **“运行”** 以预览报表，然后单击对其设置此链接的报表项。  
  
## <a name="see-also"></a>请参阅  
 [交互式排序、文档结构图和链接（报表生成器和 SSRS）](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [创建文档结构图（报表生成器和 SSRS）](create-a-document-map-report-builder-and-ssrs.md)  
  
  
