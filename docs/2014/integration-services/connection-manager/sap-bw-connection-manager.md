---
title: SAP BW 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 06b166a1-a9df-48ea-a0e8-9b8d6979c0a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b3ee629cd7701d8b06351e8932daac57637b195e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833668"
---
# <a name="sap-bw-connection-manager"></a>SAP BW 连接管理器
  SAP BW 连接管理器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的连接管理器组件。 因此，SAP BW 连接管理器提供 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的源组件和目标组件所需的与 SAP Netweaver BW 版本 7 系统连接的能力。 （SAP BW 源组件和目标组件作为 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 包的一部分，是唯一采用 SAP BW 连接管理器的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件。）  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
 当将 SAP BW 连接管理器添加到包中时，连接管理器的 `ConnectionManagerType` 属性被设为 `SAPBI`。  
  
## <a name="configuring-the-sap-bw-connection-manager"></a>配置 SAP BW 连接管理器  
 可以按下列方式配置 SAP BW 连接管理器：  
  
-   输入连接的客户端、用户名、密码和语言。  
  
-   选择连接单个应用程序服务器还是连接一组负载平衡服务器。  
  
-   如果是单个应用程序服务器，需提供主机和系统编号，如果是一组负载平衡的服务器，需提供消息服务器、组和 SID。  
  
-   启用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 组件的 RFC 函数调用自定义日志记录。 （此日志记录与可对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包启用的可选日志记录是分开进行的。）要启用 RFC 函数调用日志记录，可以指定一个目录用来存储每次 RFC 函数调用前后创建的日志文件。 （此日志记录功能会创建许多个 XML 格式的日志文件。 这些日志文件还包含传输的所有数据行，因此可能会消耗大量的磁盘空间。）如果不选择日志目录，则不启用日志记录功能。  
  
    > [!IMPORTANT]  
    >  如果传输的数据包含敏感信息，日志文件中也会包含该敏感信息。  
  
-   使用您输入的值来测试连接。  
  
 如果您不知道配置连接管理器所需的所有值，可能需要询问您的 SAP 管理员。  
  
 有关演示如何配置和使用 SAP BW 连接管理器、源和目标的演练，请参阅白皮书 [将 SQL Server 2008 Integration Services 与 SAP BI 7.0 一起使用](https://go.microsoft.com/fwlink/?LinkID=137090)。 此白皮书还说明如何在 SAP BW 中配置所需的对象。  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>使用 SSIS 设计器配置源  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的 SAP BW 连接管理器属性的详细信息，请单击以下主题：  
  
-   [SAP BW 连接管理器编辑器](../sap-bw-connection-manager-editor.md)  
  
## <a name="see-also"></a>请参阅  
 [Microsoft Connector 1.1 for SAP BW 组件](../microsoft-connector-for-sap-bw-components.md)  
  
  
