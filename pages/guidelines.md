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


The following guidelines ensure that your work will be fully compliant with all resources available in Capitains Tool suite. If you are not too familiar with CTS, please see the [Vocabulary](/pages/vocabulary.html). You can find a documented example repository at [https://github.com/Capitains/documented-repo](https://github.com/Capitains/documented-repo).

## Forewords

CapiTainS guidelines are the results of years of strugle with Perseus data maintenance. When one maintainer would try to update a typo, it could takes hours and days to update the servers to serve the correct data. In 2013, Perseus took the decision to implement CTS (Canonical Text Services) as a big step towards Linked Open Data. The idea behind the CTS API implementation would be to ideally build a new Perseus on microservices to resolve the maintainability issues it had as well as serve data in a decentralized fashion to external data users.

All implementation of CTS up to CapiTainS' ones were focused principally on technologies that would not implement, in a rather balanced way, scalability and maintanability. While CapiTainS itself does not enforce the use of its own APIs software, the CapiTainS guidelines were built to explicitly state CTS related informations in text files so that it could be reused in different situation, by different softwares with clear metadata information provided.

CTS requires two main component's types, texts and metadata (or inventory information). They provides data consumers with all required informations, from edition informations to textual node, including citation scheme informations. CapiTainS splitted these informations so that the Citation Scheme is an inherent part of the text, using traditional TEI capacities, while all other metadata can be found in separated files. The reasoning behind this split was to allow for separate maintenance of general metadata - used to browse a catalog of texts - and texts metadata such as the citation scheme. Finally, the directory structure of CapiTainS allows a much simpler browsing method for finding, adding, updating resources in a repository:  by separating resources by URN levels, it brings ease of maintenance. 

## Participants 

Bridget Almas and Thibault Clérice are the original developers of these guidelines. A special mention to Michael Gursky who first put the idea out there of this directory structure as well as the metadata splitting.

## CTS URN Choice

URN choice is quite often one of the first question people ask when trying to decided wether or not CTS is good for them, and it often feels to us that it prevents people to actually adopt the standard. Here is a list of language with recommandations for your language choice. If you want to provide 


| ISO 639-2   | Language         | Type of text         | Recommandation                                                                                                                                                                                                                                                                                                                   |  
| ----------- | ----------       | --------------       | ----------------                                                                                                                                                                                                                                                                                                                 |  
| ara         | Classical Arabic | Literature           | Use the CTS Namespace "greekLit". Refer to the [Perseus' Catalog](http://catalog.perseus.org) to find the work urn. Do not mind contacting them                                                                                                                                                                                  |  
| fro         | Medieval French  | Literature           | Use the CTS namespace "froLit". Use the Jonas database permalinks number to chose your textgroup and work identifiers : http://jonas.irht.cnrs.fr/ , *eg* the [Vie de Saint Martin](http://jonas.irht.cnrs.fr/oeuvre/1856) of [Wauchier de Denain](http://jonas.irht.cnrs.fr/intervenant/915) should be `urn:cts:jns915.jns1856` |  
| grc         | Ancient Greek    | Classical Literature | Use the CTS Namespace "greekLit". Refer to the [Perseus' Catalog](http://catalog.perseus.org) to find the work urn. Do not mind contacting them                                                                                                                                                                                  |  
| grc         | Ancient Greek    | Inscriptions         | Need documentation.                                                                                                                                                                                                                                                                                                              |  
| grc         | Ancient Greek    | Papyrii              | Need documentation.                                                                                                                                                                                                                                                                                                              |  
| lat         | Latin            | Classical Literature | Use the CTS Namespace "latinLit". Refer to the [Perseus' Catalog](http://catalog.perseus.org) to find the work urn. Do not mind contacting them                                                                                                                                                                                  |  
| lat         | Latin            | Inscriptions         | Need documentation.                                                                                                                                                                                                                                                                                                              |  
| lat         | Latin            | Papyrii              | Need documentation.                                                                                                                                                                                                                                                                                                              |  


Finally, for the last part of the urn (the edition or translation identifier), we recommend to use the name of your project or lab, followed by a dash, an iso 639-2 code and a number that you could increment should you provide other editions, *eg* ciham-fro1, perseus-eng1, opp-lat1, etc.

In general, a CTS URN should be lowercase only and be as short as possible. If it uses external identifier, the identifier provider (tlg, stoa, jns) should be part of the scheme. Feel free to contact us by github or [by mail](mailto:capitains[at]googlegroups.com) if you need help or want to propose a provided

## Directory structure

1. A texts repository should be built with a main data folder.
2. The data folder should contain directories which are named after textgroup urn's component. *For example, urn:cts:latinLit:phi1294.phi002.perseus-lat2 would have a directory phi1294.*
3. The textgroup directory contains a `__cts__.xml` file ([see below](#Texgroup_Metadata_Files)) containing metadata about the textgroup
4. The textgroup directory contains directories which are named after work urn's component. *For example, urn:cts:latinLit:phi1294.phi002.perseus-lat2 would have a directory phi002.*
5. The work directory contains editions' and translations' files.
6. The work directory contains a `__cts__.xml` file ([see below](#Work_Metadata_Files)) containing metadata about the work, editions and translations.
7. Edition' and translation' files are named after their urn using every component except the namespace. *For example, urn:cts:latinLit:phi1294.phi002.perseus-lat2 would be phi1294.phi002.perseus-lat2.*

{% highlight %}
data/
  |- textgroup
    |- __cts__.xml
    |- work
      |- __cts__.xml
      |- full-urn.xml
{% endhighlight %}

**Example**

{% highlight %}
data/
  |- phi1294
    |- __cts__.xml
    |- phi001
      |- phi1294.phi001.perseus-lat2.xml
      |- __cts__.xml
    |- phi002
      |- phi1294.phi002.perseus-lat2.xml
      |- __cts__.xml
 |- tlg0012
    |- __cts__.xml
    |- tlg001
      |- __cts__.xml
      |- tlg0012.tlg001.perseus-grc1.xml
      |- tlg0012.tlg001.perseus-eng2.xml
{% endhighlight %}

## Metadata Files

Instead of relying on edition and translation TEI files or building a general inventories, splitting resources into individual file allows for balanced responsability between a cataloging approach and a text reading one. CapiTainS guidelines are non-restrictives : as you as the minimal information is available, you can add nodes coming from other namespaces.

### Textgroup Metadata File

{% highlight xml %}
<!-- 
  The urn of the textgroup node must contains only the urn up to the textgroup component
-->
<ti:textgroup xmlns:ti="http://chs.harvard.edu/xmlns/cts" urn="urn:cts:latinLit:phi1294">
    <!-- 
      Groupname is the name of the textgroup. 
      There needs to be at least one groupname node, with a clear lang declaration. 
      One groupname at least is required.
    -->
    <ti:groupname xml:lang="eng">Martial</ti:groupname>
    <ti:groupname xml:lang="lat">Marcus Valerius Martialis</ti:groupname>
</ti:textgroup>
{% endhighlight %}

### Work Metadata File

{% highlight xml %}
<!--
  The work nodes has three attributes :
    - The first one, groupUrn, contains only the urn up to the textgroup component
    - The second, urn, contains only the urn up to the work component
    - The third, xml:lang, reflects the language of the work, *ie* the language of the edition.
-->
<ti:work xmlns:ti="http://chs.harvard.edu/xmlns/cts"
  groupUrn="urn:cts:latinLit:phi1294"
  urn="urn:cts:latinLit:phi1294.phi002"
  xml:lang="lat"
>
    <!--
      Work must have at least one title node.
      Title node need xml:lang declaration, it reflects the language of the title.
    -->
    <ti:title xml:lang="eng">Epigrammata</ti:title>
    <!-- 
      For each "text", either edition or translation, there should be a ti:edition or ti:translation node

      The edition nodes has two attributes :
        - The first one, workUrn, contains only the urn up to the work component
        - The second, urn, contains the full urn
    -->
    <ti:edition 
      workUrn="urn:cts:latinLit:phi1294.phi002" 
      urn="urn:cts:latinLit:phi1294.phi002.perseus-lat2"
    >
        <!--
          Edition and Translation must have at least one title node.
          Title represents the title of the edition.
          Title node need xml:lang declaration, it reflects the language of the title.
        -->
        <ti:label xml:lang="eng">Martial's Epigrammata</ti:label>
        <!--
          Edition and Translation must have at least one description node.
          Description node need xml:lang declaration, it reflects the language of the description.
          
        -->
        <ti:description xml:lang="eng">
            M. Valerii Martialis Epigrammaton libri / recognovit W. Heraeus
        </ti:description>
    </ti:edition>
    <!--
      The edition nodes has two attributes :
        - The first one, workUrn, contains only the urn up to the work component
        - The second, urn, contains the full urn
    -->
    <ti:translation workUrn="urn:cts:latinLit:phi1294.phi002" urn="urn:cts:latinLit:phi1294.phi002.perseus-eng2">
        <ti:label xml:lang="eng">Epigrammata</ti:label>
        <ti:description xml:lang="eng">Nice translations informations</ti:description>
    </ti:translation>
</ti:work>
{% endhighlight %}

## TEI XML

### URN Informations

There is two different recommendations :

1. If the text is epidoc, the convention is to set it in the following xpath : `TEI/text/body/div[@type="edition" or @type="translation"]/@n` 
2. If the text is normal TEI, the convention is to set it in the following xpath : `TEI/text/body/@n`

The same node should have an `xml:lang` attribute stating the language of the text.

### Citation informations

The RefsDecl in the teiHeader of the TEI XML files must accurately represent the canonical citation scheme of the document. If we use the [cRefPattern](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-cRefPattern.html) syntax for this element to define the Xpaths and citation mapping patterns it should allow us to be able to automatically contruct the CTS citationMapping components of the CTS TextInventory for any given text.

Example from [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/SA.html#SACR](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/SA.html#SACR):

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

## Related tools