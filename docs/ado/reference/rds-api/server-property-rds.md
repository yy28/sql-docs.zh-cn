---
title: Server 属性（RDS） |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d196a60986734c5717be9711af1fa28accee414
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67963474"
---
# <a name="server-property-rds"></a>Server 属性 (RDS)
指示 Internet Information Services （IIS）名称和通信协议。  
  
 您可以在设计时在 RDS 的对象标记中设置**服务器**属性[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象，或在运行时在脚本代码中运行。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
 **HTTP**  
  
 设计时语法  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 运行时语法  
  
```  
  
DataControl  
.Server="https://  
awebsrvr:port  
"  
  
```  
  
 **HTTPS**  
  
 设计时语法  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 运行时语法  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 设计时语法  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 运行时语法  
  
```  
  
DataControl.Server="computername"  
```  
  
 **进程内**  
  
 设计时语法  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 运行时语法  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>parameters  
 *awebsrvr*或*computername*  
 如果服务器位于远程计算机上，则为包含 Internet 或 intranet 路径或计算机名称的**字符串**值;或者，如果服务器在本地计算机上，则为空字符串。  
  
 *口*  
 可选。 用于连接到运行 IIS 的服务器的端口。 端口号在 Internet Explorer 中设置（在 "**视图**" 菜单上，单击 "**选项**"，然后选择 "**连接**" 选项卡）或在 IIS 中。  
  
 *DataControl*  
 表示 RDS 的对象变量 **。DataControl**对象。  
  
## <a name="remarks"></a>备注  
 服务器是 RDS 的位置 **。处理 DataControl**请求（即，查询或更新）。 默认情况下，所有请求均由[RDSServer DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象[MSDFMAP 处理。处理程序](../../../ado/guide/remote-data-service/datafactory-customization.md)组件和[MSDFMAP。](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)指定服务器上的 INI 文件。 请记住，在将服务器更改为协调新旧的 MSDFMAP 中的设置时 **。INI**文件。 不兼容性可能会导致一台服务器上的成功请求在另一台服务器上失败。 如果服务器属性设置为空字符串 ""，则将在本地计算机上使用这些对象。  
  
## <a name="applies-to"></a>应用于  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [服务器属性示例（VBScript）](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [Connect 属性（RDS）](../../../ado/reference/rds-api/connect-property-rds.md)   
 [SQL 属性](../../../ado/reference/rds-api/sql-property.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


