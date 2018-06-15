---
title: 提示属性的动态 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Prompt property [ADO]
ms.assetid: c4f001b5-8d16-4d39-a42e-c0e2faaaceaf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7b5c0637f7befb1419f5cb96bbcd421d59cc7b8
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280626"
---
# <a name="prompt-property-dynamic-ado"></a>提示属性的动态 (ADO)
指定的 OLE DB 访问接口是否应提示用户输入的初始化信息。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置并返回[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)值。  
  
## <a name="remarks"></a>Remarks  
 **提示**是动态的属性，这可能会追加到[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)OLE DB 访问接口的集合。 若要初始化的信息提示，OLE DB 提供程序通常将向用户显示一个对话框。  
  
 动态属性[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象将会丢失时**连接**已关闭。 **提示**属性必须在重新打开之前重置**连接**若要使用默认值以外的值。  
  
> [!NOTE]
>  未指定提供程序应提示中的用户将无法使其响应对话框中的方案中的用户。 例如，用户将无法响应的应用程序运行而不是用户的客户端上的服务器系统上是否与在没有用户登录中的系统上运行该应用程序。 在这些情况下，应用程序将无限期地等待响应，看起来死锁。  
  
## <a name="usage"></a>用法  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
