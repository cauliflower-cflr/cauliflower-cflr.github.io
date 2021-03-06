---
title: Unoptimised Dynamic Dispatch (virtual)
layout: post
---

Points-to with dynamic dispatch semantics, using an accurate virtual-dispatch model.
Callsite-method linking occus if the receiver variable points-to .n object of a type that defines (or uses) this method.
This schematic is un-optimised, and is used to demonstrate how the optimiser creates an efficient specification from this much simpler one.

```
Actual [index]  <- vari . site;
Alloc           <- vari . heap;
AllocType       <- heap . type;
Assign          <- vari . vari;
Definer [desc]  <- type . meth;
Formal [index]  <- vari . meth;
Load [field]    <- vari . vari;
Receiver [desc] <- vari . site;
ReturnCallsite  <- vari . site;
ReturnMethod    <- vari . meth;
Store [field]   <- vari . vari;

VPT             <- vari . heap;

VPT -> Alloc;
VPT -> Assign, VPT;
VPT -> -Load[f], VPT, -VPT, -Store[f], VPT;
VPT -> Formal[i], -Definer[d], -AllocType, -VPT, Receiver[d], -Actual[i], VPT;
VPT -> ReturnCallsite, -Receiver[d], VPT, AllocType, Definer[d], -ReturnMethod, VPT;
```
