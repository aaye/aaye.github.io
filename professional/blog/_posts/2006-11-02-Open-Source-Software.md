---
layout: blogpost
title: Open Source Software
date: 2006-11-02
categories: [coding,oss]
---
While I am not quite an anti-evangelist for open source software, I find that whenever I look in that direction for possible solution the source itself is an illegible mess of incoherent and often badly verified code. My current project is to get a working XML processor into the main build so that I can use an XML based system for the data files, and I can then hook it into the collada system for processing of those files. I opted to go with LibXML2 since it was rated very high in terms of development and standards compliance. I did not realize at the time that making that decision was akin to deciding to go into an iron maiden because it looked like it was engineered very well using very sharp and good quality steel. Oops, my mistake! The code base has slowly been driving me nuts, having an almost haphazard approach to pointer arithmetic and variable size definitions. The common belief that sizeof(void*) == sizeof(int) is enough to drive someone trying to get code working on x64 architecture around the bend. This little side project is definitely gonna take me a couple more days to complete, so until then - adieu
