---
title: URL 属性 (RDS) |Microsoft 文档
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- URL property [ADO]
ms.assetid: 8c56b233-1be8-442c-8d0e-a4c96465bc99
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e798b7e4afd6ddf0e2238acff56adcff0a3cfb5c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="url-property-rds"></a>URL 属性 (RDS)
指示一个字符串，包含相对或绝对 URL。  
  
 你可以设置**URL**在设计时属性[DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的对象标记，或在运行时中的脚本代码。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>Parameters  
 *Server*  
 A**字符串**包含有效的 URL 的值。  
  
 *DataControl*  
 表示的对象变量**DataControl**对象。  
  
## <a name="remarks"></a>注释  
 通常情况下，URL 标识的 Active Server Page (.asp) 文件，可以生成返回[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。 因此，用户可以获取**记录集**而无需调用服务器端[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象，或程序的自定义业务对象。  
  
 如果**URL**已设置属性， [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)将将更改提交到 URL 指定的位置。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [URL 属性示例 (VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)


