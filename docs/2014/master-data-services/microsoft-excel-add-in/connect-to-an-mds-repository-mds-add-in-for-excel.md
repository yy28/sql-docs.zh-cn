---
title: 连接 MDS 存储库 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8f427312-4c09-4c8b-b9f9-8b235557a74b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 5f29cdaad3f362c190372ec510f24cb67efe15f7
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84961387"
---
# <a name="connect-to-an-mds-repository-mds-add-in-for-excel"></a>连接 MDS 存储库（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，你必须先连接到 MDS 存储库，然后才能加载或发布数据。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   **** 您必须有权访问“资源管理器”功能区域。  
  
### <a name="to-connect-to-an-mds-repository"></a>连接 MDS 存储库  
  
1.  在 MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中的 **“主数据”** 选项卡上的 **“连接并加载”** 组中，单击 **“连接”** 按钮下的箭头，然后单击 **“管理连接”**。  
  
2.  在 **“管理连接”** 对话框上的 **“新建连接”** 部分中，单击 **“创建新连接”**。  
  
3.  单击 **“新建”**。  
  
4.  在 **“添加新连接”** 对话框的 **“描述”** 字段中，键入您的连接说明。 在您单击工具栏上的 **“连接”** 按钮后将显示此连接。  
  
5.  在“MDS 服务器地址”框中，键入 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序的 URL，例如 http://contoso/mds****。  
  
    > [!NOTE]  
    >  确保使用计算机名称；而不要使用“localhost”。  
  
6.  单击“确定”。 名称将显示在 **“现有连接”** 部分中。  
  
7.  还可以单击 **“测试”** 对连接进行测试。 将显示一个确认或错误对话框。 单击 **“确定”** 将其关闭。  
  
8.  单击“连接”。 随即显示 **Master Data Services** 窗格。  
  
## <a name="next-steps"></a>后续步骤  
  
-   [将数据从 MDS 加载到 Excel](export-data-to-excel-from-master-data-services.md)  
  
-   [在加载 &#40;MDS Add-in for Excel 前筛选数据&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>另请参阅  
 [连接（用于 Excel 的 MDS 外接程序）](connections-mds-add-in-for-excel.md)  
  
  
