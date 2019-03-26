---
title: 错误和事件参考 (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, events
- events [Integration Services]
- errors [Integration Services]
- Integration Services, errors
ms.assetid: cf4f0f14-8087-42d7-9b67-e4929228abd6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7f9e6845c7bcaaffc85621338a169cdaa2c10dc5
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58271269"
---
# <a name="errors-and-events-reference-integration-services"></a>错误和事件参考 (Integration Services)
  本节包含与 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]有关的多个错误和事件的相关信息。 其中包括错误消息的原因和解决方法信息。  
  
 有关 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 错误消息的详细信息（包括大多数 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 错误及其说明的列表），请参阅 [Integration Services 错误和消息引用](../integration-services/integration-services-error-and-message-reference.md)。 但列表目前不包括故障排除信息。  
  
> [!IMPORTANT]  
>  使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 时可能看到的许多错误消息来自其他组件。 其中可能包括 OLE DB 访问接口、其他数据库组件（如 [!INCLUDE[ssDE](../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ）或者其他服务或组件（如文件系统、SMTP 服务器或 Microsoft 消息队列）。 若要查找有关这些外部错误消息的信息，请参阅特定于组件的文档。  
  
## <a name="error-messages"></a>错误消息  
  
|错误的符号名称|描述|  
|----------------------------|-----------------|  
|DTS_E_CACHELOADEDFROMFILE|指示由于“缓存转换”转换正在尝试将数据写入内存中的缓存中而导致包无法运行。 但是，缓存连接管理器已将一个缓存文件加载到内存中的缓存中。|  
|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|指示由于指定的连接失败而导致包无法运行。|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|指示数据流组件正试图将 Unicode 字符串数据传递给另一个希望在对应列上使用非 Unicode 字符串数据的组件，反之亦然。|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|指示数据流组件正试图将 Unicode 字符串数据传递给另一个希望在对应列上使用非 Unicode 字符串数据的组件，反之亦然。|  
|DTS_E_CANTINSERTCOLUMNTYPE|指示由于不支持 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 列数据类型和数据库列数据类型之间的转换而导致列无法添加到数据库表中。|  
|DTS_E_CONNECTIONNOTFOUND|指示由于找不到指定的连接管理器而导致包无法运行。|  
|DTS_E_CONNECTIONREQUIREDFORMETADATA|指示 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器必须连接到数据源，以便为源或目标检索新的或更新的元数据，同时还指示它无法连接到数据源。|  
|DTS_E_MULTIPLECACHEWRITES|指示由于“缓存转换”转换正在尝试将数据写入内存中的缓存中而导致包无法运行。 但是，另一个“缓存转换”转换已将数据写入内存中的缓存中。|  
|DTS_E_PRODUCTLEVELTOLOW|指示由于未安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的适当版本而无法运行包。|  
|DTS_E_READNOTFILLEDCACHE|指示在“缓存转换”转换将数据写入缓存的同时，查找转换尝试从内存中的缓存中读取数据。|  
|DTS_E_UNPROTECTXMLFAILED|指示系统没有解密受保护的 XML 节点。|  
|DTS_E_WRITEWHILECACHEINUSE|指示在查找转换从内存中的缓存中读取数据的同时，“缓存转换”转换尝试将数据写入内存中的缓存中。|  
|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|指示数据源中的列元数据与连接到数据源的源或目标组件中的列元数据不匹配。|  
  
## <a name="events-sqlispackage"></a>事件 (SQLISPackage)  
 有关详细信息，请参阅 [由 Integration Services 包记录的事件](../integration-services/performance/events-logged-by-an-integration-services-package.md)。  
  
|事件|描述|  
|-----------|-----------------|  
|SQLISPackage_12288|指示包已启动。|  
|SQLISPackage_12289|指示包已成功完成运行。|  
|SQLISPACKAGE_12291|指示包无法完成运行即已停止。|  
|SQLISPackage_12546|指示包中的一项任务或其他可执行文件已经完成其工作。|  
|SQLISPackage_12549|指示包中引发了一条警告消息。|  
|SQLISPackage_12550|指示包中引发了一条错误消息。|  
|SQLISPackage_12551|指示包未完成其工作即已停止。|  
|SQLISPackage_12557|指示包已完成运行。|  
  
## <a name="events-sqlisservice"></a>事件 (SQLISService)  
 有关详细信息，请参阅 [由 Integration Services 服务记录的事件](../integration-services/service/events-logged-by-the-integration-services-service.md)。  
  
|事件|描述|  
|-----------|-----------------|  
|SQLISService_256|指示服务正要启动。|  
|SQLISService_257|指示服务已经启动。|  
|SQLISService_258|指示服务正要停止。|  
|SQLISService_259|指示服务已经停止。|  
|SQLISService_260|指示服务尝试启动，但却未能启动。|  
|SQLISService_272|指示在指定位置不存在配置文件。|  
|SQLISService_273|指示无法读取配置文件或配置文件无效。|  
|SQLISService_274|指示包含配置文件位置的注册表项不存在或为空。|  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../integration-services/integration-services-error-and-message-reference.md)  
  
  
