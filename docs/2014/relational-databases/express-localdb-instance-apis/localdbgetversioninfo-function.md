---
title: LocalDBGetVersionInfo 函数 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBGetVersionInfo
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: d4aaea30-1d0d-4436-bcdc-5c101d27b1c1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cce316685bccb2724eb89965e4e466fe58fb807e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85027730"
---
# <a name="localdbgetversioninfo-function"></a>LocalDBGetVersionInfo 函数
  返回有关指定的 SQL Server Express LocalDB 版本的信息，如该版本是否存在以及完整的 LocalDB 版本号（包括内部版本号和发行版本号）。  
  
 此信息以名为 LocalDBVersionInfo 的形式返回 `struct` ， **LocalDBVersionInfo**该格式具有以下定义。  
  
```  
typedef struct _LocalDBVersionInfo  
{  
      // Contains the size of the LocalDBVersionInfo struct  
      DWORD  cbLocalDBVersionInfoSize;  
  
      // Holds the version name  
      TLocalDBVersionwszVersion;  
  
      // TRUE if the instance files exist on disk, FALSE otherwise  
      BOOL   bExists;  
  
      // Holds the LocalDB version for the instance in the format: major.minor.build.revision  
      DWORD  dwMajor;  
      DWORD  dwMinor;  
      DWORD  dwBuild;  
      DWORD  dwRevision;  
} LocalDBVersionInfo;  
  
```  
  
 **头文件：** sqlncli.msi  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT LocalDBGetVersionInfo(  
           PCWSTR wszVersionName,           PLocalDBVersionInfo pVersionInfo,           DWORD dwVersionInfoSize);  
```  
  
## <a name="parameters"></a>参数  
 *wszVersionName*  
 [输入] LocalDB 版本名称。  
  
 *pVersionInfo*  
 [输出] 要存储有关 LocalDB 版本信息的缓冲区。  
  
 *dwVersionInfoSize*  
 送保存*VersionInfo*缓冲区的大小。  
  
## <a name="returns"></a>返回  
 S_OK  
 函数成功。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 计算机上没有安装 SQL Server Express LocalDB。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 一个或多个指定的输入参数无效。  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../express-localdb-error-messages/localdb-error-unknown-version.md)  
 指定的 LocalDB 版本不存在。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 发生了意外错误。 有关详细信息，请参阅事件日志。  
  
## <a name="details"></a>详细信息  
 引入 `struct` 大小参数（*lpVersionInfoSize*）背后的基本原理是使 API 能够返回不同版本的**LocalDBVersionInfostruct**，从而有效地实现向前和向后兼容性。  
  
 如果 `struct` 大小参数（*lpVersionInfoSize*）与已知版本的**LocalDBVersionInfostruct**的大小匹配，则返回该版本的 `struct` 。 否则，返回 LOCALDB_ERROR_INVALID_PARAMETER。  
  
 **LocalDBGetVersionInfo** API 用法的典型示例如下所示：  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L"11.0", &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>备注  
 有关使用 LocalDB API 的代码示例，请参阅[SQL Server Express LocalDB 引用](../sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Express LocalDB 标头信息和版本信息](sql-server-express-localdb-header-and-version-information.md)  
  
  
