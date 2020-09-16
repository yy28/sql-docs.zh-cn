---
description: getTrustStore 方法 (SQLServerDataSource)
title: getTrustStore 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustStore Method (SQLServerDataSource)
apilocation:
- getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7afcb2b9d8402bf1fd8d2f4637488ba8c091f4c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433989"
---
# <a name="gettruststore-method-sqlserverdatasource"></a>getTrustStore 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回指向证书 trustStore 文件的路径（包括文件名）。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>返回值  
 包含指向证书 trustStore 文件路径（包括文件名）的字符串****；如果未设置值，则为 Null。  
  
## <a name="remarks"></a>注解  
 如果未设置 trustStore 属性，[getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md) 方法将返回 Null。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
