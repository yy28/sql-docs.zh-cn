---
title: setApplicationName 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 24d6e48d-53c4-4da2-a6de-1cdff463c9cd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f0f91762dd168f4136a4a476b47dfe36b749e16
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67975562"
---
# <a name="setapplicationname-method-sqlserverdatasource"></a>setApplicationName 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置应用程序名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setApplicationName(java.lang.String applicationName)  
```  
  
#### <a name="parameters"></a>parameters  
 *applicationName*  
  
 包含应用程序名称的一个字符串  。  
  
## <a name="remarks"></a>备注  
 此应用程序名称用于在各种 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分析和日志记录工具中标识特定的应用程序。 如果未设置应用程序名称，getApplicationName 方法则将返回未本地化的字符串“[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]”。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
