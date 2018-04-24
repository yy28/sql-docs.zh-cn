---
title: FetchOptions 属性 (RDS) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 91b6a6c4c40bd3b31a539c42d89a6711953f582b
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="fetchoptions-property-rds"></a>FetchOptions 属性 (RDS)
指示异步获取数据的类型。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="setting-and-return-values"></a>设置和返回值  
 设置或返回下列值之一。  
  
|常量|Description|  
|--------------|-----------------|  
|**adcFetchUpFront**|所有记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)控制权返回给应用程序之前提取。 完整**记录集**允许应用程序使用它执行任何操作之前提取。|  
|**adcFetchBackground**|控件可以返回到应用程序，只要已提取的第一批的记录。 后续读取**记录集**尝试访问未获取第一个批处理中的记录将被延迟，直到实际提取所发现的记录，届时控件返回到应用程序。|  
|**adcFetchAsync**|默认值。 控件立即返回到应用程序时在后台提取记录。 如果应用程序尝试读取尚未获取记录，将读取接近所发现的记录的记录并控件将立即返回，该值指示当前末尾**记录集**已达到。 例如，调用[MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)将使当前记录位置移动到最后一个记录实际提取，即使更多记录将继续填充**记录集**。|  
  
> [!NOTE]
>  使用这些常量每个客户端的可执行文件必须提供其声明。 你可剪切并粘贴文件 Adcvbs.inc，位于 RDS 库的默认安装文件夹中的所需的常量声明。  
  
## <a name="remarks"></a>注释  
 在 Web 应用程序，你通常需要使用**adcFetchAsync** （默认值），因为它提供更好的性能。 在编译的客户端应用程序中，通常要使用**adcFetchBackground**。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [ExecuteOptions 和 FetchOptions 属性示例 (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


