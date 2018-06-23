---
title: 新建链接的报表页 （报表管理器） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2014
ms.assetid: fefb46e8-6901-4d50-a3f8-7c49ad72e7b1
caps.latest.revision: 22
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 635352076fac4e993ce7a46e3b66c2e1089f6b59
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018552"
---
# <a name="new-linked-report-page-report-manager"></a>“新建链接报表”页（报表管理器）
  使用“新建链接报表”页可以创建链接报表。 链接报表是指具有自己的设置和属性、但链接到其他报表的报表定义的报表。 如果您有一个基础报表并且希望在它的基础上针对特定组或特定用户加以改动，则链接报表很有用；根据您指定为参数的区域代码返回不同数据的区域报表便是链接报表的一个例子。 链接报表通常是通过参数化报表创建。如果您希望每个报表具有不同的参数值，则可以为每个报表实例保存不同的参数值以创建参数化报表。 不过，您也可以通过有权访问的任何报表创建链接报表。  
  
 链接报表可以具有自己的名称、说明、位置、参数属性、报表执行属性、报表历史记录属性、权限和订阅。 但是，链接报表必须使用提供报表定义的基础报表的数据源属性和布局。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-new-linked-report-page-from-the-contents-page"></a>从“内容”页打开“新建链接报表”页  
  
1.  打开报表管理器，找到要创建链接报表的报表。  
  
2.  悬停在该报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“创建链接报表”**。  
  
###### <a name="to-open-the-new-linked-report-page-from-the-general-properties-page-of-a-report"></a>从报表的“常规属性”页打开“新建链接报表”页  
  
1.  打开报表管理器，找到要创建链接报表的报表。  
  
2.  悬停在该报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”**。 这会打开该报表的“常规”属性页。  
  
4.  在项工具栏中，单击 **“创建链接报表”**。  
  
## <a name="options"></a>“常规”  
 **名称**  
 指定链接报表的名称。 名称必须至少包含一个字母数字字符。 还可以包含空格和某些符号。 但是，指定名称时不得使用字符 ; ? : @ & = +，$ / * \< > |"或 / 指定一个名称。  
  
 **Description**  
 键入对报表内容的说明。 有权访问该报表的用户可以在“内容”页中查看此说明。  
  
 **位置**  
 指定包含该报表的文件夹路径。 默认情况下，链接报表创建时位于基础报表所在的文件夹中。 单击 **“更改位置”** 可以将链接报表放入其他文件夹。  
  
 **确定**  
 单击 **“确定”** 可以保存更改并返回基础报表的“常规”属性页。  
  
## <a name="see-also"></a>请参阅  
 [创建链接的报表](reports/create-a-linked-report.md)   
 [报表的“常规”属性页（报表管理器）](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  