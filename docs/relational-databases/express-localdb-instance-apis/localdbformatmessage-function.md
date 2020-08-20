---
description: LocalDBFormatMessage 函数
title: LocalDBFormatMessage 函数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBFormatMessage
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5d3083d789124023985577d1a04a811ff2273915
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475834"
---
# <a name="localdbformatmessage-function"></a>LocalDBFormatMessage 函数
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  返回指定的 SQL Server Express LocalDB 错误的本地化文本说明。  
  
 **头文件：** sqlncli.msi  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT LocalDBFormatMessage(  
           HRESULT hrLocalDB,  
           DWORD dwFlags,   
           DWORD dwLanguageId,   
           LPWSTR wszMessage,   
           LPDWORD lpcchMessage   
);  
```  
  
## <a name="parameters"></a>参数  
 *hrLocalDB*  
 [输入] LocalDB 错误代码。  
  
 dwFlags   
 [输入] 用于指定此函数的行为的标志。  
  
 可用标志：  
  
 LOCALDB_TRUNCATE_ERR_MESSAGE  
 如果输入缓冲区太小，则将截断错误消息以适合缓冲区。  
  
 *dwLanguageId*  
 [输入] 所需的语言 (LANGID) 或 0，在这种情况下，将使用 Win32 FormatMessage 语言顺序。  
  
 *wszMessage*  
 [输出] 要存储 LocalDB 错误消息的缓冲区。  
  
 *lpcchMessage*  
 [输入/输出]输入时包含 *wszMessage* 缓冲区的大小（以字符为限）。 输出时，如果给定的缓冲区太小，则包含所需的缓冲区大小（以字符数表示，包括任何尾随空格）。 如果函数成功，则包含消息中的字符数（任何尾随空格除外）。  
  
## <a name="returns"></a>返回  
 S_OK  
 函数成功。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 计算机上没有安装 SQL Server Express LocalDB。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 一个或多个指定的输入参数无效。  
  
 [LOCALDB_ERROR_UNKNOWN_ERROR_CODE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-error-code.md)  
 请求的消息不存在。  
  
 [LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-language-id.md)  
 该消息在请求的语言中不可用。  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../../relational-databases/express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 输入缓冲区 *wszMessage* 太短，不请求截断。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 发生了意外错误。 有关详细信息，请参阅事件日志。  
  
## <a name="remarks"></a>备注  
 有关使用 LocalDB API 的代码示例，请参阅 [SQL Server Express LocalDB 引用](../../relational-databases/sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Express LocalDB 标头信息和版本信息](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
