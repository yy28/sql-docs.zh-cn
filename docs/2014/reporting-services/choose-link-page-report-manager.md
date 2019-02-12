---
title: 选择链接页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a89a555d-efa3-45d6-951e-db78ec6a2c8e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ae9bebff71148f9b88228c77fb3946919c7fd197
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036118"
---
# <a name="choose-link-page-report-manager"></a>“选择链接”页（报表管理器）
  使用“选择链接”页可为当前所选链接报表选择要基于的不同报表。 链接报表基于已发布到报表服务器的其他报表。 链接报表使用基础报表的布局和数据，但是其属性页与基础报表不同，以便您可以自定义参数属性、安全设置、名称、说明和位置。  
  
 通过“选择链接”页，可以选择另一个已发布的报表来与链接报表一起使用。 更改链接信息不会影响链接报表的其他设置（例如安全性和参数设置）。 报表服务器将不验证您选择的内容，因此请确保所选报表具有的参数与您在链接报表上指定的参数相同。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-choose-link-page"></a>打开“选择链接”页  
  
1.  打开报表管理器，找到要更改的链接报表。  
  
2.  悬停在链接报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”**。 这会打开该链接报表的 **“常规”** 属性页。  
  
4.  在 **“常规”** 选项卡上的属性页中单击 **“更改链接”**。  
  
## <a name="options"></a>选项  
 **位置**  
 指定已发布报表的全名，包括文件夹路径和报表名称。 您可以键入报表的全名，也可以使用树视图导航到要使用的报表。  
  
 **树视图**  
 显示报表服务器文件夹层次结构中的所有文件夹。 若要通过树视图来填写 **“位置”** 字段，请单击相应报表的名称。  
  
## <a name="see-also"></a>请参阅  
 [报表的“常规”属性页（报表管理器）](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [“新建链接报表”页（报表管理器）](../../2014/reporting-services/new-linked-report-page-report-manager.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
