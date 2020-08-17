---
description: Unicode 数据和服务器代码页
title: Unicode 数据和服务器代码页 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- metadata [SQL Server], stored procedures
- Unicode [SQL Server], extended stored procedures
- extended stored procedures [SQL Server], metadata
ms.assetid: 52310260-a892-4b27-ad2e-bf164b98ee80
author: rothja
ms.author: jroth
ms.openlocfilehash: 2fd22a9fa5410a5e9489d3e0cb72949b24ba298d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88328863"
---
# <a name="unicode-data-and-server-code-pages"></a>Unicode 数据和服务器代码页
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 扩展存储过程 API 将对 Unicode 数据启用；但是，它不对 Unicode 元数据启用。 #define Unicode 指令不影响扩展存储过程 API。  
  
 由扩展存储过程 API 返回的或由您的扩展存储过程应用程序提供给它的所有元数据都假定位于服务器的多字节代码页中。 扩展存储过程 API 服务器应用程序的默认代码页是运行应用程序的计算机的 ANSI 代码页，可以通过调用 **srv_pfield** ，并将字段参数设置为 SRV_SPROC_CODEPAGE 来获取此页。  
  
 如果您的扩展存储过程 API 应用程序启用了 Unicode，则必须将您的 Unicode 元数据列名称、错误消息等转换为多字节数据，然后才能将该数据传递给扩展存储过程 API。  
  
## <a name="example"></a>示例  
 以下扩展存储过程提供了上述 Unicode 转换的示例。 请注意：  
  
-   列数据将作为 Unicode 数据传递到 **srv_describe** ，因为该列被描述为 SRVNVARCHAR。  
  
-   列名元数据将作为多字节数据传递到 **srv_describe** 。  
  
     扩展存储过程调用 **srv_pfield** ，并将字段参数设置为 SRV_SPROC_CODEPAGE 以获取的多字节代码页 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   错误消息将作为多字节数据传递到 **srv_sendmsg** 。  
  
    ```  
    __declspec(dllexport) RETCODE proc1 (SRV_PROC *srvproc)  
    {  
        #define MAX_COL_NAME_LEN 25  
        #define MAX_COL_DATA_LEN 50  
        #define MAX_ERR_MSG_LEN 250  
        #define MAX_SERVER_ERROR 20000  
        #define XP_ERROR_NUMBER MAX_SERVER_ERROR+1  
  
        int retval;  
        UINT serverCodePage;  
        CHAR *szServerCodePage;  
  
        WCHAR unicodeColumnName[MAX_COL_NAME_LEN];  
        CHAR multibyteColumnName[MAX_COL_NAME_LEN];  
  
        WCHAR unicodeColumnData[MAX_COL_DATA_LEN];  
  
        WCHAR unicodeErrorMessage[MAX_ERR_MSG_LEN];  
        CHAR  multibyteErrorMessage[MAX_ERR_MSG_LEN];  
  
        lstrcpyW (unicodeColumnName, L"column1");  
        lstrcpyW (unicodeColumnData, L"column1 data");  
        lstrcpyW (unicodeErrorMessage, L"No Error!");  
  
        // Obtain server code page.  
        //  
        szServerCodePage = srv_pfield (srvproc, SRV_SPROC_CODEPAGE, NULL);      
        if (NULL != szServerCodePage)  
            serverCodePage = atol(szServerCodePage);  
        else   
        {   // Problem situation exists.  
            srv_senddone(srvproc, (SRV_DONE_ERROR | SRV_DONE_MORE), 0, 0);  
            return 1;  
        }  
  
        // Convert column name for Unicode to multibyte using the   
        // server code page.  
        //  
        retval = WideCharToMultiByte(    
            serverCodePage,                 // code page  
            0,                              // default  
            unicodeColumnName,              // wide-character string  
            -1,                             // string is null terminated  
            multibyteColumnName,            // address of buffer for new  
                                            //   string  
            sizeof (multibyteColumnName),   // size of buffer  
            NULL, NULL);  
  
        if (0 == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"Conversion to multibyte  
            failed.");  
            goto Error;  
        }  
  
        retval = srv_describe (srvproc, 1, multibyteColumnName,  
        SRV_NULLTERM,   
          SRVNVARCHAR, MAX_COL_DATA_LEN*sizeof(WCHAR), // destination  
            SRVNVARCHAR, lstrlenW(unicodeColumnData)*sizeof(WCHAR),  
            unicodeColumnData); //source  
        if (FAIL == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"srv_describe failed.");  
            goto Error;  
        }  
  
       retval = srv_sendrow(srvproc);  
        if (FAIL == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"srv_sendrow failed.");  
            goto Error;  
        }  
  
        retval = srv_senddone (srvproc, SRV_DONE_MORE|SRV_DONE_COUNT, 0, 1);  
        if (FAIL == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"srv_senddone failed.");  
            goto Error;  
        }  
  
        return 0;  
    Error:  
        // convert error message from Unicode to multibyte.  
        retval = WideCharToMultiByte(    
            serverCodePage,                 // code page  
            0,                              // default  
            unicodeErrorMessage,            // wide-character string  
            -1,                             // string is null terminated  
            multibyteErrorMessage,          // address of buffer for new  
                                            //   string  
            sizeof (multibyteErrorMessage), // size of buffer  
            NULL, NULL);  
  
    srv_sendmsg(srvproc, SRV_MSG_ERROR, XP_ERROR_NUMBER, SRV_INFO, 1,  
                NULL, 0, __LINE__,   
                multibyteErrorMessage,  
                SRV_NULLTERM);  
  
        srv_senddone(srvproc, (SRV_DONE_ERROR | SRV_DONE_MORE), 0, 0);  
  
        return 1;  
    }  
  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [扩展存储过程 API srv_wsendmsg &#40;&#41;](../../relational-databases/extended-stored-procedures-reference/srv-wsendmsg-extended-stored-procedure-api.md)  
  
  
