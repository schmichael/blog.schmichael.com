---
title: Why I hate Microsoft Office
author: Michael Schurter
layout: post
date: 2005-08-03
url: /2005/08/03/why-i-hate-microsoft-office/
dsq_thread_id:
  - 463869737
categories:
  - IT
tags:
  - Synthesys

---
Someone at an organization I consult at received an &#8220;Out of Memory&#8221; error when attempting to copy and paste a chart in Microsoft Excel 97. After attempting the resolution methods from [&#8220;Mr. Excel&#8221;][1] and [a MS KnowledgeBase article][2], the error persisted.

Then I read [this interesting page][3] on Excel memory issues, which led me to the conclusion that Microsoft Excel is a horrifically buggy application. I wonder if [OpenOffice.org][4] suffers from similar ridiculous memory limitations&#8230; I&#8217;ve never had any problems with OOo Calc, but then again my spreadsheets are usually fairly simple (less than 6 sheets with less than a dozen charts).

Oh, and I hate Microsoft&#8217;s complete abuse of MDI window behavior in Office as well. Just needed to get that in there. 😉

**Update:** After upgrading the user received a new error whenever he attempted to copy and paste charts: &#8220;No more new fonts may be applied in this workbook.&#8221; Luckily Microsoft is nice enough to cover this in a [Knowledge Base Article][5]. Of course it didn&#8217;t work&#8230; &#8230;until I noticed the user had about half a dozen hidden charts underneath every visible chart! Deleting the hidden charts and applying the suggested resolution from the KB article finally got it working.

More importantly: **OOo Calc opened the file beautifully and was able to copy and paste just fine.** (This isn&#8217;t the first time I&#8217;ve had OOo handle MS Office files better than Office!)

 [1]: http://www.mrexcel.com/archive/Errors/20970.html
 [2]: http://support.microsoft.com/default.aspx?scid=kb;EN-US;Q168650
 [3]: http://www.decisionmodels.com/memlimitsc.htm
 [4]: http://www.openoffice.org
 [5]: http://support.microsoft.com/default.aspx?scid=kb;en-us;215573