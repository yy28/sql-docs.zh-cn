---
title: 安装 Microsoft Connector for 1.1 SAP BW |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ff4176fabb78aede03ca04fdf64fc52085431c9b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37248789"
---
# <a name="installing-the-microsoft-connector-for-11-sap-bw"></a>安装 Microsoft Connector for 1.1 SAP BW
  若要安装[!INCLUDE[msCoName](../includes/msconame-md.md)]Connector 1.1 for SAP BW 及其文档，下载并从 SQL Server 功能包网页运行 Windows 安装程序包。  
  
> [!IMPORTANT]  
>  针对 Microsoft Connector 1.1 for SAP BW 的文档假定您熟悉 SAP Netweaver BW 环境。 有关 SAP NetWeaver BW 的详细信息，或者有关如何配置 SAP Netweaver BW 对象和过程的信息，请参阅您的 SAP 文档。  
  
> [!IMPORTANT]  
>  从 SAP Netweaver BW 提取数据要求额外的 SAP 许可。 请向 SAP 核实以便确认这些要求。  
  
## <a name="required-sap-files"></a>必需的 SAP 文件  
 若要使用[!INCLUDE[msCoName](../includes/msconame-md.md)]Connector 1.1 for SAP BW，你无需在本地计算机上安装 SAP 前端软件 (SAP GUI)。  
  
 但是，必须将 SAP .NET 连接器文件 librfc32.dll 复制到 Windows 文件夹的系统子文件夹中。 （通常，此文件夹位置为 **C:\Windows\system32**。）  
  
## <a name="considerations-for-64-bit-computers"></a>针对 64 位计算机的注意事项  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW 完全支持 64 位版本的[!INCLUDE[msCoName](../includes/msconame-md.md)]Windows。 64 位计算机上， [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW 具有以下附加要求：  
  
-   若要在任何 64 位 Windows 操作系统上的 64 位模式中运行包，请将 SAP GUI 文件 librfc32.dll 的 64 位版本复制到 Windows 文件夹的 **system32** 文件夹中。 （通常，此文件位置为 **C:\Windows\system32**。）  
  
-   若要在任何 64 位 Windows 操作系统上的 32 位模式中运行包，请将 SAP GUI 文件 librfc32.dll 复制到 Windows 文件夹的 **SysWow64** 文件夹中。 （通常，此文件夹位置为 **C:\Windows\SysWow64**。）  
  
  
