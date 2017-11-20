---
title: "安装 Microsoft Connector for SAP BW |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 663ae1f9c71987729b96510157ce39868490f00b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="installing-the-microsoft-connector-for-sap-bw"></a>安装 Microsoft Connector for SAP BW
  [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW for SQL Server 2016 是 SQL Server 2016 功能包的一个组件。 若要安装 Connector for SAP BW 及其文档，请从 [SQL Server 2016 功能包网页](http://go.microsoft.com/fwlink/?LinkId=746297)下载并运行安装程序。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector for SAP BW 的文档假定你熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
> [!IMPORTANT]  
>  从 SAP Netweaver BW 提取数据要求额外的 SAP 许可。 请向 SAP 核实以便确认这些要求。  
  
## <a name="required-sap-files"></a>必需的 SAP 文件  
 若要使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW，你不必在本地计算机上安装 SAP 前端软件 (SAP GUI)。  
  
 但是，必须将 SAP .NET 连接器文件 librfc32.dll 复制到 Windows 文件夹的系统子文件夹中。 （通常，此文件夹位置为 **C:\Windows\system32**。）  
  
## <a name="considerations-for-64-bit-computers"></a>针对 64 位计算机的注意事项  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW 完全支持 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 的 64 位版本。 在 64 位计算机上， [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW 具有以下附加要求：  
  
-   若要在任何 64 位 Windows 操作系统上的 64 位模式中运行包，请将 SAP GUI 文件 librfc32.dll 的 64 位版本复制到 Windows 文件夹的 **system32** 文件夹中。 （通常，此文件位置为 **C:\Windows\system32**。）  
  
-   若要在任何 64 位 Windows 操作系统上的 32 位模式中运行包，请将 SAP GUI 文件 librfc32.dll 复制到 Windows 文件夹的 **SysWow64** 文件夹中。 （通常，此文件夹位置为 **C:\Windows\SysWow64**。）  
  
  

