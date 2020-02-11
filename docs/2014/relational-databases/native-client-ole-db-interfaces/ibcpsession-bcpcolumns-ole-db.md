---
title: IBCPSession：： BCPColumns （OLE DB） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPColumns (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPColumns method
ms.assetid: c338abe8-9e30-4853-a7c6-b1a6c00095e1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7108760ebdb5e7e3e6367b801b07d4f8140a62d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63238737"
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns (OLE DB)
  设置绑定到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中列的字段数。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPColumns(   
DBCOUNTITEMnColumns);  
```  
  
## <a name="remarks"></a>备注  
 在内部，它调用 [IBCPSession::BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md) 以便为字段数据设置默认值。 这些默认值从当通过 [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md) 指定表名称时提供程序内部检索的 SQL Server 列信息中获取。  
  
> [!NOTE]  
>  只有在已用某一有效的文件名调用 BCPInit 后，才能调用此方法****。  
  
 只有在您要使用不同于默认设置的用户文件格式时，才应调用此方法。 有关默认用户文件格式的说明的详细信息，请参阅 BCPInit 方法****。  
  
 在调用 BCPColumns 方法后，必须为用户文件中的每一列都调用 BCPColFmt 方法，以便完全定义某一自定义文件格式********。  
  
## <a name="arguments"></a>参数  
 *nColumns*[in]  
 用户文件中字段的总数。 即使准备将数据从用户文件大容量复制到某一 SQL Server 表，并且不想复制用户文件中的所有字段，仍必须将 nColumns 参数设置为用户字段的总数**。 然后，可通过 BCPColFmt 指定跳过的字段****。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 出现访问接口特定的错误；若要获取详细信息，请使用 [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) 接口。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如，在调用该方法之前，未调用 BCPInit 方法****。 在为某一大容量复制操作多次调用此方法时，也会发生这一意外调用。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
## <a name="see-also"></a>另请参阅  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [执行大容量复制操作](../native-client/features/performing-bulk-copy-operations.md)  
  
  
