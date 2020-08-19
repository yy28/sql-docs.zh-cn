---
description: RDS 方法
title: RDS 方法 |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- RDS methods [ADO]
- methods [ADO], RDS
ms.assetid: c2c6af1a-3c44-4c9d-ad33-b381552c71af
author: rothja
ms.author: jroth
ms.openlocfilehash: 7f8685ead3b7f62861d6e27792a850af3140ebe3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438789"
---
# <a name="rds-methods"></a>RDS 方法
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件 (参阅 Windows 8 和 [Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416) ，以了解更多详细信息) 。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到 [WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
|方法|描述|  
|-|-|  
|[取消 (RDS) ](../../../ado/reference/rds-api/cancel-method-rds.md)|取消执行挂起的异步方法调用。|  
|[CancelUpdate (RDS) ](../../../ado/reference/rds-api/cancelupdate-method-rds.md)|取消对 **记录集** 对象的当前行或新行所做的任何更改。|  
|[ConvertToString (RDS) ](../../../ado/reference/rds-api/converttostring-method-rds.md)|将 **记录集** 转换为表示记录集数据的 MIME 字符串。|  
|[CreateObject (RDS) ](../../../ado/reference/rds-api/createobject-method-rds.md)|为目标业务对象创建代理并返回指向它的指针。|  
|[CreateRecordset (RDS) ](../../../ado/reference/rds-api/createrecordset-method-rds.md)|创建一个空的、断开连接的 **记录集**。|  
|[Execute 方法 (RDS)](../../../ado/reference/rds-api/execute-method-rds.md)|执行请求并创建高级数据行集 (以便与 ADO 2.5 和更高版本一起使用) 。|  
|[Execute21 方法 (RDS)](../../../ado/reference/rds-api/execute21-method-rds.md)|执行请求并创建高级数据行集 (以便与 ADO 2.1) 一起使用。|  
|[InvokeService (RDS)](../../../ado/reference/rds-api/invokeservice-rds.md)|返回一个指针，该指针指向对象的更好的版本上所请求的接口。|  
|[MoveFirst、MoveLast、MoveNext、MovePrevious (RDS) ](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)|移动到指定 **记录集** 对象中的第一条、最后一条、下一条记录或上一条记录。|  
|[查询 (RDS) ](../../../ado/reference/rds-api/query-method-rds.md)|使用有效的 SQL 查询字符串返回 **记录集**。|  
|[刷新 (RDS) ](../../../ado/reference/rds-api/refresh-method-rds.md)|重新查询 **连接** 属性中指定的数据源，并更新查询结果。|  
|[重置 (RDS) ](../../../ado/reference/rds-api/reset-method-rds.md)|基于指定的排序和筛选器属性，对客户端 **记录集**执行排序或筛选。|  
|[SubmitChanges (RDS) ](../../../ado/reference/rds-api/submitchanges-method-rds.md)|将本地缓存的可更新 **记录集** 的挂起的更改提交到 **连接** 属性中指定的数据源。|  
|[Synchronize 方法 (RDS)](../../../ado/reference/rds-api/synchronize-method-rds.md)|使用连接字符串指定的数据库同步给定的记录集， (用于 ADO 2.5 和更高版本的) 。|  
|[Synchronize21 方法 (RDS)](../../../ado/reference/rds-api/synchronize21-method-rds.md)|使用连接字符串指定的数据库同步给定的记录集， (用于 ADO 2.1) 。|


