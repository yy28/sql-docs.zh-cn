---
title: ObjectProxy (ADO-WFC 语法) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 485d011fa6762acd04cad54ff7fffc8d8136e063
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917948"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy（ADO - WFC 语法）
**ObjectProxy**对象表示的服务器，并返回由**createObject**方法[DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)对象。 ObjectProxy 类具有一种方法**调用**，这可以在服务器上调用方法并返回该调用中生成的对象。  
  
 **包 com.ms.wfc.data**  
  
## <a name="methods"></a>方法  
  
### <a name="call-method-adowfc-syntax"></a>调用方法 （ADO/WFC 语法）  
 调用由 ObjectProxy 所表示的服务器上的方法。 （可选） 可能会作为对象的数组传递方法自变量。  
  
#### <a name="syntax"></a>语法  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>返回  
 Object  
 调用该方法生成的对象。  
  
#### <a name="parameters"></a>Parameters  
 *ObjectProxy*  
 **ObjectProxy**表示服务器的对象。  
  
 *方法*  
 一个字符串，包含要在服务器上调用的方法的名称。  
  
 *参数*  
 可选。 是在服务器上的方法的参数的对象的数组。 Java 数据类型自动转换为适用于在服务器上使用的数据类型中。
