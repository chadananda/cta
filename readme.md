# CTA API
### Computer Translator's Aid - Experimental API

In the 80's of the last century, an intrepid team of hungry volunteers crafted a reference engine called CTA. This project exposes some of the valuable CTA data as a Restful web service so that developers can experiment with other uses of the CTA data.

The CTA data links every word or phrase translated by Shoghi Effendi from Arabic and Farsi into English. The purpose was to help translators to create English renderings more consistent with those of Shoghi Effendi.

### Included in this Repository

This repository includes two NPM modules:

  * *cta*: a REST client with promise-wrapped http calls and local caching
  * *cta-server*: a FeathersJS-based REST server with fast LokiJS in-memory database

### To Setup CTA API Server

```
 npm install cta_server
 npm run server
 >>> CTA API server running at http://localhost:1844
```


### To Use CTA Client

To use client, simply install:

```npm install cta_client```

To initialize, create object pointing to running server instance:

```
 import cta_client from 'cta_client'
 CONST cta = new cta_client('http://localhost:1844')
```

Look up source terms, translation terms or generate provisional translation

```
cta.sources('justice', lang='en', authors='').then(res => console.log(res.data))
   // {
   //   term: 'justice', lang: 'en',
   //   source:[ {w:'عدالة',    lang:'ar', num:55},
   //            {w:'عدل',      lang:'ar', num:40},
   //            {w:'إنصاف',    lang:'ar', num:27},
   //            {w:'استقامة',  lang:'ar', num:5 },
   //            {w:'دادگستری', lang:'fa', num:17},
   //            {w:'داد',      lang:'ar', num:3 } ]
   // }
```

```
cta.translations('عدالة', lang='ar', authors='').then(res => console.log(res.data))
   // {
   //   term: 'عدالة', lang: 'ar',
   //   source:[ {w:'إنصاف',  lang:'ar', num:55},
   //            {w:'إنصاف',  lang:'ar', num:40} ]
   // }
```

```
cta.provisional('يَا مَلأَ البَيَانِ هَلْ نَسِيْتُمْ وَصَايَايَ', 'en').then(res => console.log(res.data))
   // {
   //   source: 'يَا مَلأَ البَيَانِ هَلْ نَسِيْتُمْ وَصَايَايَ',
   //   translation: 'O people of the Bayan! Have ye forgotten My exhortations?'
   // }
```

### Some other possible commands:

* translation_report // generate full report of translations based on all stems and roots
* altwords // pivot list of terms also translated from the same word
* ??? ideas?

#### Licence

This is free and unencumbered software released into the public domain. [http://unlicense.org](http://unlicense.org)

