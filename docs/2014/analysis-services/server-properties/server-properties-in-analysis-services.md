---
title: 在 Analysis Services 中配置服务器属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, configuration properties
- Analysis Services, configuration properties
- SQL Server Analysis Services, configuration properties
- configuration options [Analysis Services]
- server properties [Analysis Services]
- properties [Analysis Services], configuration
- properties [Analysis Services]
ms.assetid: 274b89cd-14ed-4666-bc13-eedf1de51e18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 31c05bbc1be8376144eb191ff28a9cdc6eebdd8a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068903"
---
# <a name="configure-server-properties-in-analysis-services"></a>在 Analysis Services 中配置服务器属性
  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理员可以修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的默认服务器配置属性。 每个实例都有自己的配置属性，可以独立于同一服务器上的其他实例进行设置。  
  
 若要设置服务器属性，请使用 SQL Server Management Studio 或编辑特定实例的 msmdsrv.ini 文件。  
  
 本主题包含以下各节：  
  
 [配置服务器（实例）属性](#bkmk_config)  
  
 [服务器属性参考](#bkmk_ref)  
  
##  <a name="bkmk_config"></a>配置服务器（实例）属性  
 SQL Server Management Studio 中的属性页包含一部分可用的属性，仅显示可能要修改的那些属性。 msmdsrv.ini 文件中提供了一组完整的属性。  
  
> [!NOTE]  
>  本主题未说明 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的部署配置属性。 有关部署配置的详细信息，请参阅[为解决方案部署指定配置设置](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)。  
  
#### <a name="view-or-set-configuration-properties-in-management-studio"></a>在 Management Studio 中查看或设置配置属性  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。  
  
     在对象资源管理器中，右键单击 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，再单击****“属性”。 随即出现“常规”页，显示更为常用的属性。  
  
2.  若要查看更多属性，请选中该页底部的****“显示高级(全部)属性”复选框。  
  
     只有表格模式服务器和多维模式服务器才支持修改服务器属性。 如果安装了 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]，请始终使用默认值，除非 Microsoft 产品支持工程师另有说明。  
  
     对于如何通过属性解决操作或性能问题的指导，请参阅 [SQL Server 2008 R2 Analysis Services 操作指南](https://go.microsoft.com/fwlink/?LinkID=225539)。  
  
     也可以在 Microsoft 白皮书 [SQL Server 2005 Analysis Services (SSAS) Server Properties](https://go.microsoft.com/fwlink/?LinkID=199102)（SQL Server 2005 Analysis Services (SSAS) 服务器属性）中查阅服务器属性（这些属性在最近几个版本中大多没有发生变化）的信息。  
  
    > [!NOTE]  
    >  某些属性只能在 msmdrsrv.ini 文件中进行设置。 如果在显示高级属性后仍然看不见要设置的属性，则可能需要直接编辑 msmdsrv.ini 文件。  
  
#### <a name="view-or-edit-configuration-properties-in-the-msmdsrvini-file"></a>在 msmdsrv.ini 文件中查看或编辑配置属性  
  
1.  开始之前，请在 Management Studio 的“常规”属性页中检查 **DataDir** 属性以确认 Analysis Services 程序文件（包括 msmdsrv.ini 文件）的位置。 确认程序文件位置可确保您修改的就是所需的文件。  
  
    > [!NOTE]  
    >  在默认安装中，该文件可能位于 \Program Files\Microsoft SQL Server\MSAS12.MSSQLSERVER\OLAP\Config 文件夹中。  
  
2.  创建该文件的备份，以备将来恢复原始文件时使用。  
  
3.  使用文本编辑器查看或编辑 msmdsrv.ini 文件。  
  
4.  在保存该文件后，您必须重新启动该服务。  
  
##  <a name="bkmk_ref"></a>服务器属性参考  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置属性对于微调系统非常重要。 例如，为了使查询日志行为与您的要求相一致，您可以设置相关的属性。  
  
 以下主题介绍了各种 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置属性：  
  
|主题|说明|  
|-----------|-----------------|  
|[常规属性](general-properties.md)|常规属性既是基本属性，又是高级属性，包括定义数据目录、备份目录和其他服务器行为的属性。|  
|[数据挖掘属性](data-mining-properties.md)|数据挖掘属性控制着启用和禁用哪些数据挖掘算法。 默认情况下，启用所有算法。|  
|DSO|不再支持 DSO。 忽略 DSO 属性。|  
|[功能属性](feature-properties.md)|功能属性与产品功能有关，大多数是高级属性，包括控制服务器实例之间的链接的属性。|  
|[FileStore 属性](filestore-properties.md)|文件存储属性仅用于高级用途。 其中包括高级内存管理设置。|  
|[锁管理器属性](lock-manager-properties.md)|锁管理器属性定义与锁定和超时有关的服务器行为。 这些属性多数仅适用于高级用途。|  
|[日志属性](log-properties.md)|日志属性控制是否在服务器上记录事件以及记录事件的位置和方式。 其中包括错误日志记录、异常日志记录、网络流量记录器、查询日志记录和跟踪。|  
|[内存属性](memory-properties.md)|内存属性控制服务器如何使用内存。 这些属性主要用于高级用途。|  
|[网络属性](network-properties.md)|网络属性控制与网络有关的服务器行为，包括控制压缩和二进制 XML 的属性。 这些属性多数仅适用于高级用途。|  
|[OLAP 属性](olap-properties.md)|OLAP 属性控制多维数据集和维度处理、迟缓处理、数据缓存和查询行为。 其中既包括基本属性，也包括高级属性。|  
|[安全属性](security-properties.md)|安全部分包含定义访问权限的基本属性和高级属性。 其中包括与管理员和用户有关的设置。|  
|[线程池属性](thread-pool-properties.md)|线程池属性控制服务器创建多少线程。 这些属性主要是高级属性。|  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 实例管理](../instances/analysis-services-instance-management.md)   
 [为解决方案部署指定配置设置](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
