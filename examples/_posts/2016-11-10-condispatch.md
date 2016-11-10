---
title: Unoptimised Dynamic Dispatch (conservative)
layout: post
---

An over-approximation of points-to with dynamic dispatch semantics.
Callsite-method linking occus if the declared type of the receiver is a super-type of the method's class.
This schematic is un-optimised, and is used to demonstrate how the optimiser creates an efficient specification from this much simpler one.

```
Actual [index]  <- vari . site;
Alloc           <- vari . heap;
Assign          <- vari . vari;
Definer [desc]  <- type . meth;
Formal [index]  <- vari . meth;
Load [field]    <- vari . vari;
Receiver [desc] <- vari . site;
ReflexSubclass  <- type . type;
ReturnCallsite  <- vari . site;
ReturnMethod    <- vari . meth;
Store [field]   <- vari . vari;
VarType         <- vari . type;

VPT             <- vari . heap;

VPT -> Alloc;
VPT -> Assign, VPT;
VPT -> -Load[f], VPT, -VPT, -Store[f], VPT;
VPT -> Formal[i], -Definer[d], ReflexSubclass, -VarType, Receiver[d], -Actual[i], VPT;
VPT -> ReturnCallsite, -Receiver[d], VarType, -ReflexSubclass, Definer[d], -ReturnMethod, VPT;
```
