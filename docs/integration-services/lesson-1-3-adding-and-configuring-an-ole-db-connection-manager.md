---
title: 步骤 3：添加和配置 OLE DB 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3fbb4994b1f7f7416fbdbdde5dc6377b396dae9a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52539072"
---
# <a name="lesson-1-3---adding-and-configuring-an-ole-db-connection-manager"></a>第 1-3 课 - 添加和配置 OLE DB 连接管理器
添加了用于连接到数据源的平面文件连接管理器以后，下一个任务是添加用于连接到目标的 OLE DB 连接管理器。 通过 OLE DB 连接管理器，包可以在任何 OLE DB 兼容的数据源中提取数据或加载数据。 使用 OLE DB 连接管理器，可以为连接指定服务器、身份验证方法和默认数据库。  
  
在本课中，将创建使用 Windows 身份验证的 OLE DB 连接管理器，以连接到 **AdventureWorksDB2012**的本地实例。 本教程以后要创建的其他组件（如查找转换和 OLE DB 目标）也将引用此处创建的 OLE DB 连接管理器。  
  
### <a name="add-and-configure-an-ole-db-connection-manager-to-the-ssis-package"></a>向 SSIS 包中添加 OLE DB 连接管理器并对其进行配置  
  
1.  右键单击“连接管理器”区域中的任意位置，再单击“新建 OLE DB 连接”。  
  
2.  在 **“配置 OLE DB 连接管理器”** 对话框中，单击 **“新建”**。  
  
3.  在“服务器名称”中，输入 **localhost**。  
  
    将 localhost 指定为服务器名称时，连接管理器将连接到本地计算机上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的默认实例。 若要使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的远程实例，请将 localhost 替换为要连接到的服务器的名称。  
  
4.  在“登录到服务器”组中，确认选择了“使用 Windows 身份验证”。  
  
5.  在“连接到数据库”组的“选择或输入数据库名称”框中，输入或选择“AdventureWorksDW2012”。  
  
6.  单击“测试连接”，验证指定的连接设置是否有效。  
  
7.  单击“确定” 。  
  
8.  单击“确定” 。  
  
9. 在“配置 OLE DB 连接管理器”对话框的“数据连接”窗格中，确认选择了“localhost.AdventureWorksDW2012”。  
  
10. 单击“确定” 。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[步骤 4：将数据流任务添加到包](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>另请参阅  
[OLE DB 连接管理器](../integration-services/connection-manager/ole-db-connection-manager.md)  
  
