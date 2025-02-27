---
title: "When Breakpoint Is Hit Dialog Box"
description: Use When Breakpoint is Hit to specify an action on breaking. You can specify that a message be printed, and that execution should continue afterwards.
ms.date: "11/04/2016"
ms.topic: "ui-reference"
f1_keywords:
  - "vs.debug.whenbreakpointishit"
dev_langs:
  - "CSharp"
  - "VB"
  - "FSharp"
  - "C++"
  - "JScript"
  - "SQL"
author: "mikejo5000"
ms.author: "mikejo"
manager: jmartens
ms.subservice: debug-diagnostics
---
# When Breakpoint Is Hit Dialog Box

With this dialog box, you can customize the action that occurs when a breakpoint is hit.

## UIElement List
 **Print a Message**
 Prints a message, using DebuggerDisplay syntax. For more information, see [Using the DebuggerDisplay Attribute](../debugger/using-the-debuggerdisplay-attribute.md).

 This textbox also supports special keywords (such as $ADDRESS) that can be used by themselves or within the curly braces of a DebuggerDisplay expression. The available keywords are listed on the dialog box.

 **Continue Execution**
 This control is enabled only when **Print a Message** is selected. With this control selected, you can use a breakpoint as a tracepoint to trace your program execution, rather than breaking when the location is hit.

## See also
- [Using Breakpoints](../debugger/using-breakpoints.md)
- [Using the DebuggerDisplay Attribute](../debugger/using-the-debuggerdisplay-attribute.md)