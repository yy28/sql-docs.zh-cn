---
title: InvokeService (RDS) |Microsoft 文档
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
- InvokeService [RDS]
ms.assetid: ad45c676-ec7e-4a3a-9a6b-a54f75eb3012
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 92927a240c0501196c1b9bf0c1643f6cb0f708d4
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35288286"
---
# <a name="invokeservice-rds"></a>InvokeService (RDS)
返回一个指向所请求的接口的对象的功能更强大版本上。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>Parameters  
 *riid*  
  
 [in]所请求的接口的标识符。  
  
 *punkNotSoFunctionalInterface*  
  
 [in]功能较少的源对象。  
  
 *ppunkMoreFunctionalInterface*  
  
 [out]接收请求中的接口指针的指针变量的地址*riid*。 在成功返回时， *ppunkMoreFunctionalInterface*参数包含对象的请求的接口指针。 如果对象不支持在指定的接口*riid*， *ppunkMoreFunctionalInterface*设置为 NULL。  
  
## <a name="return-value"></a>返回值  
 HRESULT 值，该值指示如果对的调用**InvokeService**方法成功。  
  
## <a name="remarks"></a>Remarks  
 RDS 光标引擎实现**InvokeService**采用输入行集 （或多个结果对象）、 填充游标引擎从输入行集，然后返回一个指向自身。  
  
## <a name="applies-to"></a>适用范围  
 [IRDSService 接口 (RDS)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [RDS 方法](../../../ado/reference/rds-api/rds-methods.md)


