---
description: "Retrieves the virtual table shape symbol identifier of the symbol."
title: "IDiaSymbol::get_virtualTableShapeId"
ms.date: "11/04/2016"
ms.topic: "reference"
dev_langs:
  - "C++"
helpviewer_keywords:
  - "IDiaSymbol::get_virtualTableShapeId method"
author: "mikejo5000"
ms.author: "mikejo"
manager: jmartens
ms.subservice: debug-diagnostics
---
# IDiaSymbol::get_virtualTableShapeId

Retrieves the virtual table shape symbol identifier of the symbol.

## Syntax

```C++
HRESULT get_virtualTableShapeId ( 
   DWORD* pRetVal
);
```

#### Parameters
 `pRetVal`

[out] Returns the virtual table shape symbol ID of the symbol.

## Return Value
 If successful, returns `S_OK`; otherwise, returns `S_FALSE` or an error code.

> [!NOTE]
> A return value of `S_FALSE` means that the property is not available for the symbol.

## Remarks
 The identifier is a unique value created by the DIA SDK to mark all symbols as unique.

## See also
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
