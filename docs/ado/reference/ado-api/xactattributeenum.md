---
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
ms.openlocfilehash: d645c648b6e1410f96beb567d7fb496e5fdae2d2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764418"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
指定[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的事务特性。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|通过调用[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)以自动启动新事务来执行保留中止。 并非所有提供程序都支持此行为。|  
|**adXactCommitRetaining**|131072|通过调用[CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)以自动启动新事务来执行保留提交。 并非所有提供程序都支持此行为。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>应用于  
 [Attributes 属性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
