---
title: 基本 RDS 编程模型 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4b8f08cda158c21d556b251d3e141b333418ca38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704358"
---
# <a name="basic-rds-programming-model"></a>基本的 RDS 编程模型
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 解决以下环境中存在的应用程序：客户端应用程序指定将在一台服务器并返回所需的信息所必需的参数执行的程序。 调用上对指定的数据源的服务器提升访问权限的程序中检索信息、 根据需要处理数据，然后返回到客户端应用程序可以轻松地使用窗体中生成的信息。 RDS 提供了可以执行以下操作序列的方式：  
  
-   指定的服务器上，要调用的程序并获取一种方法来从客户端引用它。 (有时称为此引用*代理*。 它表示远程服务器程序。 客户端应用程序将"调用"代理像它是本地的程序，但它实际上调用远程服务器程序。）  
  
-   调用服务器程序。 将参数传递给服务器程序的标识数据源以及要发出的命令。 （服务器程序实际上使用 ADO 来获得对数据源的访问。 ADO 与给定的参数之一建立连接，然后发出另一个参数中指定的命令。）  
  
-   服务器程序获得[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)数据源中的对象。 （可选）**记录集**在服务器上处理对象。  
  
-   服务器程序将返回最后一个**记录集**到客户端应用程序对象。  
  
-   在客户端**记录集**对象放到可以轻松地使用由 visual 控件的窗体。  
  
-   对进行任何修改**记录集**对象发送回服务器程序，使用它们来更新数据源。  
  
 此编程模型中包含某些便利功能。 如果不需要复杂的服务器程序访问数据源，并且如果你提供所需的连接和命令参数，RDS 将自动检索指定的数据的简单的默认服务器程序。  
  
 如果需要更复杂的处理，则可以指定自己的自定义服务器程序。 例如，自定义服务器程序有其可供使用 ADO 的完整功能，因为它无法连接到多个不同的数据源、 某种复杂方式合并其数据，然后返回到客户端应用程序的简单、 已处理的结果。  
  
 最后，如果你的需求之间在某处，ADO 现在支持自定义默认服务器程序的行为。  
  
## <a name="see-also"></a>请参阅  
 [RDS 编程模型的详细信息](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [RDS 方案](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 使用情况和安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


