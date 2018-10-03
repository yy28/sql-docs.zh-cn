---
title: LocalDBFormatMessage 函数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- LocalDBFormatMessage
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e711b82bea95490fcf0188d5ed94c398f31c6335
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070977"
---
# <a name="localdbformatmessage-function"></a>LocalDBFormatMessage 函数
  返回指定的 SQL Server Express LocalDB 错误的本地化文本说明。  
  
 **标头文件：** sqlncli.h  
  
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
  
## <a name="parameters"></a>Parameters  
 *hrLocalDB*  
 [输入] LocalDB 错误代码。  
  
 *dwFlags*  
 [输入] 用于指定此函数的行为的标志。  
  
 可用标志：  
  
 LOCALDB_TRUNCATE_ERR_MESSAGE  
 如果输入缓冲区太小，则将截断错误消息以适合缓冲区。  
  
 *dwLanguageId*  
 [输入] 所需的语言 (LANGID) 或 0，在这种情况下，将使用 Win32 FormatMessage 语言顺序。  
  
 *wszMessage*  
 [输出] 要存储 LocalDB 错误消息的缓冲区。  
  
 *lpcchMessage*  
 [输入/输出]在输入中包含的大小*wszMessage*以字符为单位的缓冲区。 输出时，如果给定的缓冲区太小，则包含所需的缓冲区大小（以字符数表示，包括任何尾随空格）。 如果函数成功，则包含消息中的字符数（任何尾随空格除外）。  
  
## <a name="returns"></a>返回  
 S_OK  
 函数成功。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 计算机上没有安装 SQL Server Express LocalDB。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 一个或多个指定的输入参数无效。  
  
 [LOCALDB_ERROR_UNKNOWN_ERROR_CODE](../express-localdb-error-messages/localdb-error-unknown-error-code.md)  
 请求的消息不存在。  
  
 [LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID](../express-localdb-error-messages/localdb-error-unknown-language-id.md)  
 该消息在请求的语言中不可用。  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 输入的缓冲区*wszMessage*太短，并且未请求截断。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 发生了意外错误。 有关详细信息，请参阅事件日志。  
  
## <a name="remarks"></a>备注  
 有关使用 LocalDB API 的代码示例，请参阅[SQL Server Express LocalDB 参考](../sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Express LocalDB 标头信息和版本信息](sql-server-express-localdb-header-and-version-information.md)  
  
  
