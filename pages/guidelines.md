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


The following guidelines ensure that your work will be fully compliant with all resources available in Capitains Tool suite. If you are not too familiar with CTS, please see the [Vocabulary](/pages/vocabulary.html).

## Forewords

CapiTainS guidelines are the results of years of strugle with Perseus data maintenance. When one maintainer would try to update a typo, it could takes hours and days to update the servers to serve the correct data. In 2013, Perseus took the decision to implement CTS (Canonical Text Services) as a big step towards Linked Open Data. The idea behind the CTS API implementation would be to ideally build a new Perseus on microservices to resolve the maintainability issues it had as well as serve data in a decentralized fashion to external data users.

All implementation of CTS up to CapiTainS' ones were focused principally on technologies that would not implement, in a rather balanced way, scalability and maintanability. While CapiTainS itself does not enforce the use of its own APIs software, the CapiTainS guidelines were built to explicitly state CTS related informations in text files so that it could be reused in different situation, by different softwares with clear metadata information provided.

CTS requires two main component's types, texts and metadata (or inventory information). They provides data consumers with all required informations, from edition informations to textual node, including citation scheme informations. CapiTainS splitted these informations so that the Citation Scheme is an inherent part of the text, using traditional TEI capacities, while all other metadata can be found in separated files. The reasoning behind this split was to allow for separate maintenance of general metadata - used to browse a catalog of texts - and texts metadata such as the citation scheme. Finally, the directory structure of CapiTainS allows a much simpler browsing method for finding, adding, updating resources in a repository:  by separating resources by URN levels, it brings ease of maintenance. 

## Participants 

Bridget Almas and Thibault Clérice are the original developers of these guidelines. A special mention to Michael Gursky who first put the idea out there of this directory structure as well as the metadata splitting.

## CTS URN Choice

URN choice is quite often one of the first question people ask when trying to decided wether or not CTS is good for them, and it often feels to us that it prevents people to actually adopt the standard. Here is a list of language with recommandations for your language choice. If you want to provide 

| ISO 639-2 | Language | Type of text | Recommandation |
|-----------|----------|--------------|----------------|
| ara       | Classical Arabic | Literature |  Use the CTS Namespace "greekLit". Refer to the [Perseus' Catalog](http://catalog.perseus.org) to find the work urn. Do not mind contacting them |
| fro       | Medieval French | Literature | Use the CTS namespace "froLit". Use the Jonas database permalinks number to chose your textgroup and work identifiers : http://jonas.irht.cnrs.fr/ , *eg* the [Vie de Saint Martin](http://jonas.irht.cnrs.fr/oeuvre/1856) of [Wauchier de Denain](http://jonas.irht.cnrs.fr/intervenant/915) should be `urn:cts:jns915.jns1856` |
| grc       | Ancient Greek    | Classical Literature   | Use the CTS Namespace "greekLit". Refer to the [Perseus' Catalog](http://catalog.perseus.org) to find the work urn. Do not mind contacting them |
| grc       | Ancient Greek    | Inscriptions | Need documentation. |
| grc       | Ancient Greek    | Papyrii | Need documentation. |
| lat       | Latin    | Classical Literature   | Use the CTS Namespace "latinLit". Refer to the [Perseus' Catalog](http://catalog.perseus.org) to find the work urn. Do not mind contacting them |
| lat       | Latin    | Inscriptions | Need documentation. |
| lat       | Latin    | Papyrii | Need documentation. |

Finally, for the last part of the urn (the edition or translation identifier), we recommend to use the name of your project or lab, followed by a dash, an iso 639-2 code and a number that you could increment should you provide other editions, *eg* ciham-fro1, perseus-eng1, opp-lat1, etc.

In general, a CTS URN should be lowercase only and be as short as possible. If it uses external identifier, the identifier provider (tlg, stoa, jns) should be part of the scheme. Feel free to contact us by github or [by mail](mailto:capitains[at]googlegroups.com) if you need help or want to propose a provided

## Directory structure

## Metadata Files

## TEI XML

## Related tools

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