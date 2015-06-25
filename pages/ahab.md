---
layout: page
title: "Ahab"
group: navigation
description: "Description of the Ahab Service Norm"
---
{% include JB/setup %}

* TOC
{:toc}

## Introduction

Ahab has implementations for [eXistDB restxq](http://github.com/Capitains/Ahab-eXistDB) and a [cache layer written for Flask](http://github.com/Capitains/Ahab) (Python web app). Ahab provides new functionnalities to CTS repositories, using CTS as its basic informations.

Addition to Ahab are welcome, either as implementations or as requests ! Ahab is a norm, not a software !

## Implementations

- [Ahab-ExistDB](http://github.com/Capitains/Ahab-eXistDB) : Implementation of the Ahab API for eXistDB restxq services

Others :

- [Ahab for Flask](http://github.com/Capitains/Ahab) : Ahab for Flask is mostly a cache layer that you can add on top of your implementations. Ahab for eXistDB being quite slow for big requests, the addition of a strong cache layer between the API and the user allowed for better performances.

## Requests

Ahab supports two different URL naming convention, and both should be supported by implementations : a RESTful one and a "GET" one.

- "GET" request should accept a `request` url parameter to specify the request to do. All other request parameters would be added normally. *e.g.* `http://localhost/ahab?request=Search&query=lasciv*&urn=urn:cts:latinLit:phi1294`
- REST request should be written as : `/ahab/rest/v1.0/*requestname*/`. Further details are given for each request when applicable.

### Search
**Purpose**: Search proposes to do fulltext search on a specific area of a CTS API.

{:.table}
| Parameter | Type | Required/optional | Description |  
|  ------   | ---- | ----------------- | ----------- | 
| urn       | str  | Required          | A full or partial urn (from Domain to edition node). *e.g.* : `urn:cts:latinLit` will query the full Latin literature domain while `urn:cts:latinLit:phi1294` will only query Martial's texts |
| query     | str  | Required          | The text to search for. Depending on implementation, could use jokers (See [eXistDB documentation](http://exist-db.org/exist/apps/doc/lucene.xml#D2.2.5.10)) |
| start     | int  | Optional          | Starting result index |
| limit     | int  | Optional          | Limit of results to be shown |

#### XML Reply schema

Example query : `ahab?request=Search&query=ἀλλήλους&urn=urn:cts:greekLit`

{% highlight xml %}
<ahab:Search xmlns:ahab="http://github.com/Capitains/ahab">
    <!-- @elapsed-time is not required -->
    <ahab:request elapsed-time="2967">
        <!-- This is kind of a free section -->
        <ahab:requestName>Search</ahab:requestName>
        <ahab:requestUrn>urn:cts:greekLit</ahab:requestUrn>
        <ahab:query>ἀλλήλους</ahab:query>
        <ahab:option />
    </ahab:request>
    <ahab:reply>
        <!-- Parameters informations -->
        <ahab:query>ἀλλήλους</ahab:query>
        <ahab:urn>urn:cts:greekLit</ahab:urn>
        <ahab:results ahab:offset="1" ahab:limit="5" ahab:count="67">
            <ahab:result>
                <ahab:urn>urn:cts:greekLit:tlg0003.tlg001.perseus-grc2</ahab:urn>
                <ahab:passageUrn>urn:cts:greekLit:tlg0003.tlg001.perseus-grc2:1.1.1</ahab:passageUrn>
                <ahab:text>
                    <p>
                        <span class="previous"> Θουκυδίδης Ἀθηναῖος ξυνέγραψε τὸν πόλεμον τῶν
              Πελοποννησίων καὶ Ἀθηναίων, ὡς ἐπολέμησαν πρὸς  </span>
                        <span class="hi">ἀλλήλους</span>
                        <span class="following">, ἀρξάμενος εὐθὺς καθισταμένου
              καὶ ἐλπίσας μέγαν τε ἔσεσθαι καὶ ἀξιολογώτατον τῶν προγεγενημένων, τεκμαιρόμενος ὅτι
              ἀκμάζοντές τε ᾖσαν ἐς αὐτὸν ἀμφότεροι παρασκευῇ τῇ πάσῃ καὶ τὸ ἄλλο Ἑλληνικὸν ὁρῶν
              ξυνιστάμενον πρὸς ἑκατέρους, τὸ μὲν εὐθύς, τὸ δὲ κ ...</span>
                    </p>
                </ahab:text>
            </ahab:result>
        </ahab:results>
    </ahab:reply>
</ahab:Search>
{% endhighlight %}

#### JSON Reply schema

{% highlight json %}
{
  "reply": {
    "count": "2",
    "limit": 10,
    "offset": 1,
    "results": [
      {
        "passage": "urn:cts:latinLit:phi1294.phi002.perseus-lat2:3.20.6",
        "text": {
          "after": "elegis an severus herois?",
          "hi": "Lascivus",
          "previous": ""
        },
        "urn": "urn:cts:latinLit:phi1294.phi002.perseus-lat2"
      },
      {
        "passage": "urn:cts:latinLit:phi0959.phi007.perseus-lat2:4.701",
        "text": {
          "after": "in aevo ",
          "hi": "lascivus",
          "previous": " filius huius erat primo"
        },
        "urn": "urn:cts:latinLit:phi0959.phi007.perseus-lat2"
      }
    ]
  },
  "request": {
    "query": "lascivus",
    "urn": "urn:cts:latinLit"
  }
}
{% endhighlight %}
### Permalink
**Purpose**: Permalink is a tool to help retrieve a urn on a CTS api. CTS API are based on the prerequisite to know the right inventory. If the API has more than one inventory, having this tool can help external users to find a text without knowing their inventory.

**RESTful implementation** : In REST implementation, the query parameter "urn" shoud be put as follow : `ahab/rest/v1.0/permalink/urn:cts...`

{:.table}
| Parameter | Type | Required/optional | Description |  
|  ------   | ---- | ----------------- | ----------- | 
| urn       | str  | Required          | A work, edition or translation urn |

#### XML Reply schema

For the request `/ahab?request=Permalink&urn=urn:cts:greekLit:tlg0003.tlg001`

{% highlight xml %}
<ahab:Permalink xmlns:ahab="http://github.com/Capitains/ahab">
    <ahab:request elapsed-time="180">
        <!-- This is kind of a free section -->
        <ahab:requestName>Permalink</ahab:requestName>
        <ahab:requestUrn>urn:cts:greekLit:tlg0003.tlg001.perseus-grc1</ahab:requestUrn>
        <ahab:query/>
        <ahab:option/>
    </ahab:request>
    <ahab:reply>
        <!-- The full urn of the edition or translation -->
        <ahab:urn>urn:cts:greekLit:tlg0003.tlg001.perseus-grc1</ahab:urn>
        <!-- A proposed query -->
        <ahab:request>GetValidReff</ahab:request>
        <!-- The name of the inventory -->
        <ahab:inventory>grc</ahab:inventory>
    </ahab:reply>
</ahab:Permalink>
{% endhighlight %}