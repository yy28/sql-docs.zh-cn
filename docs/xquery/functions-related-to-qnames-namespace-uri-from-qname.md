---
title: 命名空间 uri-从-QName （XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 96edefd5409520109e2b2155507dd8879ed4b0d3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67946637"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>与 QName 相关的函数 - namespace-uri-from-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回表示 *$arg*指定的 QName 的命名空间 uri 的字符串。 如果 *$arg*是空序列，则结果为空序列。  
  
## <a name="syntax"></a>语法  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 是返回其命名空间 URI 的 QName。  
  
## <a name="examples"></a>示例  
 本主题提供了对存储在 AdventureWorks 数据库的各种**xml**类型列中的 xml 实例的 XQuery 示例。  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. 检索 QName 的命名空间 URI  
 有关工作示例，请参阅[本地名称 from-QName &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md)。  
  
### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **命名空间 uri-QName （）** 函数返回 xs： string 的实例，而不是 Xs： anyURI。  
  
## <a name="see-also"></a>另请参阅  
 [与 QNames &#40;XQuery 相关的函数&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
