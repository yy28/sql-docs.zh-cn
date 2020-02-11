---
title: FetchOptions 属性（RDS） |Microsoft Docs
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
ms.openlocfilehash: 4e4e0943a675ef7cf3684ccddd2699fba02dac9e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964127"
---
# <a name="fetchoptions-property-rds"></a>FetchOptions 属性 (RDS)
指示异步提取的类型。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="setting-and-return-values"></a>设置和返回值  
 设置或返回以下值之一。  
  
|一直|说明|  
|--------------|-----------------|  
|**adcFetchUpFront**|在将控制权返回到应用程序之前，将提取[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)的所有记录。 在允许应用程序执行任何操作之前，将提取完整的**记录集**。|  
|**adcFetchBackground**|提取第一批记录后，控件即可返回到应用程序。 对于尝试访问第一批中未提取的记录的记录**集**，后面的记录将被延迟，直到实际提取所查找的记录为止，此时控件返回到应用程序。|  
|**adcFetchAsync**|默认值。 当在后台提取记录时，控件立即返回到应用程序。 如果应用程序尝试读取尚未提取的记录，则将读取与所查找记录最接近的记录，并且控制将立即返回，这表示已到达**记录集**的当前端。 例如，对[MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)的调用会将当前记录位置移动到实际提取的最后一条记录，即使更多记录将继续填充**记录集**。|  
  
> [!NOTE]
>  每个使用这些常量的客户端可执行文件都必须为其提供声明。 你可以从文件 Adcvbs 中剪切并粘贴所需的常量声明，该文件位于 RDS 库的默认安装文件夹中。  
  
## <a name="remarks"></a>备注  
 在 Web 应用程序中，通常需要使用**adcFetchAsync** （默认值），因为它提供更好的性能。 在已编译的客户端应用程序中，通常需要使用**adcFetchBackground**。  
  
## <a name="applies-to"></a>应用于  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [ExecuteOptions 和 FetchOptions 属性示例（VBScript）](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


