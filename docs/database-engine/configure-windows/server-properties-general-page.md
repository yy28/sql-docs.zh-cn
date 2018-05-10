---
title: 服务器属性（“常规”页）- SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.setsapassword.f1
- sql13.swb.serverproperties.activedirectory.f1
- sql13.swb.serverproperties.prodinfo.f1
ms.assetid: 10ac57f1-b4bd-4528-bb66-3e47ccf663e7
caps.latest.revision: 30
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 34c019dfd0d4fd443c61eb0993359dd63883ffa5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="server-properties---general-page"></a>服务器属性 -“常规”页
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用此页可以查看有关 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装的只读信息。  
  
## <a name="property-grid"></a>属性网格  
 查看所选服务器的属性，例如服务器名称、服务器操作系统或处理器数。  
  
 **名称**  
 显示服务器实例的名称。  
  
 **Product**  
 显示当前运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本。  
  
 **操作系统**  
 显示当前运行的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 操作系统。  
  
 **平台**  
 说明运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的操作系统和硬件。  
  
 **版本(Version)**  
 显示当前运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的版本号。  
  
 **语言**  
 显示正在运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例支持的语言。  
  
 **内存**  
 列出服务器上安装的内存量。  
  
 **Processors**  
 显示安装的 CPU 数。  
  
 **根目录**  
 显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例所在位置的路径，通常为 C:\Program Files\Microsoft SQL Server\\。  
  
 **服务器排序规则**  
 显示服务器支持的排序规则。 排序规则指定用于 Unicode 数据和非 Unicode 数据的特定代码页和排序顺序。  
  
 **已群集化**  
 如果在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集中配置了该服务器实例，则显示“True”；如果未群集该服务器实例，则显示“False”。  
  
 **启用 HADR**  
 如果启用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 功能，则显示“True”；如果禁用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 功能，则显示“False”。 有关启用或禁用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 的详细信息，请参阅[启用和禁用 AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)。  
  
## <a name="description-field"></a>说明字段  
 查看服务器属性的其他信息。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
