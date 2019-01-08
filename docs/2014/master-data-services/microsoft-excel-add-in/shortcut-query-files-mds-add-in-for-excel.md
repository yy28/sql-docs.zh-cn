---
title: 快捷查询文件 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 1ba0219a-6c40-41fa-aff9-8c8f41ef3220
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: e966260ac9880ffbdc722abca8eef86c5409da6a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750859"
---
# <a name="shortcut-query-files-mds-add-in-for-excel"></a>快捷查询文件（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，使用快捷查询文件可快速连接并加载常用数据。 当您要与他人共享 MDS 数据时，也可以使用这些文件。 不需要保存工作表再通过电子邮件发送，而应保存一个快捷查询文件然后通过电子邮件发送该文件。 这将确保您同时连接到 MDS 存储库，以获取最新数据。  
  
 快捷查询文件是包含以下相关信息的 XML 文件：  
  
-   MDS 存储库连接。  
  
-   模型、版本和实体。  
  
-   创建快捷方式时应用的任何筛选器。  
  
-   创建快捷方式时从左到右的列顺序。  
  
 可以将这些文件保存在一个列表中，然后在打开该外接程序时从中进行选择。 您可以将其导出到您的计算机或某个共享位置，也可以将其发送给其他人。  
  
## <a name="queryopener-application"></a>QueryOpener 应用程序  
 安装了 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 的所有用户都装有名为 QueryOpener 的应用程序。 此应用程序用于在 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中打开快捷查询文件。 如果双击快捷查询文件，将自动使用此应用程序在该外接程序中打开该文件。  
  
 使用此应用程序打开快捷查询文件时，系统会提示将该连接视为“安全”连接，这意味着你信任此位置的内容。 每次将某个连接标记为安全连接后，该连接都会添加到列表中。 如果要清空该列表，请打开 **“设置”** 对话框，然后在 **“添加到安全列表的服务器”** 部分中，单击 **“全部清除”**。  
  
 应用程序的默认位置是*驱动器*: \Program Files\Microsoft SQL Server\120\Master Data Services\Excel Add-In\Microsoft.MasterDataServices.QueryOpener.exe。  
  
 有两种方式可以打开快捷查询文件：可以导入这些文件，或通过双击自动打开这些文件。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|将活动工作表的内容另存为一个快捷查询文件。|[保存快捷查询文件（用于 Excel 的 MDS 外接程序）](save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|通过电子邮件发送表示活动工作表内容的快捷查询文件。|[以电子邮件形式发送快捷查询文件（用于 Excel 的 MDS 外接程序）](email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [连接（用于 Excel 的 MDS 外接程序）](connections-mds-add-in-for-excel.md)  
  
-   [用于 Microsoft Excel 的 Master Data Services 外接程序](master-data-services-add-in-for-microsoft-excel.md)  
  
-   [安全性 (Master Data Services)](../security-master-data-services.md)  
  
  
