Three components which affect the output volume are be stride, filter and zero padding.
---
**Zero Padding** will be virtualize border to make the loss of data less.
**Stride** is the step used when sliding the filter over the input data.
**filter** is a unit of output data. (=receptive field)

The output volume will be (w - f ) s + 1 or (w - f + 2p) / s , since the padding is optional
