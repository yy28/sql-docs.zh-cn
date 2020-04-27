---
title: 报表服务器项属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- item-specific properties [Reporting Services]
- report items [Reporting Services], properties
- items [Reporting Services], properties
ms.assetid: 21edec6d-9897-48fb-8c75-182305b1dbdb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6ed8a56892cfd70b43341ffff8349faa56094a97
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62519137"
---
# <a name="report-server-item-properties"></a>报表服务器项属性
  项属性是特定于报表服务器数据库中的项的属性。 此类属性包括报表、链接报表、文件夹、资源、模型和数据源。  
  
 以下项属性名称是保留名称。 您不能创建具有相同名称的用户定义属性。 您可以使用报表服务器 Web 服务方法读取或修改其中的许多属性。  
  
## <a name="item-properties"></a>项属性  
 以下属性应用于报表服务器数据库中的所有项。  
  
|属性|说明|  
|--------------|-----------------|  
|**System.createdby**|最初将项添加到报表服务器数据库的用户的名称。|  
|**CreationDate**|将项添加到报表服务器数据库的日期和时间。|  
|**说明**|项的说明。|  
|**Hidden**|一个值，指示项对于用户是否可见以及是否可供用户使用。|  
|**ID**|报表服务器数据库中项的 ID。|  
|**ModifiedBy**|最后对报表服务器数据库中的项进行修改的用户的名称。|  
|**ModifiedDate**|用户最后修改该项的日期和时间。|  
|**名称**|报表服务器数据库中项的名称。|  
|**路径**|项的完整路径名称。 报表服务器数据库中任何项的路径都具有最大字符长度 260。|  
|**大小**|报表服务器数据库中项的大小，以字节为单位。|  
|**类型**|报表服务器数据库中项的类型。|  
|**VirtualPath**|指向报表服务器数据库中项的虚拟路径。 <xref:ReportService2010.CatalogItem.VirtualPath%2A> 属性的值是用户在其下应看到该项的路径。 例如，名为 report1 的报表位于用户的个人“我的报表”文件夹中，它具有虚拟路径 /My Reports。 该项的实际路径是 /Users/username/My Reports。|  
  
## <a name="folder-properties"></a>文件夹属性  
 除了前面列出的项属性外，以下属性应用于报表服务器数据库中的文件夹。  
  
|属性|说明|  
|--------------|-----------------|  
|**保留**|<xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法为报表服务器保留的文件夹返回的值。 保留文件夹包括 Users、My Reports 和 /。 保留文件夹不能修改或删除。|  
  
## <a name="report-properties"></a>报表属性  
 除了前面列出的项属性外，以下属性应用于报表服务器数据库中的报表。  
  
|属性|说明|  
|--------------|-----------------|  
|**语言**|在报表中使用的语言。 该值是在 Internet 工程任务组 (IETF) RFC1766 规范中定义的语言代码。 第一部分由两个字符构成，指定基本语言。 第二部分由连字符分隔，指定语言的变化形式或变体。 如果未在与报表定义中的 `Style` 元素相关联的 `Body` 元素中指定某一值，则默认值是该报表服务器的语言。|  
|`ReportProcessingTimeout`|以秒为单位的单独报表的超时值。 如果设置了该值，则经过指定时间后报表服务器会尝试停止处理报表。 有效值为 `-1` 到 `2`、`147`、`483`、`647`。 如果值为 `-1`，则处理期间报表不会超时。 如果值为`null`，则系统属性`ReportProcessingTimeout`的值用于报表处理超时。默认值为`null`。 有关详细信息，请参阅[报表服务器系统属性](reporting-services-properties-report-server-system-properties.md)。|  
|**ExecutionDate**|为报表最后创建报表快照的日期和时间。|  
|**CanRunUnattended**|一个值，指示报表是否可按照时间表以无人参与的方式运行。 如果该属性设置为 `true`，则定义报表参数的默认值，并且数据源凭据将与报表一起存储，或者凭据检索选项设置为 `None`。 如果该属性设置为 `false`，则未满足以无人参与的方式运行报表的先决条件。 有关详细信息，请参阅[配置无人参与的执行帐户（SSRS 配置管理器）](../../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。|  
|**HasParameterDefaultValues**|一个值，指示报表是否为所有报表参数都设置了有效的默认值。 如果某一报表没有报表参数，该值也是 `true`。 如果该属性设置为 `false`，则一个或多个报表参数没有有效的默认值。|  
|HasDataSourceCredentials****|一个值，指示为与报表相关联的所有数据源设置的凭据检索选项是 `None` 或 `Store`。 如果该属性设置为 `false`，则为与报表相关联的某一数据源设置的凭据检索选项是 `Integrated` 或 `Prompt`。|  
|**IsSnapshotExecution**|一个值，用于指示报表是否为快照。|  
|**HasScheduleReadyDataSources**|一个值，指示是否将报表的数据源配置为支持计划的执行。 如果该属性设置为 `false`，则用户无法订阅该报表。|  
  
## <a name="resource-properties"></a>资源属性  
 除了前面列出的项属性外，以下属性应用于报表服务器数据库中的资源。  
  
|属性|说明|  
|--------------|-----------------|  
|**MimeType**|报表服务器数据库中资源的 MIME 类型。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../report-server-web-service.md)   
 [技术参考 (SSRS)](../../technical-reference-ssrs.md)  
  
  
