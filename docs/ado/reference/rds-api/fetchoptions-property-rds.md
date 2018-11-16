---
title: FetchOptions 属性 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19b266474c348af50db26fddafeea79d4cf33ade
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602557"
---
# <a name="fetchoptions-property-rds"></a>FetchOptions 属性 (RDS)
指示异步获取数据的类型。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="setting-and-return-values"></a>设置和返回值  
 设置或返回以下值之一。  
  
|常量|Description|  
|--------------|-----------------|  
|**adcFetchUpFront**|中的所有记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)在控制返回到应用程序之前提取。 完整**记录集**提取之前允许该应用程序以使用它执行任何操作。|  
|**adcFetchBackground**|只要已提取的记录的第一批，控件可以返回到应用程序。 后续读取**记录集**尝试访问未获取第一个批处理中的记录将延迟到实际提取所发现的记录，同时控制将返回到应用程序。|  
|**adcFetchAsync**|默认值。 控件立即返回到应用程序时在后台提取记录。 如果应用程序尝试读取尚未获取一条记录，将读取所发现的记录与最接近的记录并控制会立即返回，该值指示当前末尾**记录集**达到了。 例如，调用[MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)将使当前记录位置移动到最后一个记录实际提取，即使多个记录将继续填充**记录集**。|  
  
> [!NOTE]
>  使用这些常量在每个客户端的可执行文件必须提供其声明。 您可以剪切并粘贴您要从文件 Adcvbs.inc，位于 RDS 库的默认安装文件夹中的常量声明。  
  
## <a name="remarks"></a>备注  
 在 Web 应用程序，通常要使用**adcFetchAsync** （默认值），因为它提供了更好的性能。 在已编译的客户端应用程序中，通常要使用**adcFetchBackground**。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [ExecuteOptions 和 FetchOptions 属性示例 (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


