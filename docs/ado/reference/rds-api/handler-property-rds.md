---
title: 处理程序属性 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 653e29f8666f63cd4867b11b378ee8711f8b0508
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606437"
---
# <a name="handler-property-rds"></a>Handler 属性 (RDS)
指示服务器端自定义程序 （处理程序） 的功能进行扩展的名称[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)，并使用任何参数*处理程序*。  
  
 **适用于：** [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataControl*  
 表示的对象变量[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *String*  
 一个**字符串**值，该值包含名称的处理程序和任何参数，所有通过以逗号分隔 (例如， `"handlerName,parm1,parm2,...,parm` *N*`"`)。  
  
## <a name="remarks"></a>备注  
 此属性支持[自定义](../../../ado/guide/remote-data-service/datafactory-customization.md)，需要设置的功能[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。  
  
 名称的处理程序和其参数，如果有，用逗号分隔 （"，"）。 如果分号将会导致不可预知的行为 （";"） 中任意位置出现*字符串*。 您可以编写自己的处理程序，前提是它支持**IDataFactoryHandler**接口。  
  
 默认处理程序的名称是**MSDFMAP。处理程序**，其默认参数是一个名为的自定义项文件**MSDFMAP。INI**。 使用此属性来调用由服务器管理员创建的备用自定义项文件。  
  
 设置的替代方法**处理程序**属性是指定一个处理程序和中的参数[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性; 也就是说，"**处理程序 = * * * parameter1，处理程序名称parameter2...;*".  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [Handler 属性示例 (VB)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [自定义 DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


