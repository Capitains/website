---
layout: page
title: "Guidelines"
heahder: "Guidelines"
group: navigation
description: ""
---
{% include JB/setup %}

*Warning* : The following guidelines ensure that your work will be fully compliant with all resources available in Capitains Tool suite. Most of them are written in regard of Inventory Maker or eXistDB way to package informations.

## General arguments

Ideally, a CTS API implementation should be able to work with both a traditional full CTS inventory, as well as with directory structure conventions, metadata fragments, and the TEI RefsDecl header. There are several reasons for supporting the naming convention/metadata fragment approach:

1. As the number of texts increases, a single large XML file containing the entire inventory becomes unmanageable
2. Texts can be added and removed easily without requiring updates to a master file.
3. It avoids redundancy and duplication of information, particularly with regard to the citation mapping information which should be contained in the TEI XML file anyway.

## TEI Markup

###RefsDecl element


The RefsDecl in the teiHeader of the TEI XML files must accurately represent the canonical citation scheme of the document. If we use the [cRefPattern](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-cRefPattern.html) syntax for this element to define the Xpaths and citation mapping patterns it should allow us to be able to automatically contruct the CTS citationMapping components of the CTS TextInventory for any given text.

Example from [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/SA.html#SACR](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/SA.html#SACR):

{% highlight xml %}
<refsDecl xml:id="biblical">
 <cRefPattern matchPattern="(.+) (.+):(.+)"
  replacementPattern="#xpath(//div[@n='$1']/div[$2]/div[$3])">
  <p>This pointer pattern extracts and references the <q>book,</q>
   <q>chapter,</q> and <q>verse</q> parts of a biblical reference.</p>
 </cRefPattern>
 <cRefPattern matchPattern="(.+) (.+)"
  replacementPattern="#xpath(//div[@n='$1']/div[$2])">
  <p>This pointer pattern extracts and references the <q>book</q> and
  <q>chapter</q> parts of a biblical reference.</p>
 </cRefPattern>
 <cRefPattern matchPattern="(.+)"
  replacementPattern="#xpath(//div[@n='$1'])">
  <p>This pointer pattern extracts and references just the <q>book</q>
     part of a biblical reference.</p>
 </cRefPattern>
</refsDecl>
{% endhighlight %}

So example for e.g. Homer Iliad:

Citation Mapping:

{% highlight xml %}
 <citationMapping>
    <citation label="Book" xpath="/div1[@n='?']" scope="/TEI.2/text/body">
        <citation label="Line" xpath="//l[@n='?']"
            scope="/TEI.2/text/body/div1[@n='?']"/>
    </citation>
</citationMapping>
{% endhighlight %}

And as CREF

{% highlight xml %}
<refsDecl n="CTS">
 <cRefPattern 
   n="line"
   matchPattern="(.+).(.+)"
   replacementPattern="#xpath(/TEI.2/text/body/div[@n='$1']//l[@n='$2'])">
  <p>This pointer pattern extracts book and line</p>
 </cRefPattern>
 <cRefPattern 
   n="book"
   matchPattern="(.+)"
   replacementPattern="#xpath(/TEI.2/text/body/div[@n='$1'])">
  <p>This pointer pattern extracts book.</p>
 </cRefPattern>
</refsDecl>
{% endhighlight %}

As you see, the `@replacementPattern` is an xpath, using $1 to represent the information required to identify an element. The `@matchPattern` simply follows the CTS citation system (*ie* 1.pr.2). Finally, `@n` provides the future inventory informations about the label of the citation (*ie* line, life, book, poem, section, etc.)

###Urn informations

###Epidoc or TEI ?

## CTS Metadata files

## Packaging for easy install