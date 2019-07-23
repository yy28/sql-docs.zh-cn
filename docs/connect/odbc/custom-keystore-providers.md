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
author: MightyPen
ms.openlocfilehash: 0cf2946517be732094d01ff9889faf080a36e85b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006492"
---
# <a name="custom-keystore-providers"></a>自定义密钥存储提供程序
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>概述

SQL Server 2016 的列加密功能要求客户端检索服务器上存储的加密列加密密钥 (ECEKs), 然后将其解密为列加密密钥 (Cek), 以便访问存储在加密列中的数据。 ECEKs 是通过列主密钥 (Cmk) 进行加密的, 而 CMK 的安全性对列加密的安全性很重要。 因此, 应将 CMK 存储在安全位置;列加密密钥存储提供程序的目的是提供一个接口, 以允许 ODBC 驱动程序访问这些安全存储的 Cmk。 对于具有自己的安全存储的用户, 自定义密钥存储提供程序接口提供了一个框架, 用于实现对 ODBC 驱动程序的 CMK 的安全存储的访问, 然后可以使用该框架来执行 CEK 加密和解密。

每个密钥存储提供程序包含和管理一个或多个 Cmk, 它们由密钥路径标识, 由提供程序定义的格式的字符串。 此方法连同加密算法, 以及提供程序定义的字符串, 可用于执行 CEK 加密和解密 ECEK。 该算法与提供程序的 ECEK 和名称一起存储在数据库的加密元数据中;有关详细信息, 请参阅[创建列主密钥](../../t-sql/statements/create-column-master-key-transact-sql.md)和[创建列加密密钥](../../t-sql/statements/create-column-encryption-key-transact-sql.md)。 因此, 密钥管理的两个基本操作是:

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

`CEKeystoreProvider_name`其中使用来标识特定的列加密密钥存储提供程序 (CEKeystoreProvider), CEKeystoreProvider 使用其他参数对 (E) CEK 进行加密/解密。 Name 和 keypath 由 CMK 元数据提供, 而算法和 ECEK 值由 CEK 元数据提供。 多个密钥存储提供程序可以与默认的内置提供程序一起存在。 执行需要 CEK 的操作时, 驱动程序会使用 CMK 元数据按名称查找适当的密钥存储提供程序, 并执行其解密操作, 该操作可以表示为:

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

尽管驱动程序无需加密 Cek, 但密钥管理工具可能需要执行此操作才能实现 CMK 创建和旋转等操作;这需要执行反运算:

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>CEKeyStoreProvider 接口

本文档详细介绍了 CEKeyStoreProvider 接口。 实现此接口的密钥存储提供程序可由 Microsoft ODBC Driver for SQL Server 使用。 CEKeyStoreProvider 实施者可以使用本指南来开发可供驱动程序使用的自定义密钥存储提供程序。

密钥存储提供程序库 ("提供程序库") 是一个可通过 ODBC 驱动程序加载的动态链接库, 其中包含一个或多个密钥存储提供程序。 该符号`CEKeystoreProvider`必须由提供程序库导出, 并为指向结构的以`CEKeystoreProvider` null 结尾的指针数组的地址, 每个用于库中的密钥存储提供程序。

`CEKeystoreProvider`结构定义单个密钥存储提供程序的入口点:

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
|`Name`|密钥存储提供程序的名称。 它不得与驱动程序先前加载的任何其他密钥存储提供程序或此库中存在的任何其他密钥存储提供程序相同。 以 Null 结尾的宽字符*字符串。|
|`Init`|初始化函数。 如果初始化函数不是必需的, 则此字段可以为 null。|
|`Read`|提供程序读取函数。 如果不需要, 则可以为 null。|
|`Write`|提供程序写入函数。 如果读取不为 null, 则为必需。 如果不需要, 则可以为 null。|
|`DecryptCEK`|ECEK 解密函数。 此函数是存在密钥存储提供程序的原因, 不能为 null。|
|`EncryptCEK`|CEK 加密函数。 该驱动程序不调用此函数, 但提供它是为了允许以编程方式访问密钥管理工具创建的 ECEK。 如果不需要, 则可以为 null。|
|`Free`|终止函数。 如果不需要, 则可以为 null。|

除了免费外, 此接口中的函数都有一对参数**ctx**和**onError**。 前者标识调用函数的上下文, 而后者用于报告错误。 有关详细信息, 请参阅下面的[上下文](#context-association)和[错误处理](#error-handling)。

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
提供程序定义的初始化函数的占位符名称。 在加载提供程序之后、首次需要它来执行 ECEK 解密或 Read ()/Write () 请求之前, 驱动程序将调用此函数一次。 使用此函数可执行所需的任何初始化。 

|参数|描述|
|:--|:--|
|`ctx`|送操作上下文。|
|`onError`|送错误报告函数。|
|`Return Value`|如果返回非零值以指示失败, 则返回零。|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

提供程序定义的通信函数的占位符名称。 当应用程序请求使用 SQL_COPT_SS_CEKEYSTOREDATA 连接属性从 (以前写入) 的提供程序中读取数据, 并且允许应用程序从提供程序读取任意数据时, 驱动程序将调用此函数。 有关详细信息, 请参阅[与密钥存储提供程序通信](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers)。

|参数|描述|
|:--|:--|
|`ctx`|送操作上下文。|
|`onError`|送错误报告函数。|
|`data`|输出指向缓冲区的指针, 提供程序在此缓冲区中写入要由应用程序读取的数据。 这对应于 CEKEYSTOREDATA 结构的数据字段。|
|`len`|InOut指向长度值的指针;输入后, 这是数据缓冲区的最大长度, 提供程序不应向其写入超过 * 个字节。 返回时, 提供程序应将 * len 更新为实际写入的字节数。|
|`Return Value`|如果返回非零值以指示失败, 则返回零。|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
提供程序定义的通信函数的占位符名称。 当应用程序请求使用 SQL_COPT_SS_CEKEYSTOREDATA 连接特性将数据写入提供程序时, 驱动程序将调用此函数, 这允许应用程序向提供程序写入任意数据。 有关详细信息, 请参阅[与密钥存储提供程序通信](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers)。

|参数|描述|
|:--|:--|
|`ctx`|送操作上下文。|
|`onError`|送错误报告函数。|
|`data`|送指向缓冲区的指针, 该缓冲区包含提供程序要读取的数据。 这对应于 CEKEYSTOREDATA 结构的数据字段。 提供程序不得从此缓冲区读取超过 len 字节。|
|`len`|送数据中可用的字节数。 这对应于 CEKEYSTOREDATA 结构的 dataSize 字段。|
|`Return Value`|如果返回非零值以指示失败, 则返回零。|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
提供者定义的 ECEK 解密函数的占位符名称。 驱动程序调用此函数将与此提供程序关联的 CMK 加密的 ECEK 解密到 CEK。

|参数|描述|
|:--|:--|
|`ctx`|送操作上下文。|
|`onError`|送错误报告函数。|
|`keyPath`|送给定 ECEK 引用的 CMK 的[KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md)元数据特性的值。 以 Null 结尾的宽字符*字符串。 这用于识别此提供程序处理的 CMK。|
|`alg`|送给定 ECEK 的[算法](../../t-sql/statements/create-column-encryption-key-transact-sql.md)元数据特性的值。 以 Null 结尾的宽字符*字符串。 这旨在标识用于加密给定 ECEK 的加密算法。|
|`ecek`|送指向要解密的 ECEK 的指针。|
|`ecekLen`|送ECEK 的长度。|
|`cekOut`|输出提供程序应为解密的 ECEK 分配内存, 并将其地址写入 cekOut 指向的指针。 必须使用[LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) 或 Free (Linux/Mac) 函数来释放此内存块。 如果由于错误或其他原因而未分配内存, 则提供程序应将 * cekOut 设置为 null 指针。|
|`cekLen`|输出提供程序应将写入的地址写入到 cekLen, 并将其写入到 * * cekOut。|
|`Return Value`|如果返回非零值以指示失败, 则返回零。|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
提供程序定义的 CEK 加密函数的占位符名称。 驱动程序不会调用此函数, 也不会通过 ODBC 接口公开其功能, 但提供它是为了允许以编程方式访问密钥管理工具创建的 ECEK。

|参数|描述|
|:--|:--|
|`ctx`|送操作上下文。|
|`onError`|送错误报告函数。|
|`keyPath`|送给定 ECEK 引用的 CMK 的[KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md)元数据特性的值。 以 Null 结尾的宽字符*字符串。 这用于识别此提供程序处理的 CMK。|
|`alg`|送给定 ECEK 的[算法](../../t-sql/statements/create-column-encryption-key-transact-sql.md)元数据特性的值。 以 Null 结尾的宽字符*字符串。 这旨在标识用于加密给定 ECEK 的加密算法。|
|`cek`|送指向要加密的 CEK 的指针。|
|`cekLen`|送CEK 的长度。|
|`ecekOut`|输出提供程序应为加密的 CEK 分配内存, 并将其地址写到 ecekOut 指向的指针。 必须使用[LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) 或 Free (Linux/Mac) 函数来释放此内存块。 如果由于错误或其他原因而未分配内存, 则提供程序应将 * ecekOut 设置为 null 指针。|
|`ecekLen`|输出提供程序应将写入到的地址写入到 ecekLen, 并将其写入到 ecekOut 中。|
|`Return Value`|如果返回非零值以指示失败, 则返回零。|

```
void (*Free)();
```
提供程序定义的终止函数的占位符名称。 此驱动程序可以在进程正常终止时调用此函数。

> [!NOTE]
> *宽字符字符串是2字节字符 (UTF-16), 原因是 SQL Server 如何存储它们。*


### <a name="error-handling"></a>错误处理

当提供程序的处理过程中出现错误时, 提供一种机制, 以允许它以更具体的详细信息将错误报告回驱动程序, 而不是布尔成功/失败。 许多函数都有一对参数**ctx**和**onError**, 它们除了成功/失败返回值外, 还用于此目的。

**Ctx**参数标识提供程序操作在其中发生的上下文。

**OnError**参数使用以下原型指向错误报告函数:

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|参数|描述|
|:--|:--|
|`ctx`|送要报告错误的上下文。|
|`msg`|送要报告的错误消息。 以 Null 结尾的宽字符字符串。 若要允许参数化信息存在, 此字符串可能包含[FormatMessage](/windows/desktop/api/winbase/nf-winbase-formatmessage)函数接受的格式的插入格式序列。 此参数可以指定扩展功能, 如下所述。|
|...|送适用于 msg 中的格式说明符的其他可变参数参数。|

若要在发生错误时进行报告, 提供程序将调用 onError, 同时提供由驱动程序传递给提供程序函数的上下文参数, 并提供一条错误消息, 其中包含可选的其他参数进行格式设置。 提供程序可以多次调用此函数, 以便在一个提供程序函数调用中连续发布多个错误消息。 例如：

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


`msg`参数通常是宽字符字符串, 但可以使用其他扩展:

通过在 IDS_MSG 宏中使用一种特殊的预定义值, 可使用驱动程序中已存在的通用错误消息, 并以本地化形式提供。 例如, 如果提供程序未能分配内存, 则`IDS_S1_001`可以使用 "内存分配失败" 消息:

`onError(ctx, IDS_MSG(IDS_S1_001));`

为了使驱动程序可识别错误, 提供程序函数必须返回失败。 当在 ODBC 操作的上下文中执行此操作时, 已发布的错误将通过标准 ODBC 诊断机制 (`SQLError`、 `SQLGetDiagRec`和`SQLGetDiagField`) 在连接或语句句柄上变为可访问。


### <a name="context-association"></a>上下文关联

除了为错误回调提供上下文外,结构还可用于确定在其中执行提供程序操作的ODBC上下文。`CEKEYSTORECONTEXT` 这允许提供程序将数据关联到其中的每个上下文, 例如实现每个连接的配置。 出于此目的, 该结构包含3个与环境、连接和语句上下文相对应的不透明指针:

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

其中每个上下文都是一个不透明的值, 而不是与相应的 ODBC 句柄相同的值, 它可用作句柄的唯一标识符: 如果 handle *X*与 Context 值*Y*相关联, 则没有其他环境、连接或语句处理的同时存在的与*x*的上下文值为*Y*的情况相同, 并且其他上下文值将与 handle *X*关联。如果要完成的提供程序操作缺少特定的句柄上下文 (例如, SQLSetConnectAttr 调用加载和配置提供程序, 其中没有语句句柄), 则结构中的相应上下文值为 null。


## <a name="example"></a>示例

### <a name="keystore-provider"></a>密钥存储提供程序

下面的代码是最小密钥存储提供程序实现的示例。

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

以下代码是使用以上密钥存储提供程序的演示应用程序。 运行此方法时, 请确保提供程序库与应用程序的二进制文件位于同一目录中, 并且连接字符串指定 (或指定包含的`ColumnEncryption=Enabled` DSN) 设置。

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
