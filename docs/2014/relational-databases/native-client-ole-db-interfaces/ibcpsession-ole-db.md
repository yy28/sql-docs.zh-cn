---
title: IBCPSession (OLE DB) |Microsoft Docs
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
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48212317"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
  IBCPSession 接口公开了对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基于文件的大容量复制操作的支持。 **IBCPSession**接口中公开[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与会话位于同一级别 Native Client OLE DB 提供程序。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序数据源对象是会话对象的工厂和连接属性 SSPROP_ENABLEBULKCOPY 中指定大容量复制操作。 此外，SSPROP_ENABLEFASTLOAD 属性应当设置为 True。  
  
 调用 IDBCreateSession::CreateSession 方法随后将创建 BulkCopySession 对象。 然后，可针对此 IBCPSession 对象的 IBCPSession 接口，采用极为相似的签名来调用通过 IBCPSession 对象公开的所有基于文件的大容量复制方法。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持通过基于内存的大容量复制操作[IRowsetFastLoad](irowsetfastload-ole-db.md)接口。  
  
 有关使用详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口大容量复制操作，请参阅[执行大容量复制操作](../native-client/features/performing-bulk-copy-operations.md)。  
  
 有关演示如何使用的示例**IBCPSession**接口，请参阅[IBCPSession::BCPDone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|方法|Description|  
|------------|-----------------|  
|[Ibcpsession:: Bcpcolfmt &#40;OLE DB&#41;](ibcpsession-bcpcolfmt-ole-db.md)|在程序变量与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列之间创建绑定。|  
|[Ibcpsession:: Bcpcolumns &#40;OLE DB&#41;](ibcpsession-bcpcolumns-ole-db.md)|设置绑定到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中列的字段数。|  
|[Ibcpsession:: Bcpcontrol &#40;OLE DB&#41;](ibcpsession-bcpcontrol-ole-db.md)|设置大容量复制操作的选项。|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md)|提交要发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的剩余行。|  
|[Ibcpsession:: Bcpexec &#40;OLE DB&#41;](ibcpsession-bcpexec-ole-db.md)|执行大容量复制操作。|  
|[Ibcpsession:: Bcpinit &#40;OLE DB&#41;](ibcpsession-bcpinit-ole-db.md)|初始化大容量复制结构，执行某些错误检查，验证数据和格式化文件名是否正确，然后打开文件。|  
|[Ibcpsession:: Bcpreadfmt &#40;OLE DB&#41;](ibcpsession-bcpreadfmt-ole-db.md)|从格式化文件中读取每一列的格式信息。|  
|[Ibcpsession:: Bcpwritefmt &#40;OLE DB&#41;](ibcpsession-bcpwritefmt-ole-db.md)|将每一列的格式信息写入格式化文件。|  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
