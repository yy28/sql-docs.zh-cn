---
title: 报表历史记录页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4c64e58a-ed83-4e29-a422-9baaac2be4b8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0b5865ecbca2ea5577fccf0c28faeabf27b9573d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48053137"
---
# <a name="report-history-page-report-manager"></a>“报表历史记录”页（报表管理器）
  使用“报表历史记录”页可以查看一段时间中生成并存储的报表快照。 根据报表服务器上设置的选项，报表历史记录可能只包含较新的快照。  
  
 报表历史记录总是显示在所源于的报表的上下文中。 您不能一起查看报表服务器中所有报表的历史记录。  
  
 要生成报表历史记录，报表必须能够以无人参与的方式运行（也就是说，报表必须使用存储的凭据；参数化报表必须包含所有参数的默认参数值）。 可以手动或以计划操作方式生成报表历史记录。 报表的历史记录属性决定报表历史记录的创建方式。  
  
 您可以通过单击报表历史记录快照来查看它。 报表历史记录中显示的快照只能通过创建的日期和时间来区分。 无法通过直观方式判断出某个快照是为响应计划而生成的还是为响应某个手动操作而生成的。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关的各版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅[SQL Server 2014 各个版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
### <a name="to-open-the-report-history-page"></a>打开“报表历史记录”页  
  
1.  打开报表管理器，找到要查看报表快照的报表。  
  
2.  悬停在该报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“查看报表历史记录”**。  
  
## <a name="options"></a>选项  
 **删除**  
 单击此选项可删除一个或多个快照。 在单击 **“删除”** 之前，请选中要删除的快照旁的复选框。  
  
 **新的快照**  
 单击此选项可向报表历史记录中添加快照。 如果在报表的“历史记录”属性页上选择了 **“允许手动创建历史记录”** 选项，则此按钮可用。  
  
 **上次运行时间**  
 显示快照创建的日期和时间。 单击说明可以查看某个特定的快照。  
  
 **大小**  
 显示报表定义及报表中的数据的总大小。 此值指示报表定义和数据所占用的报表服务器数据库的空间。 呈现的报表的大小（包括格式）实际偏大。 括号中的总大小是当前报表的报表历史记录中所有快照大小的总和。  
  
## <a name="see-also"></a>请参阅  
 [查看或删除报表历史记录&#40;报表管理器&#41;](../../2014/reporting-services/view-or-delete-report-history-report-manager.md)   
 [将快照添加到报表历史记录&#40;报表管理器&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [报表的“常规”属性页（报表管理器）](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [快照选项属性页&#40;报表管理器&#41;](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md)  
  
  
