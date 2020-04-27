---
title: IBCPSession (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- IBCPSession interface
ms.assetid: 00d0311f-8b71-4ad6-824d-0e89119347a3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 142f6ac339e437877c485588333fabb04e0bd66b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63241351"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
  IBCPSession 接口公开了对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基于文件的大容量复制操作的支持****。 **IBCPSession**接口在与会话相同的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]级别下，在 Native Client OLE DB 提供程序中公开。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序中，数据源对象是会话对象的工厂，而大容量复制操作是在连接属性 SSPROP_ENABLEBULKCOPY 中指定的。 此外，SSPROP_ENABLEFASTLOAD 属性应当设置为 True。  
  
 调用 IDBCreateSession::CreateSession 方法随后将创建 BulkCopySession 对象********。 然后，可针对此 IBCPSession 对象的 IBCPSession 接口，采用极为相似的签名来调用通过 IBCPSession 对象公开的所有基于文件的大容量复制方法************。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序通过[IRowsetFastLoad](irowsetfastload-ole-db.md)接口支持基于内存的大容量复制操作。  
  
 有关使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序进行大容量复制操作的详细信息，请参阅[执行大容量复制操作](../native-client/features/performing-bulk-copy-operations.md)。  
  
 有关演示如何使用 IBCPSession**** 接口的示例，请参阅 [IBCPSession::BCPDone (OLE DB)](ibcpsession-bcpdone-ole-db.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|方法|说明|  
|------------|-----------------|  
|[IBCPSession::BCPColFmt &#40;OLE DB&#41;](ibcpsession-bcpcolfmt-ole-db.md)|在程序变量与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列之间创建绑定。|  
|[IBCPSession::BCPColumns &#40;OLE DB&#41;](ibcpsession-bcpcolumns-ole-db.md)|设置绑定到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中列的字段数。|  
|[IBCPSession::BCPControl &#40;OLE DB&#41;](ibcpsession-bcpcontrol-ole-db.md)|设置大容量复制操作的选项。|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md)|提交要发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的剩余行。|  
|[IBCPSession::BCPExec &#40;OLE DB&#41;](ibcpsession-bcpexec-ole-db.md)|执行大容量复制操作。|  
|[IBCPSession::BCPInit &#40;OLE DB&#41;](ibcpsession-bcpinit-ole-db.md)|初始化大容量复制结构，执行某些错误检查，验证数据和格式化文件名是否正确，然后打开文件。|  
|[IBCPSession::BCPReadFmt &#40;OLE DB&#41;](ibcpsession-bcpreadfmt-ole-db.md)|从格式化文件中读取每一列的格式信息。|  
|[IBCPSession::BCPWriteFmt &#40;OLE DB&#41;](ibcpsession-bcpwritefmt-ole-db.md)|将每一列的格式信息写入格式化文件。|  
  
## <a name="see-also"></a>另请参阅  
 [接口 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
