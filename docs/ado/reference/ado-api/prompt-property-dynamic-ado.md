---
title: Prompt 属性-动态 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Prompt property [ADO]
ms.assetid: c4f001b5-8d16-4d39-a42e-c0e2faaaceaf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4f2c778a6e922477cd8b21251a638d430ce15480
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66703154"
---
# <a name="prompt-property-dynamic-ado"></a>Prompt 属性 - 动态 (ADO)
指定的 OLE DB 访问接口是否应提示用户输入的初始化信息。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置并返回[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)值。  
  
## <a name="remarks"></a>备注  
 **Prompt**是动态的属性，这可能会追加到[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)OLE DB 访问接口的集合。 若要初始化的信息提示，OLE DB 访问接口通常将向用户显示一个对话框。  
  
 动态属性[连接](../../../ado/reference/ado-api/connection-object-ado.md)后，会丢失对象**连接**已关闭。 **Prompt**属性必须在重新打开之前重置**连接**若要使用非默认值。  
  
> [!NOTE]
>  不要指定提供程序应提示用户在其中将无法再以响应对话框的用户的方案中。 例如，用户将无法再响应如果而不是用户的客户端上的服务器系统上运行应用程序或应用程序在系统上运行与在没有用户登录。 在这些情况下，应用程序将无限期地等待响应并似乎锁定。  
  
## <a name="usage"></a>用法  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
