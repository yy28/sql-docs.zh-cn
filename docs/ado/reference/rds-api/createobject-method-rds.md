---
title: CreateObject 方法 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 918836e949593672417240c1b91026e1e02c4788
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712321"
---
# <a name="createobject-method-rds"></a>CreateObject 方法 (RDS)
创建目标业务对象的代理，并返回的指针。 用来与业务对象的通信通过 Internet 发送的请求和数据服务器端存根 （stub） 代理包和封送数据。 对于进程内组件对象，不使用代理，提供只需指向对象的指针。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
 远程数据服务支持以下协议：HTTP、 HTTPS (安全套接字层的 HTTP)、 DCOM 和进程内。  
  
|Protocol|语法|  
|--------------|------------|  
|HTTP|Set object = DataSpace.CreateObject("ProgId", "https\://awebsrvr")|  
|HTTPS|Set object = DataSpace.CreateObject("ProgId", "https\://awebsrvr")|  
|DCOM|Set object = DataSpace.CreateObject("ProgId", "computername")|  
|进程内|Set object = DataSpace.CreateObject("ProgId", "")|  
  
## <a name="parameters"></a>Parameters  
 *Object*  
 计算结果为一个对象，它在指定的类型的对象变量*ProgID*。  
  
 *DataSpace*  
 表示的对象变量[rds。数据空间](../../../ado/reference/rds-api/dataspace-object-rds.md)对象，用于创建新对象的实例。  
  
 *ProgID*  
 一个**字符串**值，该值包含指定用于实现应用程序的业务规则的服务器端业务对象的编程标识符。  
  
 *awebsrvr*或*computername*  
 一个**字符串**值，该值表示用于标识在其中创建服务器业务对象的实例的 Internet 信息服务 (IIS) Web 服务器的 URL。  
  
## <a name="remarks"></a>备注  
 *HTTP 协议*是标准的 Web 协议;*HTTPS*是不安全的 Web 协议。 使用*DCOM 协议*局域网不使用 HTTP 运行时。 *进程内*协议是本地的动态链接库 (DLL); 它不使用网络。  
  
## <a name="applies-to"></a>适用范围  
 [DataSpace 对象 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [DataFactory 对象、 查询方法和 CreateObject 方法示例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [DataSpace 对象和 CreateObject 方法示例 (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [CreateRecordset 方法 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


