---
title: "处理程序属性 (RDS) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 25ac7c676fbab1e8b5899a3502fab2199b0afd22
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="handler-property-rds"></a>处理程序属性 (RDS)
指示扩展的功能的服务器端自定义程序 （处理程序） 名称[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)，和使用的任何参数*处理程序*。  
  
 **适用于：** [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataControl*  
 表示的对象变量[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *字符串*  
 A**字符串**值，包含名称的处理程序和任何参数，所有其用逗号隔开 (例如， `"handlerName,parm1,parm2,...,parm` *N*`"`)。  
  
## <a name="remarks"></a>注释  
 此属性支持[自定义](../../../ado/guide/remote-data-service/datafactory-customization.md)，一种功能，需要设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性**adUseClient**。  
  
 名称的处理程序，它的参数，如果有的话，之间用逗号 （"，"）。 如果分号，将会导致不可预知的行为 （";"） 中的任何位置显示*字符串*。 你可以编写你自己的处理程序，提供它支持**IDataFactoryHandler**接口。  
  
 默认处理程序的名称是**MSDFMAP。处理程序**，其默认参数就是一个名为的自定义文件和**MSDFMAP。INI**。 使用此属性来调用由服务器管理员创建的备用自定义项文件。  
  
 设置的替代**处理程序**属性是一个处理程序和中的使用参数指定[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性; 也就是说，"**处理程序 =** *handlerName，parameter1、 parameter2...;*".  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [处理程序属性示例 (VB)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [DataFactory 自定义项](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)



