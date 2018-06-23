---
title: 发布和重新发布报表部件（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 92dce484-f39b-403c-9caf-d8772bc3aca3
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 28c5f5063aa7e1c6e6fabe68405eb08a31feaad4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027146"
---
# <a name="publish-and-republish-report-parts-report-builder-and-ssrs"></a>发布和重新发布报表部件（报表生成器和 SSRS）
  您可以使用默认设置将报表部件发布到默认位置中，或者，您可以编辑名称和说明之类的报表部件元数据，并且将其保存在报表服务器上的其他位置。 如果您具有正确的权限，还可以将报表部件保存到与报表服务器集成的 SharePoint 站点上。  
  
 您可以将报表部件与它所依赖的、嵌入其中的数据集一起发布，也可以单独发布数据集。 如果单独发布数据集，它将成为共享数据集，并且报表部件将与其链接。 有关详细信息，请参阅 [报表生成器中的报表部件和数据集](../report-data/report-parts-and-datasets-in-report-builder.md)。  
  
 您可以重新发布现有的报表部件。 如果您具有权限，则可以将报表部件的原始实例保存在服务器上, 即使您没有创建它。 您还可以将其发布为新的报表部件，并且将它保存在相同或不同的位置。  
  
### <a name="to-publish-a-report-part"></a>发布报表部件  
  
1.  在报表生成器菜单上，单击 **“发布报表部件”**。  
  
     如果您没有连接到某一报表服务器，则系统将会提示您进行连接。 如果您无法连接到报表服务器，则不能发布报表部件。  
  
2.  若要使用默认设置将报表部件保存到默认位置，请单击 **“使用默认设置发布所有报表部件”**。  
  
     否则，单击 **“在发布前查看和修改报表部件”**。  
  
3.  编辑报表部件名称和说明：双击名称以便编辑它，然后在“说明”字段中单击以便添加说明。  
  
    > [!NOTE]  
    >  最好提供报表部件名称和说明，以便在搜索时帮助用户识别它。 对于整个路径而言，报表部件名称的最大长度是 260 个字符，包括服务器上文件夹的名称，后随报表部件的实际名称。  
  
4.  若要将报表部件保存到默认位置外的其他文件夹，请单击 **“浏览”** 按钮。  
  
5.  在您为报表中的所有报表部件都设置了选项之后，请单击 **“发布”**。  
  
     在发布报表部件后，对话框将显示哪些报表部件已成功发布，哪些未成功发布。 对于未能发布的报表部件，您可以在 **“发布报表部件”** 对话框中查看详细信息。  
  
6.  单击 **“关闭”**。  
  
### <a name="to-republish-a-report-part"></a>重新发布报表部件  
  
1.  按照前面的过程发布报表部件。  
  
2.  在 **“发布报表部件”** 对话框中，如果您单击 **“作为报表部件的新副本发布”**，则报表生成器将不会保存在服务器的现有报表部件上，而将改为创建另一个报表部件。  
  
> [!NOTE]  
>  如果您将其作为新的报表部件发布，则该报表部件将具有新的唯一 ID。 如果原始报表部件发生更改，它将不再接收更新。  
  
## <a name="see-also"></a>请参阅  
 [报表部件&#40;报表生成器和 SSRS&#41;](../report-parts-report-builder-and-ssrs.md)   
 [报表部件和报表生成器中的数据集](../report-data/report-parts-and-datasets-in-report-builder.md)   
 [解决报表部件&#40;报表生成器和 SSRS&#41;](../troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [检查更新或关闭更新&#40;报表生成器和 SSRS&#41;](../check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md)   
 [查找报表部件和设置默认文件夹&#40;报表生成器和 SSRS&#41;](browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
  