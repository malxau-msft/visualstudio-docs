---
title: Perf insights for ConcurrentDictionary.Keys
description: Learn how to improve performance for ConcurrentDictionary.Keys.
ms.date: 06/19/2023
ms.topic: reference
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.subservice: debug-diagnostics
---

# Slow ConcurrentDictionary.Keys lookup

This article describes performance insights for <xref:System.Collections.Concurrent.ConcurrentDictionary%602.Keys%2A?displayProperty=nameWithType>.

## Cause

`System.Collections.Concurrent.ConcurrentDictionary.Keys` is resulting in a slow lookup.

## Performance insight description

`ConcurrentDictionary.Keys` takes a lock and makes a read-only copy of the list of keys. Enumerating the key-value pairs can be more efficient in many circumstances because it avoids locking the entire collection to copy all of the keys.

If you need to use lots of `ConcurrentDictionary.Keys` method calls, for example, one per request, do not use the default constructor, and instead use a constructor that allows you to specify the concurrency value. The default constructor uses concurrency level equal to the number of cores on the box. Use a smaller number as the concurrency level instead, and then check the overall memory usage.

If you don't need to consider thread-safety, `ConcurrentDictionary` can be more costly than `Dictionary`. So check whether you need to use `ConcurrentDictionary`.

## How to investigate a warning

In the CPU Usage tool, click **View source code** to go to the [call tree](../profiling/cpu-usage.md#BKMK_Call_tree_structure) and source line highlighting view, which shows where the most amount of time is spent in `ConcurrentDictionary.Keys`. From this point, trace back to where the method is used and check whether you can enumerate the key-value pairs instead.

## See also

[Identify hot paths with Flame Graph](../profiling/flame-graph.md)
