---
title: 设置属性的连接管理器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], modifying
- modifying connection managers
ms.assetid: 54793114-2198-4d80-8091-e241d5a5d13c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 92ac3366a2473fb92fe33dcf884d3806c65e8609
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388255"
---
# <a name="set-the-properties-of-a-connection-manager"></a>设置连接管理器的属性
  所有连接管理器都可以使用 **“属性”** 窗口进行配置。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 还提供了用于在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中修改不同类型的连接管理器的自定义对话框。 对话框中所包含的选项集将因连接管理器类型的不同而变化。  
  
### <a name="to-modify-a-connection-manager-using-the-properties-window"></a>使用“属性”窗口修改连接管理器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 SSIS 设计器中，单击 **“控制流”** 选项卡、 **“数据流”** 选项卡或 **“事件处理程序”** 选项卡，以使 **“连接管理器”** 区域可用。  
  
4.  右键单击该连接管理器，再单击“属性”。  
  
5.  在 **“属性”** 窗口中，编辑属性值。 **“属性”** 窗口提供对在连接管理器的标准编辑器中无法配置的一些属性的访问。  
  
6.  单击“确定” 。  
  
7.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
### <a name="to-modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>使用连接管理器对话框修改连接管理器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，单击 **“控制流”** 选项卡、 **“数据流”** 选项卡或 **“事件处理程序”** 选项卡，以使 **“连接管理器”** 区域可用。  
  
4.  在“连接管理器”区域中，双击连接管理器以打开“连接管理器”对话框。 有关特定连接管理器类型以及每种类型可用的选项的信息，请参阅下表。  
  
    |“连接管理器”|选项|  
    |------------------------|-------------|  
    |[ADO 连接管理器](connection-manager/ado-connection-manager.md)|[配置 OLE DB 连接管理器](configure-ole-db-connection-manager.md)|  
    |[ADO.NET 连接管理器](connection-manager/ado-net-connection-manager.md)|[配置 ADO.NET 连接管理器](configure-ado-net-connection-manager.md)|  
    |[Analysis Services 连接管理器](connection-manager/analysis-services-connection-manager.md)|[“添加 Analysis Services 连接管理器”对话框 UI 参考](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 连接管理器](connection-manager/excel-connection-manager.md)|[Excel 连接管理器编辑器](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[文件连接管理器](connection-manager/file-connection-manager.md)|[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[多文件连接管理器](connection-manager/multiple-files-connection-manager.md)|[“添加文件连接管理器”对话框 UI 参考](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[平面文件连接管理器](connection-manager/flat-file-connection-manager.md)|[平面文件连接管理器编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)<br /><br /> [平面文件连接管理器编辑器（“列”页）](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [平面文件连接管理器编辑器（“高级”页）](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [平面文件连接管理器编辑器（“预览”页）](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[多平面文件连接管理器](connection-manager/multiple-flat-files-connection-manager.md)|[多平面文件连接管理器编辑器（“常规”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [多平面文件连接管理器编辑器（“列”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [多平面文件连接管理器编辑器（“高级”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [多平面文件连接管理器编辑器（“预览”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 连接管理器](connection-manager/ftp-connection-manager.md)|[FTP 连接管理器编辑器](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[HTTP 连接管理器](connection-manager/http-connection-manager.md)|[HTTP 连接管理器编辑器（“服务器”页）](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP 连接管理器编辑器（“代理”页）](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 连接管理器](connection-manager/msmq-connection-manager.md)|[MSMQ 连接管理器编辑器](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[ODBC 连接管理器](connection-manager/odbc-connection-manager.md)|[ODBC 连接管理器 UI 参考](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 连接管理器](connection-manager/ole-db-connection-manager.md)|[配置 OLE DB 连接管理器](configure-ole-db-connection-manager.md)|  
    |[SMO 连接管理器](connection-manager/smo-connection-manager.md)|[SMO 连接管理器编辑器](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[SMTP 连接管理器](connection-manager/smtp-connection-manager.md)|[SMTP 连接管理器编辑器](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 连接管理器](connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 连接管理器编辑器（“连接”页）](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [SQL Server Compact Edition 连接管理器编辑器（“全部”页）](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 连接管理器](connection-manager/wmi-connection-manager.md)|[WMI 连接管理器编辑器](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
5.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services (SSIS) 连接](connection-manager/integration-services-ssis-connections.md)   
 [在包中添加、删除或共享连接管理器](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)  
  
  
