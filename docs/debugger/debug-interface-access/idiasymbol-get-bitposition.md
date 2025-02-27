---
description: "Retrieves the bit position of location."
title: "IDiaSymbol::get_bitPosition"
ms.date: "11/04/2016"
ms.topic: "reference"
dev_langs:
  - "C++"
helpviewer_keywords:
  - "IDiaSymbol::get_bitPosition method"
author: "mikejo5000"
ms.author: "mikejo"
manager: jmartens
ms.subservice: debug-diagnostics
---
# IDiaSymbol::get_bitPosition

Retrieves the bit position of location. Used when the [LocationType Enumeration](../../debugger/debug-interface-access/locationtype.md) is `LocIsBitField`.

## Syntax

```C++
HRESULT get_bitPosition ( 
   DWORD* pRetVal
);
```

#### Parameters
 `pRetVal`

[out] Returns the bit position of the location.

## Return Value
 If successful, returns `S_OK`; otherwise, returns `S_FALSE` or error code.

> [!NOTE]
> A return value of `S_FALSE` means the property is not available for the symbol.

## Requirements

|Requirement|Description|
|-----------------|-----------------|
|Header:|dia2.h|
|Version:|DIA SDK v7.0|

## See also
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType Enumeration](../../debugger/debug-interface-access/locationtype.md)
