---
description: XactAttributeEnum
title: XactAttributeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
author: rothja
ms.author: jroth
ms.openlocfilehash: 2528c9b7a8cf9eb2918983d90e57ac39e6ee989e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441449"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
指定 [连接](../../../ado/reference/ado-api/connection-object-ado.md) 对象的事务特性。  
  
|返回的常量|值|描述|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|通过调用 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 以自动启动新事务来执行保留中止。 并非所有提供程序都支持此行为。|  
|**adXactCommitRetaining**|131072|通过调用 [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 以自动启动新事务来执行保留提交。 并非所有提供程序都支持此行为。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>适用于  
 [Attributes 属性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
