---
title: ICommand (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ICommand [SQL Server Native Client]
ms.assetid: 5e24b3a0-0658-44fc-b653-f4c52f9eb328
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4e583b08cf0ba55268c4acb9e19722d3a693d50
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62987322"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
  本主题讨论特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的 OLE DB 行为。  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 如果插入的数据大于列的大小，通常会导致错误。 但是，可能会出现将返回 S_OK、但 dwStatus 将设置为 DBSTATUS_S_TRUNCATED 的情况**。 当用参数插入数据时，通常会发生这种情况，列的大小不足以容纳数据， `ICommandWithParameters::SetParameterInfo`并且尚未调用。  
  
## <a name="see-also"></a>另请参阅  
 [接口 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
