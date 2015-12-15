---
layout: post
title: Eclipse Mars bug in XML Preferences in Linux
---

It seems to be a bug at least in Mars.1 Release (4.5.1) when trying to set the identation size inside XML > XML Files > Editor dialog. It's imposible identation size when ident using spaces is selected. to change that value and by default is 1.

To overcome this issue edit manually he following file in your workspace:
    
    .metadata/.plugins/org.eclipse.core.runtime/.settings/org.eclipse.wst.xml.core.prefs

And add the following line (if you want 4 char for your indentation):
indentationSize=4