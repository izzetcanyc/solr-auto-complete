# solr-auto-complete
Type AHead Solr Auto Complete Tool

Aim of this project to create auto-suggest feature for search application which enumerates all possiblities and maps them to find best choices. Final result will satisfy very demanding situations. 

STEPS:


1. Installations, Working with Core and Using Query:white_check_mark:
2. Adding Req. Components:white_check_mark:
3. Loopup Implementation:white_check_mark:
4. Working With Multiple Dictionaries:white_check_mark:
5. Context Filtering:white_check_mark:
6. Testing Results:white_check_mark:

Tools and Requirements:


* Apache Solr
* Java JDK
* Localhost

Creatıng core
`>> bin/solr create -c <core-name-here>`


* This will create a core which will be a workspace for us. Core includes documents.

Modıfying schema:

```curl -X POST -H 'Content-type:application/json' --data-binary '{
"add-field":{
"name":"cat",
"type":"text_general",
"indexed":"true",
"stored":true }
}' http://localhost:8983/solr/myCore/schema```

We need to add fields to schema.xml (managed-schema.xml)

Indexıng data:
```bin/post -c myCore filelocation(json,xml,csv)```

One more Step For Ngram Add this codes to managed-schema.xml
```
<field name="title_ngram" type="text_ngram" indexed="true" stored="true"/>
  <copyField source="Title" dest="title_ngram"/>

  <fieldType name="text_ngram" class="solr.TextField" positionIncrementGap="100">
	<analyzer type="index">
	<tokenizer class="solr.NGramTokenizerFactory" minGramSize="2" maxGramSize="10"/>
	<filter class="solr.LowerCaseFilterFactory"/>
	</analyzer>
		<analyzer type="query">
		<tokenizer class="solr.EdgeNGramTokenizerFactory" minGramSize="2" maxGramSize="10"/>
		<filter class="solr.LowerCaseFilterFactory"/>
	</analyzer>
  </fieldType>
  ```

##Run

`>> bin/solr start`
Then Run The Maven Project



## Usage Areas

* Autocomplete tool for everywebsite which has search option
