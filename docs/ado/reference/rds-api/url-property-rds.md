---
title: URL 属性（RDS） |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- URL property [ADO]
ms.assetid: 8c56b233-1be8-442c-8d0e-a4c96465bc99
author: rothja
ms.author: jroth
ms.openlocfilehash: 09785fde3531d50f33064415ddc769eb07f0fec2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750529"
---
# <a name="url-property-rds"></a>URL 属性 (RDS)
指示一个字符串，该字符串包含相对或绝对 URL。  
  
 可以在设计时在[DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的对象标记中设置 URL 属性，也可以在运行时在脚本代码中设置**URL**属性。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>参数  
 *服务器*  
 一个**字符串**值，该值包含有效的 URL。  
  
 *DataControl*  
 表示**DataControl**对象的对象变量。  
  
## <a name="remarks"></a>备注  
 通常，URL 会标识一个活动服务器页（.asp）文件，该文件可生成并返回[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。 因此，用户可以获取**记录集**，而无需调用服务器端[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象，也无需编写自定义业务对象。  
  
 如果已设置**url**属性， [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)会将更改提交到 url 指定的位置。  
  
## <a name="applies-to"></a>应用于  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [URL 属性示例 (VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)


