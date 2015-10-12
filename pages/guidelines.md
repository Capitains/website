---
layout: page
title: "Guidelines"
heahder: "Guidelines"
group: navigation
description: ""
---
{% include JB/setup %}

**Index :**

* TOC
{:toc}
- Resources 
    - [Ant Build.xml Example](build.html)
    - [eXistDB collection.xconf Example](xconf.html)


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
    <citation label="Book" xpath="/tei:div1[@n='?']" scope="/tei:TEI/tei:text/tei:body">
        <citation label="Line" xpath="//tei:l[@n='?']"
            scope="/tei:TEI/tei:text/tei:body/tei:div1[@n='?']"/>
    </citation>
</citationMapping>
{% endhighlight %}

And as CREF

{% highlight xml %}
<refsDecl n="CTS">
 <cRefPattern 
   n="line"
   matchPattern="(.+).(.+)"
   replacementPattern="#xpath(/tei:TEI/tei:text/tei:body/tei:div[@n='$1']//tei:l[@n='$2'])">
  <p>This pointer pattern extracts book and line</p>
 </cRefPattern>
 <cRefPattern 
   n="book"
   matchPattern="(.+)"
   replacementPattern="#xpath(/tei:TEI/tei:text/tei:body/tei:div[@n='$1'])">
  <p>This pointer pattern extracts book.</p>
 </cRefPattern>
</refsDecl>
{% endhighlight %}

As you see, the `@replacementPattern` is an xpath, using $1 to represent the information required to identify an element. The `@matchPattern` simply follows the CTS citation system (*ie* 1.pr.2). Finally, `@n` provides the future inventory informations about the label of the citation (*ie* line, life, book, poem, section, etc.)

###Urn informations

The guidelines are quite simple regarding the urn information. As the CTS Inventory requires to include the online path to an element (`//(ti:edition|ti:translation)/ti:online/@docname`), the solution to avoid any relative or software specific issue is to give the original file the urn reference.

To do so, for TEI files (which are the only one supported right now by the tool suite), there is two different recommendations :

1. If the text is epidoc, the convention is to set it in the following xpath : `TEI/text/body/div[@type="edition"]/@n` 
2. If the text is plain TEI, the convention is to set it in the following xpath : `TEI/text/@n`

###Epidoc or TEI ?

*Big discussion to happen here*

## CTS Package

### Directory naming conventions

Even if it is not strictly required, the directory and files should be named according to the following convention :

{% highlight xml %}
data/
    |- textgroup
        |- work
            |- full-urn.xml
{% endhighlight %}

Which would give for a translation and an edition of the Illiad, and Martial's Epigrammata and Liber de Spectaculis :

{% highlight xml %}
data/
    |- phi1294
        |- phi001
            |- phi1294.phi001.perseus-lat2.xml
        |- phi002
            |- phi1294.phi002.perseus-lat2.xml
    |- tlg0012
        |- tlg001
            |- tlg0012.tlg001.perseus-grc1.xml
            |- tlg0012.tlg001.perseus-eng2.xml
{% endhighlight %}

### CTS Inventory Metadata for file

To build and to have an easy maintenance, the choice was made to cut inventory files into metadata files, which can be used then in the InventoryMaker to create inventory for the API. Each semantic level of folder (*ie* phi1294, phi001...) must contain a file name `__cts__.xml`.

#### Textgroup \_\_cts\_\_.xml 

{% highlight xml %}
<ti:textgroup xmlns:ti="http://chs.harvard.edu/xmlns/cts" urn="urn:cts:latinLit:phi1294">
    <ti:groupname xml:lang="eng">Martial</ti:groupname>
    <ti:groupname xml:lang="lat">Marcus Valerius Martialis</ti:groupname>
</ti:textgroup>
{% endhighlight %}

*Note : * Obviously, you don't need to put Latin or whatever translation of the groupname. We just wanted to show you it's possible. It's actually possible for every `@xml:lang` enable tag.

#### Work \_\_cts\_\_.xml 

{% highlight xml %}
<ti:work xmlns:ti="http://chs.harvard.edu/xmlns/cts" groupUrn="urn:cts:latinLit:phi1294" urn="urn:cts:latinLit:phi1294.phi002">
    <ti:title xml:lang="eng">Epigrammata</ti:title>
    <!-- For each "text", either edition or translation, there should be a ti:edition or ti:translation node -->
    <ti:edition workUrn="urn:cts:latinLit:phi1294.phi002" urn="urn:cts:latinLit:phi1294.phi002.perseus-lat2">
        <ti:label xml:lang="eng">Epigrammata</ti:label>
        <ti:description xml:lang="eng">
            M. Valerii Martialis Epigrammaton libri / recognovit W. Heraeus
        </ti:description>
        <!-- 
            As you can see, there is no <online /> tag here.
            Simply because they are environment dependant.
            And so they are generated upon full inventory generation, hence the cRefPattern convention
        -->
    </ti:edition>
    <ti:translation workUrn="urn:cts:latinLit:phi1294.phi002" urn="urn:cts:latinLit:phi1294.phi002.perseus-eng2">
        <ti:label xml:lang="eng">Epigrammata</ti:label>
        <ti:description xml:lang="eng">Nice translations informations</ti:description>
    </ti:translation>
</ti:work>
{% endhighlight %}

### Packaging for eXistDB install

While it's not necessary to use eXistDB, relying on it might help you as it is fully compliant with every xQuery app we have been developping for now. Our tools are focused on that right now, and we are happy to see developers expand their compatibility with other native xml database such as MarkLogic or BaseX.

There is a simple way to generate your package : eXistDB's eXide app. You can see a tutorial in the [Tutorial tab](../tutorial.html). Once you have done that, just change the build.xml according to the one available on this [page](build.html) and replace or create the collection.xconf file [with this skeletton](xconf.md)

Put your xml resources in the data folder, do a `ant build` at the root of your repository : You are ready for eXistDB tools !