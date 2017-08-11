---
title: "实现的传递扩展插件 IDeliveryExtension 接口 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
caps.latest.revision: 37
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: ac54345b14ba3ff84a755e0ce4e8b1c4e9acab13
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>为传递扩展插件实现 IDeliveryExtension 接口
  传递扩展插件类用于根据报表通知的内容将通知传递给用户。 传递扩展插件类还提供了基础结构，用于验证传递到传递扩展插件的用户设置。 此外，传递扩展插件类应包含特定的属性，客户端可以使用这些属性获得有关扩展插件的名称、扩展插件支持的设置以及可用于传递扩展插件的呈现格式的信息。  
  
 ![IDeliveryExtension 接口过程](../../../reporting-services/extensions/delivery-extension/media/bk-ext-02.gif "IDeliveryExtension 接口过程")  
IDeliveryExtension 接口允许对用户数据进行验证，以及使客户端能够了解所需的传递设置  
  
 若要创建传递扩展插件类，应实现 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 和 <xref:Microsoft.ReportingServices.Interfaces.IExtension>。 **IDeliveryExtension**接口使你的传递扩展插件，将使用的报表通知传递<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A>方法和验证使用的传入扩展设置<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A>方法。 **IExtension**接口使你传递扩展插件以实现本地化的扩展名，并以处理特定于扩展的配置信息存储在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]配置文件。 通过实现**IExtension**，传递扩展插件包含<xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A>属性。 强烈建议[!INCLUDE[ssRS](../../../includes/ssrs-md.md)]传递扩展插件支持**LocalizedName**属性，以便用户遇到的熟悉用户界面，如报表管理器中的扩展名称。  
  
 传递扩展插件还必须实现**ExtensionSettings**属性**IDeliveryExtension**接口。 报表服务器使用由 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> 属性返回的值以评估传递扩展插件所要求的设置。 与传递扩展插件交互的客户端使用报表服务器 Web 服务的 <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> 方法为传递扩展插件返回设置列表。  
  
 还可以使用传递扩展插件类检索和处理存储在 RSReportServer.config 文件中的自定义配置数据。 有关处理自定义配置数据的详细信息，请参阅 <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A> 方法。  
  
 有关示例**IDeliveryExtension**类实现，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
