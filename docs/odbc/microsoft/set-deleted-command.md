---
title: SET DELETED 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5efbd7e98b430128e52634f5c7d71597afc89ace
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806065"
---
# <a name="set-deleted-command"></a>SET DELETED 命令
指定是否已处理标记为删除的记录，并指明它们是否可在其他命令中使用。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 （默认为驱动程序，Visual FoxPro 的默认值为 OFF。）指定的命令 （包括相关表中的记录） 的记录操作的使用范围忽略记录标记为待删除。  
  
 OFF  
 指定记录标记为要删除可访问的记录 （包括相关表中的记录） 运行的命令使用作用域。  
  
## <a name="remarks"></a>备注  
 查询可以使用 Visual FoxPro 雕像技术，如果表索引上已删除 （） 优化使用已删除 （） 以测试记录的状态。  
  
> [!IMPORTANT]  
>  如果该命令的默认作用域为当前记录或包含单个记录的范围，将忽略设置已删除。 索引始终忽略设置删除和索引表中的所有记录。  
  
## <a name="see-also"></a>请参阅  
 [DELETE - SQL 命令](../../odbc/microsoft/delete-sql-command.md)
