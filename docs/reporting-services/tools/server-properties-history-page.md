---
title: 服务器属性（“历史记录”页）| Microsoft Docs
ms.date: 06/10/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f4f3c13e6393dc935c09d54a274d2dbe357401f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571361"
---
# <a name="server-properties-history-page"></a>服务器属性（“历史记录”页）
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 中使用此 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 页可设置要保留的报表历史记录副本数的默认值。 该默认值为所有报表提供建立报表历史记录限制的初始设置。 可以针对不同的报表采用不同的设置。  
  
 报表历史记录是一系列报表快照，这些快照中包括创建快照时报表的数据和布局。 可以使用报表历史记录来保留报表在特定日期或时间的副本。 可以为在处于本机模式的报表服务器上或配置了 SharePoint 集成模式的报表服务器上运行的单个报表创建和管理报表历史记录。  
  
 报表历史记录快照存储在报表服务器数据库中。 如果要保留无限多个快照，请确保定期检查数据库大小，确保它的增长速度不会过快或占用太多的磁盘空间。  
  
 若要打开此页，请执行以下操作：
 1) 启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
 2) 连接到报表服务器实例。
 3) 右键单击报表服务器名称，然后选择“属性”  。
 4) 单击 **“历史记录”** 将此页打开。  
  
## <a name="options"></a>选项  
 **不限制报表历史记录中保留的快照数**  
 保留所有的报表历史记录快照。 要减少报表历史记录的大小，必须手动删除快照。  
  
 **限制报表历史记录的副本数**  
 保留设定数量的报表历史记录快照。 到达限制后，将从报表历史记录中删除较旧的副本以便为新副本腾出空间。  
  
 如果以后限制报表历史记录，则在现有的报表历史记录超出您指定的限制时，报表服务器将减少现有的报表历史记录以符合新限制。 首先删除最旧的报表快照。 如果报表历史为空或者低于限制，则添加新的报表快照。 到达限制后，将在添加新的报表快照时删除时间最早的快照。  
  
## <a name="see-also"></a>另请参阅  
 [设置报表服务器属性 (Management Studio)](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [在 Management Studio 中连接到报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Management Studio 中报表服务器的 F1 帮助](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
