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


The following guidelines ensure that your work will be fully compliant with all resources available in the Capitains Tool suite. If you are not too familiar with CTS, please see the [Vocabulary](/pages/vocabulary.html). You can find a documented example repository at [https://github.com/Capitains/documented-repo](https://github.com/Capitains/documented-repo).

## Foreword

CapiTainS guidelines are the results of years of struggle with Perseus data maintenance. When someone would try to update a typo, it could take  days to update the servers to serve the correct data. In 2013, Perseus made the decision to implement CTS (Canonical Text Services) as a big step towards Linked Open Data. The idea behind the CTS API implementation would ideally be to  build a new Perseus on microservices. This would in turn  resolve the maintainability issues  as well as serve data in a decentralized fashion to external data users.

All implementations of CTS  were focused principally on technologies that had some limitations with regard to  scalability,  maintainability, or both. CapiTainS, as a CTS standards compliant development effort, does not require the use of its own API implementation when it comes to its other tools:CapiTainS components are interoperable with other CTS-compliant software. CapiTainS guidelines were built to explicitly state CTS related information in files so that it could be reused in different situations, by different software, with clear metadata information provided.

CTS requires two main component types, texts and metadata (or inventory information). They provide data consumers with all required information to serve the texts via a CTS API, from edition information to textual node, including citation scheme information. CapiTainS splits this information so that the Citation Scheme is an inherent part of the text, using traditional TEI capacities, while all other metadata can be found in separate files. The reasoning behind this split was to allow for separate maintenance of general metadata - used to browse a catalog of texts - and text metadata such as the citation scheme. Finally, the directory structure of CapiTainS allows a much simpler browsing method for finding, adding, updating resources in a repository: by separating resources by URN levels, it brings ease of maintenance

## Participants 

Thibault Clérice and Bridget Almas are the original developers of these guidelines. A special mention to Michael Gursky who first put the idea out there of this directory structure as well as the metadata splitting.

## CTS URN Choice

URN choice is quite often one of the first questions people ask when trying to decided wether or not CTS is good for them, and it often feels to us that it prevents people from actually adopting the standard. Here is a list of languages with recommendations for your language choice.  


{: .table .table-striped .table-hover}
| ISO 639-2   | Language         | Type of text         | Recommendation                                                                                                                                                                                                                                                                                                                   |  
| ----------- | ----------       | --------------       | ----------------                                                                                                                                                                                                                                                                                                                 |  
| ara         | Classical Arabic | Literature           | Use the CTS Namespace "arabicLit". Refer to the [Perseus' Catalog](http://catalog.perseus.org) to find the work urn. Questions can be addressed to catalog "at" perseus.tufts.edu.                                                                                                                                                                                   |  
| fro         | Medieval French  | Literature           | Use the CTS namespace "froLit". Use the Jonas database permalinks number to chose your textgroup and work identifiers : http://jonas.irht.cnrs.fr/ , *eg* the [Vie de Saint Martin](http://jonas.irht.cnrs.fr/oeuvre/1856) of [Wauchier de Denain](http://jonas.irht.cnrs.fr/intervenant/915) should be `urn:cts:jns915.jns1856` |  
| grc         | Ancient Greek    | Classical Literature | Use the CTS Namespace "greekLit". Refer to the [Perseus' Catalog](http://catalog.perseus.org) to find the work urn. Questions can be addressed to catalog "at" perseus.tufts.edu.                                                                                                                                                                                  |  
| grc         | Ancient Greek    | Inscriptions         | Need documentation.                                                                                                                                                                                                                                                                                                              |  
| grc         | Ancient Greek    | Papyrii              | Need documentation.                                                                                                                                                                                                                                                                                                              |  
| lat         | Latin            | Classical Literature | Use the CTS Namespace "latinLit". Refer to the [Perseus' Catalog](http://catalog.perseus.org) to find the work urn. Questions can be addressed to catalog "at" perseus.tufts.edu.                                                                                                                                                                                  |  
| lat         | Latin            | Inscriptions         | Need documentation.                                                                                                                                                                                                                                                                                                              |  
| lat         | Latin            | Papyrii              | Need documentation.                                                                                                                                                                                                                                                                                                              |  


Finally, for the last part of the urn (the edition, translation, or commentary identifier), we recommend using the name of your project or lab, followed by a dash, an iso 639-2 code and a number that you could increment should you provide other editions, *eg* ciham-fro1, perseus-eng1, opp-lat1, etc.

In general, a CTS URN should be lowercase only and be as short as possible. If it uses external identifier, the identifier provider (tlg, stoa, jns) should be part of the scheme. Feel free to contact us by github or [by mail](mailto:capitains[at]googlegroups.com) if you need help or want to propose a provider. 

## Directory structure

1. A text repository should be built with a main data folder.
2. The data folder should contain directories which are named after textgroup's urn component. *For example, urn:cts:latinLit:phi1294.phi002.perseus-lat2 would have a directory phi1294.*
3. The textgroup directory contains a `__cts__.xml` file ([see below](#Texgroup_Metadata_Files)) containing metadata about the textgroup
4. The textgroup directory contains directories which are named after work's urn component. *For example, urn:cts:latinLit:phi1294.phi002.perseus-lat2 would have a directory phi002.*
5. The work directory contains the edition, translation, and commentary files.
6. The work directory contains a `__cts__.xml` file ([see below](#Work_Metadata_Files)) containing metadata about the work, editions and translations.
7. Edition, translation, and commentary files are named after their urn using every component except the namespace. *For example, urn:cts:latinLit:phi1294.phi002.perseus-lat2 would be phi1294.phi002.perseus-lat2.*

```
data/
  |- textgroup
    |- __cts__.xml
    |- work
      |- __cts__.xml
      |- full-urn.xml
```

**Example**

```
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
      |- tlg0012.tlg001.perseus-eng3.xml
```

## Metadata Files

Instead of relying on edition and translation TEI files or building a general inventories, splitting resources into individual files allows for balanced responsibility between a cataloging approach and a text reading one. CapiTainS guidelines are non-restrictive : as long as the minimal information is available, you can add nodes coming from other namespaces.

### Nodes specific to CapiTainS

#### Commentary

The ti:commentary node is meant to provide information about "texts" that are not considered editions or translations but, instead, are modern texts that comment on other texts. This could include the front or back matter of an edition or translation, e.g., the introduction, glossary, appendix, etc. It could also include modern volumes that were written specifically as commentaries on a text, e.g., a commentary on the Aeneid or the Gospel of Matthew. These "texts" contain important information about authors, works, editions, translations, or even other commentaries that we wanted to be able to relate to those textual objects.

#### About

At the present time, the ti:about node exists only as a child of the ti:commentary node. It should be an empty node with a single attribute, the `urn` of the textgroup, work, edition, translation, or commentary upon which it comments.

### Textgroup Metadata File

```xml
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
```

### Work Metadata File

```xml
<!--
  The work node has three attributes :
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
      Title node needs xml:lang declaration, it reflects the language of the title.
    -->
    <ti:title xml:lang="eng">Epigrammata</ti:title>
    <!-- 
      For each "text", either edition, translation, or commentary, there should be a ti:edition, ti:translation, or ti:commentary node

      The edition nodes has two attributes :
        - The first one, workUrn, contains only the urn up to the work component
        - The second, urn, contains the full urn
    -->
    <ti:edition 
      workUrn="urn:cts:latinLit:phi1294.phi002" 
      urn="urn:cts:latinLit:phi1294.phi002.perseus-lat2"
    >
        <!--
          Edition, Translation, and Commentary must have at least one label node.
          Label represents the title of the edition.
          Label node needs xml:lang declaration, it reflects the language of the title.
        -->
        <ti:label xml:lang="mul">Martial's Epigrammata</ti:label>
        <!--
          Edition, Translation, and Commentary must have at least one description node.
          Description node needs xml:lang declaration, it reflects the language of the description.
          
        -->
        <ti:description xml:lang="lat">
            M. Valerii Martialis Epigrammaton libri / recognovit W. Heraeus
        </ti:description>
    </ti:edition>
    <!--
      The translation node has three attributes :
        - The first one, workUrn, contains only the urn up to the work component
        - The second, urn, contains the full urn
        - The third, xml:lang, contains the language of the translation
    -->
    <ti:translation workUrn="urn:cts:latinLit:phi1294.phi002" urn="urn:cts:latinLit:phi1294.phi002.perseus-eng2" xml:lang="eng">
        <ti:label xml:lang="lat">Epigrammata</ti:label>
        <ti:description xml:lang="eng">Nice translations informations</ti:description>
    </ti:translation>
    <!--
      The commentary node has three attributes :
        - The first one, workUrn, contains only the urn up to the work component
        - The second, urn, contains the full urn
        - The third, xml:lang, contains the language of the commentary
    -->
    <ti:commentary workUrn="urn:cts:latinLit:phi1294.phi002" urn="urn:cts:latinLit:phi1294.phi002.perseus-eng3" xml:lang="eng">
        <ti:label xml:lang="mul">Introduction to the English translation of Epigrammata</ti:label>
        <ti:description xml:lang="eng">Nice commentary informations</ti:description>
        <!--
          The commentary has one extra node not found in edition or translation: the ti:about node. 
          This node has one attribute :
          - urn, which contains the URN of the textgroup, work, edition, translation, or commentary that this commentary is about
        -->
        <ti:about urn="urn:cts:latinLit:phi1294.phi002.perseus-eng2"/>
    </ti:commentary>
</ti:work>

```

## TEI XML

### URN Information

There are three recommendations :

1. If the text is epidoc, the convention is to supply the URN in the following xpath : `TEI/text/body/div[@type="edition" or @type="translation" or @type="commentary"]/@n` 
2. If the text is normal TEI, the convention is to supply the URN the following xpath : `TEI/text/body/@n`
3. For normal TEI, it is also possible to supply the URN as the value of an [@xml:base](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-att.global.html) attribute in the following xpath: 
`TEI/text/@xml:base`

The same node should have an `xml:lang` attribute stating the language of the text.

### Citation information

The citation scheme is reflected in a refsDecl node, in the teiHeader's encodingDesc of the edition or the translation. In this refsDecl, we use [cRefPattern](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-cRefPattern.html) nodes to define citations levels and their xpaths. It explicitly holds the passage informations. For cross-language compatibility, it is recommended to use only XPath 1, which is the latest one implemented in the lxml library used by C, PhP and Python.

- refsDecl should be in /TEI/teiHeader/encodingDesc.
- refsDecl should have its @n property set on "CTS"
- refsDecl contains as many cRefPattern as there are levels
- cRefPattern elements are ordered from deeper node to highest node
- the matchPattern should give an information about the number of level. Traditionally, we use (\w+) regexp to match identifiers
- the replacementPattern should contain $[1-9] which represents depth of a level, ie. this book passage 1.pr.8 should match the following xpath : /tei:TEI/tei:text/tei:body/tei:div/tei:div[@n='1']/tei:div[@n='pr']/tei:div[@n='9']
- There is no tag restriction in this xpath. You can use tei:w, tei:seg, tei:p, etc.
- the @n attributes represents the name of the level, usually book, poem, line, section, chapter, paragraph, argument, etc. 
- the @n attribute should always be lowercase.
- cRefPattern can include paragraphs which translate matchPattern and level hierarchy into human readable information

```xml
<refsDecl n="CTS">
  <cRefPattern 
      n="level3"
      matchPattern="(\w+).(\w+).(\w+)"
      replacementPattern="#xpath(/tei:TEI/tei:text/tei:body/tei:div/tei:div[@n='$1']/tei:div[@n='$2']/tei:div[@n='$3'])">
      <p>This pointer pattern extracts level1 and level2 and level3</p>
  </cRefPattern>
  <cRefPattern 
      n="level2"
      matchPattern="(\w+).(\w+)"
      replacementPattern="#xpath(/tei:TEI/tei:text/tei:body/tei:div/tei:div[@n='$1']/tei:div[@n='$2'])">
      <p>This pointer pattern extracts level1 and level2</p>
  </cRefPattern>
  <cRefPattern 
      n="level1"
      matchPattern="(\w+)"
      replacementPattern="#xpath(/tei:TEI/tei:text/tei:body/tei:div/tei:div[@n='$1'])">
      <p>This pointer pattern extracts level1</p>
  </cRefPattern>
</refsDecl>
```

## Related tools

- CookieCutter template to kickstart your repository [Link](https://github.com/Capitains/cookiecutter-guidelines), [Tutorial with docker](https://www.youtube.com/watch?v=pke1nPjhpuI)
- [Testing CapiTainS Resources locally with Hook](https://www.youtube.com/watch?v=0J3RvVyMf_k)
