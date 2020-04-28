---
title: Prompt 属性-动态（ADO） |Microsoft Docs
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
ms.openlocfilehash: cde7a5ad0324bc7d5cde5e1a794eeb9e2cb3381a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931578"
---
# <a name="prompt-property-dynamic-ado"></a>Prompt 属性 - 动态 (ADO)
指定 OLE DB 提供程序是否应提示用户提供初始化信息。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置并返回一个[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)值。  
  
## <a name="remarks"></a>备注  
 **Prompt**是动态属性，OLE DB 提供程序可以将其附加到[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合。 为了提示输入初始化信息，OLE DB 提供程序通常会向用户显示一个对话框。  
  
 **连接关闭**时，[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的动态属性将丢失。 必须先重置**Prompt**属性，然后再重新打开**连接**，才能使用默认值以外的值。  
  
> [!NOTE]
>  不要指定提供程序在用户将无法响应对话框的情况下是否应提示用户。 例如，如果应用程序正在服务器系统而不是用户的客户端上运行，或者如果应用程序在没有用户登录的系统上运行，则用户将无法响应。 在这些情况下，应用程序会无限期等待响应，并似乎锁定。  
  
## <a name="usage"></a>使用情况  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>应用于  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
