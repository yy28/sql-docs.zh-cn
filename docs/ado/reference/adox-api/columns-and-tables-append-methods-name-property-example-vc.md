---
description: 列和表的 Append 方法、Name 属性示例 (VC++)
title: 列和表追加方法、Name 属性示例 (VC + +) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Name property [ADOX], VC++ example
- Append method [ADOX], VC++ example
ms.assetid: 2b6dfef9-bcdf-483d-a164-2fa3ec81a43f
author: rothja
ms.author: jroth
ms.openlocfilehash: 655c1d014f312ae0706b242bb8b108d871bcef3b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440289"
---
# <a name="columns-and-tables-append-methods-name-property-example-vc"></a>列和表的 Append 方法、Name 属性示例 (VC++)
下面的代码演示如何创建新表。  
  
```  
// BeginCreateTableCpp.cpp  
// compile with: /EHsc  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL) ) )  
      return -1;  
  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers.  These are in ADOX namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTable = NULL;  
  
   try {  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
  
      // Open the catalog  
      m_pCatalog->PutActiveConnection("Provider='Microsoft.JET.OLEDB.4.0';data source='c:\\Northwind.mdb';");  
  
      TESTHR(hr = m_pTable.CreateInstance(__uuidof(Table)));  
      m_pTable->PutName("MyTable");  
      m_pTable->Columns->Append("Column1",adInteger,0);  
      m_pTable->Columns->Append("Column2",adInteger,0);  
      m_pTable->Columns->Append("Column3",adVarWChar,50);  
      m_pCatalog->Tables->Append(_variant_t((IDispatch *)m_pTable));  
      printf("Table 'MyTable' is added.\n");  
  
      // Delete the table as this is a demonstration.  
      m_pCatalog->Tables->Delete("MyTable");  
      printf("Table 'MyTable' is deleted.\n");  
   }  
  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
  
   catch(...) {  
      cout << "Error occurred in include files...."<< endl;  
   }  
  
   ::CoUninitialize();  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [Append 列 (追加方法) ](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 表 (追加方法) ](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Name 属性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)
