---
title: 自定义密钥存储提供程序 |Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a6166d7d-ef34-4f87-bd1b-838d3ca59ae7
ms.author: v-chojas
manager: craigg
author: MightyPen
ms.openlocfilehash: 59a1458c98fb12f2f053bfd71649f40ddc5d1e4e
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2019
ms.locfileid: "55047211"
---
# <a name="custom-keystore-providers"></a>自定义密钥存储提供程序
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>概述

SQL Server 2016 的列加密功能要求的客户端检索，然后才能访问加密列中存储的数据解密列加密密钥 (Cek) 加密列加密密钥 (ECEKs) 存储在服务器上。 ECEKs 进行加密的列主密钥 (Cmk) 和 CMK 的安全性非常重要的列加密安全性。 因此，应 CMK 存储在安全的位置;列加密密钥存储提供程序的用途是提供一个接口以使 ODBC 驱动程序，用于安全地访问这些存储 Cmk。 对于具有安全存储用户，自定义密钥存储提供程序接口提供了一个框架，用于实现安全的 ODBC 驱动程序，然后用于执行 CEK 加密和解密的 CMK 存储的访问权限。

每个密钥存储提供程序包含和管理一个或多个 Cmk，由密钥路径的字符串格式的标识提供程序定义。 此操作，以及加密算法，也是由提供程序，定义的字符串可用来执行 CEK 的加密和解密的 ECEK。 该算法，以及 ECEK 和提供程序名称存储在数据库的加密元数据;请参阅[CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)并[CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md)有关详细信息。 因此，密钥管理的两个基本操作包括：

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

其中`CEKeystoreProvider_name`用于标识特定列加密密钥存储提供程序 (CEKeystoreProvider)，而其他参数供 CEKeystoreProvider，用于加密/解密 (E) CEK。 CEK 元数据提供的算法和 ECEK 值时，是由 CMK 元数据，提供名称和 keypath。 多个密钥存储提供程序可能与默认的内置提供程序一起出现。 后执行一个操作，它需要该 CEK，驱动程序使用的 CMK 元数据以查找相应的密钥存储提供程序名称，并执行其解密操作，可以表示为：

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

尽管该驱动程序都具有无需使用来加密 Cek，密钥管理工具可能需要这样做才能实现操作，如 CMK 创建和旋转。这需要执行的反向操作：

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>CEKeyStoreProvider 接口

本文档详细介绍了 CEKeyStoreProvider 接口。 实现此接口的密钥存储提供程序可供 SQL Server Microsoft ODBC 驱动程序。 CEKeyStoreProvider 实施者可以使用本指南来开发自定义密钥存储提供程序可用驱动程序。

密钥存储提供程序库 （"提供程序库"） 是一个动态链接库，它可以加载 ODBC 驱动程序，并包含一个或多个密钥存储提供程序。 符号`CEKeystoreProvider`必须导出由提供程序库，并且是以 null 结尾的指针数组的地址`CEKeystoreProvider`结构，一个用于库中的每个密钥存储提供程序。

一个`CEKeystoreProvider`结构定义的单个密钥存储提供程序的入口点：

```
typedef struct CEKeystoreProvider {
    wchar_t *Name;
    int (*Init)(CEKEYSTORECONTEXT *ctx, errFunc *onError);
    int (*Read)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int *len);
    int (*Write)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len);
    int (*DecryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *ecek,
                        unsigned short ecekLen,
                        unsigned char **cekOut,
                        unsigned short *cekLen);
    int (*EncryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *cek,
                        unsigned short cekLen,
                        unsigned char **ecekOut,
                        unsigned short *ecekLen);
    void (*Free)();
} CEKEYSTOREPROVIDER;
```

|字段名|描述|
|:--|:--|
|`Name`|密钥存储提供程序的名称。 它不能与其他任何密钥存储提供程序以前加载的驱动程序或此库中存在相同。 以 null 结尾、 宽-字符 * 字符串。|
|`Init`|初始化函数。 如果不需要初始化函数，则此字段可能为 null。|
|`Read`|提供程序读取函数。 可以为 null，如果不是必需的。|
|`Write`|提供程序写函数。 所需读取是否不为 null。 可以为 null，如果不是必需的。|
|`DecryptCEK`|ECEK 解密函数。 此函数是密钥存储提供程序，存在的原因，不能为 null。|
|`EncryptCEK`|CEK 加密函数。 该驱动程序不会调用此函数，但它允许以编程方式访问 ECEK 创建由提供密钥管理工具。 可以为 null，如果不是必需的。|
|`Free`|终止函数。 可以为 null，如果不是必需的。|

除了免费，所有此接口中的函数具有的参数，对**ctx**并**onError**。 前者标识在其中调用函数，而后者用于报告错误的上下文。 请参阅[上下文](#context-association)并[错误处理](#error-handling)下面有关详细信息。

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
提供程序定义的初始化函数的占位符名称。 该驱动程序后立即调用此函数一次，提供程序已加载，但早于第一个请求其执行 ECEK 解密或 Read()/Write() 所需的时间。 使用此函数执行其所需的任何初始化。 

|参数|描述|
|:--|:--|
|`ctx`|[输入]操作上下文。|
|`onError`|[输入]错误报告函数。|
|`Return Value`|返回非零值，指示已成功，或零表示失败。|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

一种提供程序定义通信功能的占位符名称。 当应用程序请求从 （以前编写的到） 提供程序使用 SQL_COPT_SS_CEKEYSTOREDATA 连接属性，允许应用程序从提供程序读取任意数据读取数据时，该驱动程序将调用此函数。 请参阅[与密钥存储提供程序通信](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers)有关详细信息。

|参数|描述|
|:--|:--|
|`ctx`|[输入]操作上下文。|
|`onError`|[输入]错误报告函数。|
|`data`|[输出]提供程序将在其中写入要由应用程序读取数据的缓冲区的指针。 这对应于 CEKEYSTOREDATA 结构的数据字段。|
|`len`|[InOut]指向长度值;在输入，这是数据缓冲区的最大长度和提供程序不应写入多个 * len 字节复制到它。 更新提供程序应在返回时，* len 与实际写入的字节数。|
|`Return Value`|返回非零值，指示已成功，或零表示失败。|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
一种提供程序定义通信功能的占位符名称。 当应用程序请求提供程序时使用 SQL_COPT_SS_CEKEYSTOREDATA 连接属性，允许应用程序将任意数据写入到提供程序写入数据时，驱动程序将调用此函数。 请参阅[与密钥存储提供程序通信](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers)有关详细信息。

|参数|描述|
|:--|:--|
|`ctx`|[输入]操作上下文。|
|`onError`|[输入]错误报告函数。|
|`data`|[输入]指向包含要读取的提供程序的数据的缓冲区的指针。 这对应于 CEKEYSTOREDATA 结构的数据字段。 提供程序不读取此缓冲区中多个 len 字节。|
|`len`|[输入]在数据中可用的字节数。 这对应于 CEKEYSTOREDATA 结构的 dataSize 字段。|
|`Return Value`|返回非零值，指示已成功，或零表示失败。|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
占位符名称的提供程序定义 ECEK 解密函数。 该驱动程序调用此函数来解密 ECEK 由与此提供程序关联到 CEK 的 CMK 加密。

|参数|描述|
|:--|:--|
|`ctx`|[输入]操作上下文。|
|`onError`|[输入]错误报告函数。|
|`keyPath`|[输入]值[KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) CMK 由给定 ECEK 引用的元数据特性。 以 null 终止宽-字符 * 字符串。 这是为了确定此提供程序处理 CMK。|
|`alg`|[输入]值[算法](../../t-sql/statements/create-column-encryption-key-transact-sql.md)给定 ECEK 的元数据特性。 以 null 终止宽-字符 * 字符串。 这是为了识别用于加密给定的 ECEK 的加密算法。|
|`ecek`|[输入]指向要解密的 ECEK 指针。|
|`ecekLen`|[输入]ECEK 的长度。|
|`cekOut`|[输出]提供程序应为已解密的 ECEK 分配内存和指针指向的 cekOut 写入其地址。 它必须是可释放的内存使用此块[LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) 或释放 (Linux/Mac) 函数。 如果没有内存分配因出错而或以其他方式，应设置提供程序 * cekOut 到 null 指针。|
|`cekLen`|[输出]提供程序应写入到由 cekLen 指向的地址已写入到已解密 ECEK 的长度 * * cekOut。|
|`Return Value`|返回非零值，指示已成功，或零表示失败。|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
提供程序定义的 CEK 加密函数的占位符名称。 该驱动程序不会不调用此函数也不会公开其功能通过 ODBC 接口，但它允许以编程方式访问 ECEK 创建由提供密钥管理工具。

|参数|描述|
|:--|:--|
|`ctx`|[输入]操作上下文。|
|`onError`|[输入]错误报告函数。|
|`keyPath`|[输入]值[KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) CMK 由给定 ECEK 引用的元数据特性。 以 null 终止宽-字符 * 字符串。 这是为了确定此提供程序处理 CMK。|
|`alg`|[输入]值[算法](../../t-sql/statements/create-column-encryption-key-transact-sql.md)给定 ECEK 的元数据特性。 以 null 终止宽-字符 * 字符串。 这是为了识别用于加密给定的 ECEK 的加密算法。|
|`cek`|[输入]指向要加密的 CEK。|
|`cekLen`|[输入]CEK 的长度。|
|`ecekOut`|[输出]提供程序应为加密的 CEK 分配内存和指针指向的 ecekOut 写入其地址。 它必须是可释放的内存使用此块[LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) 或释放 (Linux/Mac) 函数。 如果没有内存分配因出错而或以其他方式，应设置提供程序 * ecekOut 到 null 指针。|
|`ecekLen`|[输出]提供程序应写入到由 ecekLen 指向的地址已写入到加密的 CEK 的长度 * * ecekOut。|
|`Return Value`|返回非零值，指示已成功，或零表示失败。|

```
void (*Free)();
```
提供程序定义的终止函数的占位符名称。 驱动程序可能会调用此函数的过程的正常终止。

> [!NOTE]
> *宽字符字符串是由于 SQL Server 如何存储它们的 2 字节字符 (utf-16)。*


### <a name="error-handling"></a>错误处理

在提供程序的处理过程中出错可能时，提供了一个机制以允许其以比布尔成功/失败的更详细地返回到该驱动程序报告错误。 许多函数具有参数，对**ctx**并**onError**，其中实现此目的除了成功/失败的返回值一起使用。

**Ctx**参数标识提供程序操作发生的上下文。

**OnError**参数指向错误报告函数，用下列原型：

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|参数|描述|
|:--|:--|
|`ctx`|[输入]要在报告错误的上下文。|
|`msg`|[输入]报告错误消息。 以 null 结尾的宽字符字符串。 若要允许参数化的信息必须存在，此字符串可包含的窗体接受的格式插入设置序列[FormatMessage](/windows/desktop/api/winbase/nf-winbase-formatmessage)函数。 可通过此参数指定扩展的功能，如下所述。|
|...|[输入]中容纳不下的格式说明符消息，根据需要的其他可变参数参数。|

若要报告时出现错误，提供程序调用 onError，提供的上下文参数传递到提供程序函数按该驱动程序和可选的其他参数的错误消息要在其中设置格式。 提供程序可能会调用此函数多次发布连续在一个提供程序函数调用中的多条错误消息。 例如：

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


`msg`参数通常是宽字符字符串，但提供了其他扩展：

通过使用特殊的预定义值之一与 IDS_MSG 宏已存在的一般性错误消息和驱动程序中本地化的窗体中可能被利用。 例如，如果提供程序无法分配内存，`IDS_S1_001`可以使用"内存分配失败"消息：

`onError(ctx, IDS_MSG(IDS_S1_001));`

若要识别驱动程序错误，提供程序函数必须返回失败。 后 ODBC 操作的上下文中执行此操作，将通过标准 ODBC 诊断机制的连接或语句句柄上可访问已发布的错误 (`SQLError`， `SQLGetDiagRec`，和`SQLGetDiagField`)。


### <a name="context-association"></a>上下文关联

`CEKEYSTORECONTEXT`结构，除了提供上下文的错误回调，还可以用于确定在其中执行提供程序操作的 ODBC 上下文。 这允许提供程序，例如将关联到每个这些上下文中，数据以实现每个连接配置。 为此，该结构包含 3 个与环境、 连接和语句上下文相对应的不透明指针：

```
typedef struct CEKeystoreContext
{
void *envCtx;
void *dbcCtx;
void *stmtCtx;
} CEKEYSTORECONTEXT;
```

|字段|描述|
|:--|:--|
|`envCtx`|环境上下文。|
|`dbcCtx`|连接上下文。|
|`stmtCtx`|语句上下文。|

这些上下文中的每个都是一个不透明值，同时与相应的 ODBC 句柄，可以使用该唯一标识符作为为句柄： 如果处理*X*与上下文值相关联*Y*，然后任何其他环境、 连接或语句句柄在作为同一时间同时存在*X*上下文值为*Y*，和与相关的任何其他上下文值处理*X*。如果提供程序操作中的完成过程中没有特定的句柄上下文，（例如 SQLSetConnectAttr 调用以加载和配置提供程序，这样就没有语句句柄） 的相应结构中的上下文值为 null。


## <a name="example"></a>示例

### <a name="keystore-provider"></a>密钥存储提供程序

以下代码是最小密钥存储提供程序实现的示例。

```
/* Custom Keystore Provider Example

Windows:   compile with cl MyKSP.c /LD /MD /link /out:MyKSP.dll
Linux/Mac: compile with gcc -fshort-wchar -fPIC -o MyKSP.so -shared MyKSP.c

 */

#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#endif

#include <stdlib.h>
#include <sqltypes.h>
#include "msodbcsql.h"
#include <sql.h>
#include <sqlext.h>

int __stdcall KeystoreInit(CEKEYSTORECONTEXT *ctx, errFunc *onError) {
    printf("KSP Init() function called\n");
    return 1;
}

static unsigned char *g_encryptKey;
static unsigned int g_encryptKeyLen;

int __stdcall KeystoreWrite(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len) {
    printf("KSP Write() function called (%d bytes)\n", len);
    if (len) {
        if (g_encryptKey)
            free(g_encryptKey);
        g_encryptKey = malloc(len);
        if (!g_encryptKey) {
            onError(ctx, L"Memory Allocation Error");
            return 0;
        }
        memcpy(g_encryptKey, data, len);
        g_encryptKeyLen = len;
    }
    return 1;
}

// Very simple "encryption" scheme - rotating XOR with the key
int __stdcall KeystoreDecrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg,
    unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen) {
    unsigned int i;
    printf("KSP Decrypt() function called (keypath=%S alg=%S ecekLen=%u)\n", keyPath, alg, ecekLen);
    if (wcscmp(keyPath, L"TheOneAndOnlyKey")) {
        onError(ctx, L"Invalid key path");
        return 0;
    }
    if (wcscmp(alg, L"none")) {
        onError(ctx, L"Invalid algorithm");
        return 0;
    }
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
#ifndef _WIN32
    *cekOut = malloc(ecekLen);
#else
    *cekOut = LocalAlloc(LMEM_FIXED, ecekLen);
#endif
    if (!*cekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *cekLen = ecekLen;
    for (i = 0; i < ecekLen; i++)
        (*cekOut)[i] = ecek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

// Note that in the provider interface, this function would be referenced via the CEKEYSTOREPROVIDER
// structure. However, that does not preclude keystore providers from exporting their own functions,
// as illustrated by this example where the encryption is performed via a separate function (with a
// different prototype than the one in the KSP interface.)
#ifdef _WIN32
__declspec(dllexport)
#endif
int KeystoreEncrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError,
    unsigned char *cek, unsigned short cekLen,
    unsigned char **ecekOut, unsigned short *ecekLen) {
    unsigned int i;
    printf("KSP Encrypt() function called (cekLen=%u)\n", cekLen);
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
    *ecekOut = malloc(cekLen);
    if (!*ecekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *ecekLen = cekLen;
    for (i = 0; i < cekLen; i++)
        (*ecekOut)[i] = cek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

CEKEYSTOREPROVIDER MyCustomKSPName_desc = {
    L"MyCustomKSPName",
    KeystoreInit,
    0,
    KeystoreWrite,
    KeystoreDecrypt,
    0
};

#ifdef _WIN32
__declspec(dllexport)
#endif
CEKEYSTOREPROVIDER *CEKeystoreProvider[] = {
    &MyCustomKSPName_desc,
    0
};
```

### <a name="odbc-application"></a>ODBC 应用程序

下面的代码是一个演示应用程序，它使用更高版本的密钥存储提供程序。 当运行它，确保提供程序库是与应用程序二进制文件，同一目录中并确保连接字符串指定 （或指定的 DSN，其中包含）`ColumnEncryption=Enabled`设置。

```
/*
 Example application for demonstration of custom keystore provider usage

Windows:   compile with cl /MD kspapp.c /link odbc32.lib
Linux/Mac: compile with gcc -o kspapp -fshort-wchar kspapp.c -lodbc -ldl
 
 usage: kspapp connstr

 */

#define KSPNAME L"MyCustomKSPName"
#define PROV_ENCRYPT_KEY "JHKCWYT06N3RG98J0MBLG4E3"

#include <stdio.h>
#include <stdlib.h>
#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#include <dlfcn.h>
#endif
#include <sql.h>
#include <sqlext.h>
#include "msodbcsql.h"

/* Convenience functions */

int checkRC(SQLRETURN rc, char *msg, int ret, SQLHANDLE h, SQLSMALLINT ht) {
    if (rc == SQL_ERROR) {
        fprintf(stderr, "Error occurred upon %s\n", msg);
        if (h) {
            SQLSMALLINT i = 0;
            SQLSMALLINT outlen = 0;
            char errmsg[1024];
            while ((rc = SQLGetDiagField(
                ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
                || rc == SQL_SUCCESS_WITH_INFO) {
                fprintf(stderr, "Err#%d: %s\n", i, errmsg);
            }
        }
        if (ret)
            exit(ret);
        return 0;
    }
    else if (rc == SQL_SUCCESS_WITH_INFO && h) {
        SQLSMALLINT i = 0;
        SQLSMALLINT outlen = 0;
        char errmsg[1024];
        printf("Success with info for %s:\n", msg);
        while ((rc = SQLGetDiagField(
            ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
            || rc == SQL_SUCCESS_WITH_INFO) {
            fprintf(stderr, "Msg#%d: %s\n", i, errmsg);
        }
    }
    return 1;
}

void postKspError(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...) {
    if (msg > (wchar_t*)65535)
        wprintf(L"Provider emitted message: %s\n", msg);
    else
        wprintf(L"Provider emitted message ID %d\n", msg);
}

int main(int argc, char **argv) {
    char sqlbuf[1024];
    SQLHENV env;
    SQLHDBC dbc;
    SQLHSTMT stmt;
    SQLRETURN rc;
    unsigned char CEK[32];
    unsigned char *ECEK;
    unsigned short ECEKlen;
#ifdef _WIN32
    HMODULE hProvLib;
#else
    void *hProvLib;
#endif
    CEKEYSTORECONTEXT ctx = {0};
    CEKEYSTOREPROVIDER **ppKsp, *pKsp;
    int(__stdcall *pEncryptCEK)(CEKEYSTORECONTEXT *, errFunc *, unsigned char *, unsigned short, unsigned char **, unsigned short *);
    int i;
    if (argc < 2) {
        fprintf(stderr, "usage: kspapp connstr\n");
        return 1;
    }

    /* Load the provider library */
#ifdef _WIN32
    if (!(hProvLib = LoadLibrary("MyKSP.dll"))) {
#else
    if (!(hProvLib = dlopen("./MyKSP.so", RTLD_NOW))) {
#endif
        fprintf(stderr, "Error loading KSP library\n");
        return 2;
    }
#ifdef _WIN32
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)GetProcAddress(hProvLib, "CEKeystoreProvider"))) {
#else
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)dlsym(hProvLib, "CEKeystoreProvider"))) {
#endif
        fprintf(stderr, "The export CEKeystoreProvider was not found in the KSP library\n");
        return 3;
    }
    while (pKsp = *ppKsp++) {
        if (!memcmp(KSPNAME, pKsp->Name, sizeof(KSPNAME)))
            goto FoundProv;
    }
    fprintf(stderr, "Could not find provider in the library\n");
    return 4;
FoundProv:
    if (pKsp->Init && !pKsp->Init(&ctx, postKspError)) {
        fprintf(stderr, "Could not initialize provider\n");
        return 5;
    }
#ifdef _WIN32
    if (!(pEncryptCEK = (LPVOID)GetProcAddress(hProvLib, "KeystoreEncrypt"))) {
#else
    if (!(pEncryptCEK = dlsym(hProvLib, "KeystoreEncrypt"))) {
#endif
        fprintf(stderr, "The export KeystoreEncrypt was not found in the KSP library\n");
        return 6;
    }
    if (!pKsp->Write) {
        fprintf(stderr, "Provider does not support configuration\n");
        return 7;
    }

    /* Configure the provider with the key */
    if (!pKsp->Write(&ctx, postKspError, PROV_ENCRYPT_KEY, strlen(PROV_ENCRYPT_KEY))) {
        fprintf(stderr, "Error writing to KSP\n");
        return 8;
    }

    /* Generate a CEK and encrypt it with the provider */
    srand(time(0) ^ getpid());
    for (i = 0; i < sizeof(CEK); i++)
        CEK[i] = rand();

    if (!pEncryptCEK(&ctx, postKspError, CEK, sizeof(CEK), &ECEK, &ECEKlen)) {
        fprintf(stderr, "Error encrypting CEK\n");
        return 9;
    }

    /* Connect to Server */
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &env);
    checkRC(rc, "allocating environment handle", 2, 0, 0);
    rc = SQLSetEnvAttr(env, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0);
    checkRC(rc, "setting ODBC version to 3.0", 3, env, SQL_HANDLE_ENV);
    rc = SQLAllocHandle(SQL_HANDLE_DBC, env, &dbc);
    checkRC(rc, "allocating connection handle", 4, env, SQL_HANDLE_ENV);
    rc = SQLDriverConnect(dbc, 0, argv[1], strlen(argv[1]), NULL, 0, NULL, SQL_DRIVER_NOPROMPT);
    checkRC(rc, "connecting to data source", 5, dbc, SQL_HANDLE_DBC);
    rc = SQLAllocHandle(SQL_HANDLE_STMT, dbc, &stmt);
    checkRC(rc, "allocating statement handle", 6, dbc, SQL_HANDLE_DBC);

    /* Create a CMK definition on the server */
    {
        static char cmkSql[] = "CREATE COLUMN MASTER KEY CustomCMK WITH ("
            "KEY_STORE_PROVIDER_NAME = 'MyCustomKSPName',"
            "KEY_PATH = 'TheOneAndOnlyKey')";
        printf("Create CMK: %s\n", cmkSql);
        SQLExecDirect(stmt, cmkSql, SQL_NTS);
    }

    /* Create a CEK definition on the server */
    {
        const char cekSqlBefore[] = "CREATE COLUMN ENCRYPTION KEY CustomCEK WITH VALUES ("
            "COLUMN_MASTER_KEY = CustomCMK,"
            "ALGORITHM = 'none',"
            "ENCRYPTED_VALUE = 0x";
        char *cekSql = malloc(sizeof(cekSqlBefore) + 2 * ECEKlen + 2); /* 1 for ')', 1 for null terminator */
        strcpy(cekSql, cekSqlBefore);
        for (i = 0; i < ECEKlen; i++)
            sprintf(cekSql + sizeof(cekSqlBefore) - 1 + 2 * i, "%02x", ECEK[i]);
        strcat(cekSql, ")");
        printf("Create CEK: %s\n", cekSql);
        SQLExecDirect(stmt, cekSql, SQL_NTS);
        free(cekSql);
#ifdef _WIN32
        LocalFree(ECEK);
#else
        free(ECEK);
#endif
    }

#ifdef _WIN32
    FreeLibrary(hProvLib);
#else
    dlclose(hProvLib);
#endif

    /* Create a table with encrypted columns */
    {
        static char *tableSql = "CREATE TABLE CustomKSPTestTable ("
            "c1 int,"
            "c2 varchar(255) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = CustomCEK, ENCRYPTION_TYPE = DETERMINISTIC, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'))";
        printf("Create table: %s\n", tableSql);
        SQLExecDirect(stmt, tableSql, SQL_NTS);
    }

    /* Load provider into the ODBC Driver and configure it */
    {
        unsigned char ksd[sizeof(CEKEYSTOREDATA) + sizeof(PROV_ENCRYPT_KEY) - 1];
        CEKEYSTOREDATA *pKsd = (CEKEYSTOREDATA*)ksd;
        pKsd->name = L"MyCustomKSPName";
        pKsd->dataSize = sizeof(PROV_ENCRYPT_KEY) - 1;
        memcpy(pKsd->data, PROV_ENCRYPT_KEY, sizeof(PROV_ENCRYPT_KEY) - 1);
#ifdef _WIN32
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "MyKSP.dll", SQL_NTS);
#else
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "./MyKSP.so", SQL_NTS);
#endif
        checkRC(rc, "Loading KSP into ODBC Driver", 7, dbc, SQL_HANDLE_DBC);
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREDATA, (SQLPOINTER)pKsd, SQL_IS_POINTER);
        checkRC(rc, "Configuring the KSP", 7, dbc, SQL_HANDLE_DBC);
    }

    /* Insert some data */
    {
        int c1;
        char c2[256];
        rc = SQLBindParameter(stmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 0, 0, &c1, 0, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        rc = SQLBindParameter(stmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_VARCHAR, 255, 0, c2, 255, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        for (i = 0; i < 10; i++) {
            c1 = i * 10 + i + 1;
            sprintf(c2, "Sample data %d for column 2", i);
            rc = SQLExecDirect(stmt, "INSERT INTO CustomKSPTestTable (c1, c2) values (?, ?)", SQL_NTS);
            checkRC(rc, "Inserting rows query", 10, stmt, SQL_HANDLE_STMT);
        }
        printf("(Encrypted) data has been inserted into the [CustomKSPTestTable]. You may inspect the data now.\n"
            "Press Enter to continue...\n");
        getchar();
    }

    /* Retrieve the data */
    {
        int c1;
        char c2[256];
        rc = SQLBindCol(stmt, 1, SQL_C_LONG, &c1, 0, 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLBindCol(stmt, 2, SQL_C_CHAR, c2, sizeof(c2), 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLExecDirect(stmt, "SELECT c1, c2 FROM CustomKSPTestTable", SQL_NTS);
        checkRC(rc, "Retrieving rows query", 12, stmt, SQL_HANDLE_STMT);
        while (SQL_SUCCESS == (rc = SQLFetch(stmt)))
            printf("Retrieved data: c1=%d c2=%s\n", c1, c2);
        SQLFreeStmt(stmt, SQL_CLOSE);
        printf("Press Enter to clean up and exit...\n");
        getchar();
    }

    /* Clean up */
    {
        SQLExecDirect(stmt, "DROP TABLE CustomKSPTestTable", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN ENCRYPTION KEY CustomCEK", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN MASTER KEY CustomCMK", SQL_NTS);
        printf("Removed table, CEK, and CMK\n");
    }
    SQLDisconnect(dbc);
    SQLFreeHandle(SQL_HANDLE_DBC, dbc);
    SQLFreeHandle(SQL_HANDLE_ENV, env);
    return 0;
}

```

## <a name="see-also"></a>另请参阅

[对 ODBC 驱动程序使用 Always Encrypted](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
