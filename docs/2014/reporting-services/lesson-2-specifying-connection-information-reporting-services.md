---
title: 第 2 课：指定连接信息 (Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 67336ec0829c810a087ddfdcf79628408c045a76
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290175"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>第 2 课：指定连接信息 (Reporting Services)
  向“教程”项目添加报表之后，需要定义数据源，它是报表从关系数据库、多维数据库或其他资源访问数据所使用的连接信息。  
  
 在本课中，您将使用 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 示例数据库作为数据源。 本教程假定此数据库位于本地计算机上安装的默认 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 实例中。  
  
### <a name="to-set-up-a-connection"></a>设置连接  
  
1.  在中**报表数据**窗格中，单击**新建**，然后单击**数据源...**.  
  
    > [!NOTE]  
    >  如果“报表数据”窗格不可见，请单击“视图”菜单上的“报表数据”。  
  
2.  在 **“名称”** 中，键入 [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)]。  
  
3.  确保已选中“嵌入连接”。  
  
4.  在“类型”中，选择 Microsoft SQL Server。  
  
5.  在“连接字符串”中，键入以下文本：  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2012  
    ```  
  
     该连接字符串假定 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、报表服务器和 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库都已安装在本地计算机中，并且你拥有登录 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库的权限。  
  
    > [!NOTE]  
    >  如果使用的是带高级服务的 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 或命名实例，则连接字符串必须包括实例信息：  
    >   
    >  `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2012`  
    >   
    >  有关连接字符串的详细信息，请参阅[数据连接、 数据源和 Reporting Services 中的连接字符串](data-connections-data-sources-and-connection-strings-in-reporting-services.md)并[数据源属性对话框，常规](data-source-properties-dialog-box-general.md)。  
  
6.  在左窗格中单击“凭据”，然后单击“使用 Windows 身份验证(集成安全性)”。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] 数据源[!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)]添加到**报表数据**窗格。  
  
## <a name="next-task"></a>下一个任务  
 已成功定义了到 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 示例数据库的连接。 下一步，将创建报表。 请参阅[第 3 课：为表报表定义数据集&#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [报表生成器中的数据连接、数据源和连接字符串](data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
