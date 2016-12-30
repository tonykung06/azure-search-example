## Commands

### Creating index
`curl -v -X POST -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: f510d008-1a60-178b-1bac-48b9bae1d476" -d '{"name": "beers","fields": [{"name": "id","type": "Edm.String","key": true}, {"name": "name","type": "Edm.String"}]}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes?api-version=2015-02-28" | python -m json.tool`

### Update an index, including CORS configs
`curl -v -X PUT -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: e448288d-de9a-34e5-0497-454b05234f47" -d '{"fields":[{"name":"id","type":"Edm.String","key":true},{"name":"name","type":"Edm.String"},{"name":"activelyBrewed","type":"Edm.Boolean"},{"name":"ibu","type":"Edm.Int32"},{"name":"abv","type":"Edm.Double"},{"name":"flavors","type":"Collection(Edm.String)"},{"name":"lastTappedOn","type":"Edm.DateTimeOffset"},{"name":"breweryId","type":"Edm.String"},{"name":"breweryName","type":"Edm.String"},{"name":"breweryLocation","type":"Edm.GeographyPoint"}],"corsOptions":{"allowedOrigins":["*"]}}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers?api-version=2015-02-28" | python -m json.tool`

### List all indexes
`curl -v -X GET -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: d5821ede-4c9e-b717-db07-3a534fc6c10b" "https://tonykung-asdemo-hk-dev.search.windows.net/indexes?api-version=2015-02-28" | python -m json.tool`

### List a specific index
`curl -v -X GET -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: d5821ede-4c9e-b717-db07-3a534fc6c10b" "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/breweries?api-version=2015-02-28" | python -m json.tool`

### Deleting an index from a search service
`curl -v -X DELETE -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: d5821ede-4c9e-b717-db07-3a534fc6c10b" "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers?api-version=2015-02-28" | python -m json.tool`

### Add documents to an index of a search service
- Note: `@search.action` could be `upload`, `delete`, `merge` or `mergeOrUpload`. `upload` means UPSERT, `merge` means partial update or partial removal of a field from a document by giving null value
- Note: This api could do a batch up to 1000 documents and each doc could have different actions
- `curl -X POST -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: d33a759c-7230-b5ea-44a6-5933a84d1179" -d '{"value":[{"@search.action":"upload","id":"1","name":"FrozenBrews","slogan":"Redefiningcrispandcold","description":"LocatedattheSouthPole,thisistheonlybrewerySantaClausthinksofvisitingaftersniffingreindeerrearwhiletruckin'"'"'aoundtheglobe.","breweryType":"micro","location":{"type":"Point","coordinates":[90.000000,0.000000]}}]}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/breweries/docs/index?api-version=2015-02-28"`

### Delete documents from an index
`curl -X POST -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 99b20304-b1df-0102-feb9-cfed5a525d26" -d '{"value":[{"@search.action":"delete","id":"1"}]}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/breweries/docs/index?api-version=2015-02-28"`

### Mergin documents of an index
`curl -X POST -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 28eb5377-1416-211d-ab2b-23ff619aa59a" -d '{"value":[{"@search.action":"merge","id":"1","name":"mergedname"}]}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/breweries/docs/index?api-version=2015-02-28"`

### Retrieving a specific document from an index
`curl -X GET -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: ec5a8218-df2c-c502-a566-20d8b4223ab3" "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/1?select=*&api-version=2015-02-28"`

### Retrieving some fields of a specific document from an index
`curl -X GET -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: ec5a8218-df2c-c502-a566-20d8b4223ab3" "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/1?select=name,breweryName&api-version=2015-02-28"`

### bulk insert docs
`curl -v -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: e448288d-de9a-34e5-0497-454b05234f47" -d '{"value":[{"@search.action":"upload","id":"1","name":"AhoolAle","activelyBrewed":true,"ibu":33,"abv":5.4,"flavors":["biscuity"],"lastTappedOn":"2016-01-23","breweryId":"b3TplPdS","breweryName":"NorthernHemisphereBrewco","breweryLocation":{"type":"Point","coordinates":[-86.055565,39.899728]}},{"@search.action":"upload","id":"2","name":"AgogweAle","activelyBrewed":true,"ibu":28,"abv":2.9,"flavors":["wheat","floral"],"lastTappedOn":"2016-05-18","breweryId":"Ek4mwsBoe","breweryName":"SouthernHemisphereBrewco","breweryLocation":{"type":"Point","coordinates":[-86.149979,39.923429]}},{"@search.action":"upload","id":"3","name":"AswangAle","activelyBrewed":true,"ibu":31,"abv":4.2,"flavors":["butter","yeast"],"lastTappedOn":"2016-02-13","breweryId":"b3TplPdS","breweryName":"NorthernHemisphereBrewco","breweryLocation":{"type":"Point","coordinates":[-86.055565,39.899728]}},{"@search.action":"upload","id":"4","name":"BurusBarleyWine","activelyBrewed":true,"ibu":76,"abv":11.1,"flavors":["raisin","dried","fruit","bourbon"],"lastTappedOn":"2016-01-01","breweryId":"b3TplPdS","breweryName":"NorthernHemisphereBrewco","breweryLocation":{"type":"Point","coordinates":[-86.055565,39.899728]}},{"@search.action":"upload","id":"7","name":"HyoteChocolateStout","activelyBrewed":true,"ibu":78,"abv":7.4,"flavors":["caramel","chocolate"],"lastTappedOn":"2016-01-07","breweryId":"zkXBTiBol","breweryName":"NorthAmericanBrewco","breweryLocation":{"type":"Point","coordinates":[-86.034279,39.835432]}},{"@search.action":"upload","id":"8","name":"IgopogoPilsner","activelyBrewed":true,"ibu":36,"abv":5.7,"flavors":["malt","bread"],"lastTappedOn":"2015-11-15","breweryId":"zkXBTiBol","breweryName":"NorthernHemisphereBrewco","breweryLocation":{"type":"Point","coordinates":[-86.034279,39.835432]}},{"@search.action":"upload","id":"9","name":"JackalobeLager","activelyBrewed":true,"ibu":29,"abv":3.3,"flavors":["fruit","citrus"],"lastTappedOn":"2016-03-15","breweryId":"zkXBTiBol","breweryName":"NorthernHemisphereBrewco","breweryLocation":{"type":"Point","coordinates":[-86.034279,39.835432]}},{"@search.action":"upload","id":"11","name":"MahambaBarleyWine","activelyBrewed":true,"ibu":57,"abv":9.7,"flavors":["malt","raisin"],"lastTappedOn":"2016-04-24","breweryId":"Ek4mwsBoe","breweryName":"SouthernHemisphereBrewco","breweryLocation":{"type":"Point","coordinates":[-86.149979,39.923429]}},{"@search.action":"upload","id":"12","name":"MegalodonPaleAle","activelyBrewed":true,"ibu":99,"abv":5.7,"flavors":["bread","hops","pine"],"lastTappedOn":"2016-03-31","breweryId":"VkNvPjBse","breweryName":"OceanicBrewco","breweryLocation":{"type":"Point","coordinates":[-86.157746,39.824688]}},{"@search.action":"upload","id":"16","name":"PopeLickPorter","activelyBrewed":true,"ibu":39,"abv":6.5,"flavors":["smokey","chocolate","banana"],"lastTappedOn":"2016-01-06","breweryId":"zkXBTiBol","breweryName":"NorthAmericanBrewco","breweryLocation":{"type":"Point","coordinates":[-86.034279,39.835432]}},{"@search.action":"upload","id":"17","name":"ChocolatePukwudgieStout","activelyBrewed":true,"ibu":35,"abv":12.2,"flavors":["chocolate","coffee"],"lastTappedOn":"2016-02-25","breweryId":"zkXBTiBol","breweryName":"NorthAmericanBrewco","breweryLocation":{"type":"Point","coordinates":[-86.034279,39.835432]}},{"@search.action":"upload","id":"18","name":"SharliePilsner","activelyBrewed":true,"ibu":31,"abv":4.1,"flavors":["grass"],"lastTappedOn":"2016-02-18","breweryId":"zkXBTiBol","breweryName":"NorthAmericanBrewco","breweryLocation":{"type":"Point","coordinates":[-86.034279,39.835432]}},{"@search.action":"upload","id":"19","name":"SigbinStout","activelyBrewed":false,"ibu":65,"abv":8.1,"flavors":["coffee","caramel"],"lastTappedOn":"2016-03-18","breweryId":"b3TplPdS","breweryName":"NorthernHemisphereBrewco","breweryLocation":{"type":"Point","coordinates":[-86.055565,39.899728]}},{"@search.action":"upload","id":"21","name":"SnallygasterPaleAle","activelyBrewed":false,"ibu":89,"abv":9.7,"flavors":["pine","honey"],"lastTappedOn":"2016-04-29","breweryId":"zkXBTiBol","breweryName":"NorthAmericanBrewco","breweryLocation":{"type":"Point","coordinates":[-86.034279,39.835432]}},{"@search.action":"upload","id":"22","name":"TikibalangBarleyWine","activelyBrewed":true,"ibu":45,"abv":9.6,"flavors":["bourbon"],"lastTappedOn":"2016-03-14","breweryId":"b3TplPdS","breweryName":"NorthernHemisphereBrewco","breweryLocation":{"type":"Point","coordinates":[-86.055565,39.899728]}},{"@search.action":"upload","id":"26","name":"PalePopobawaAle","activelyBrewed":true,"ibu":30,"abv":4.4,"flavors":["wheat"],"lastTappedOn":"2016-05-09","breweryId":"Ek4mwsBoe","breweryName":"SouthernHemisphereBrewco","breweryLocation":{"type":"Point","coordinates":[-86.149979,39.923429]}},{"@search.action":"upload","id":"27","name":"NorthAdjuleLager","activelyBrewed":true,"ibu":30,"abv":3.7,"flavors":["citrus"],"lastTappedOn":"2016-02-08","breweryId":"Ek4mwsBoe","breweryName":"SouthernHemisphereBrewco","breweryLocation":{"type":"Point","coordinates":[-86.149979,39.923429]}}]}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/index?api-version=2015-02-28" | python -m json.tool`

### Simple queries

#### Searching index with suffix(*) operator
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 71e87e26-c755-9894-0c59-b46fd463fc49" -d '{
	"search": "*",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: d53214b6-ac7e-3d8a-7bad-ffe7d07347eb" -d '{
	"search": "I*",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`
- This is not valid: `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: d8c00285-d27c-d0c0-e4ed-2fbca185e7aa" -d '{
	"search": "*L",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

#### OR(|) operator, by default azure search OR the terms together
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 9f3aa480-9281-2c02-3f6e-05016f0ac959" -d '{
	"search": "porter | stout",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"` is the same as `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 0a623099-cbc5-42dc-19cd-ad962eb195d5" -d '{
	"search": "porter stout",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

#### AND(+) operator
`curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: ce5ae558-00bd-9e54-7867-88da8f22a16f" -d '{
	"search": "pale + ale",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

#### Phase("") operator
`curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 54c7c50c-e8ac-22f4-64e3-05098410b40a" -d '{
	"search": "\"pale ale\"",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

#### Mixing operators in simple queries, the operators are excuted from right to left by default
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 0f9e0325-5607-0d0e-605e-432f5ba676d8" -d '{
	"search": "m* + p* | s*",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 827b9096-2acd-7032-d346-b6c4d2d83759" -d '{
	"search": "m* | p* + s*",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

#### Precedence(...) to control the order of operations and NOT operator to exclude terms from searches
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: b8587fef-7c23-0cde-b766-19a041f88980" -d '{
	"search": "-stout",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 248659b6-67b6-f91e-36c1-c353d2585292" -d '{
	"search": "-(porter|stout)",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: d8c1d3f7-e6fa-39dc-8426-d450e45d4641" -d '{
	"search": "-pale ale",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`, means without pale OR has ale because of the default "any" searchMode, we could change to ANDed the NOT operator by configuring searchMode to "all"
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: f20a7527-ee9d-90f9-0d44-66f9bceb6265" -d '{
	"search": "stout -chocolate",
	"searchMode": "all",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

### Full queries / Lucene queries

#### wildcard
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: a716b9da-1ff5-2ce9-9045-dcba8dbe7a36" -d '{
	"search": "P*e",
	"queryType": "full",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

#### AND
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 4678bb5d-1d88-2add-6685-cafea0c4ddbe" -d '{
	"search": "pale && ale",
	"queryType": "full",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

#### REQUIRED
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 6faf7f7a-e9e8-0edb-4291-ea3f883aad3f" -d '{
	"search": "+pale +ale",
	"queryType": "full",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`, to define required terms

#### NOT
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 8664f928-29a1-e7c0-0b24-74d1b8fe45f7" -d '{
	"search": "stout -chocolate",
	"queryType": "full",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`, return results that have stout AND without chocolate

#### field-level queries
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 62cc7ed3-c541-9694-c3f2-c3ea4aeed331" -d '{
	"search": "((name:(porter|stout)) AND (breweryName:\"North American Brewco\"))",
	"queryType": "full",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

#### Fuzzy searches
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: c1e55adf-96e4-3e9e-8ccd-32634208380f" -d '{
	"search": "Puckwudgie6~",
	"queryType": "full",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`, by default the distance(number of operations to transform one string to another string) is 1 and the maximum allowed is 2
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 5508df8e-afc1-c644-3cc0-98c814de078f" -d '{
	"search": "Puckwudgie~2",
	"queryType": "full",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

#### Proximity searches, the order of words doesn't matter, all about distance between words
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 58743498-181c-e846-a1f1-9df9fd9f8ed4" -d '{
	"search": "\"Chocolate Stout\"~1",
	"queryType": "full",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 58743498-181c-e846-a1f1-9df9fd9f8ed4" -d '{
	"search": "\"Chocolate Stout\"~0",
	"queryType": "full",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`, allowed distance: zero

#### Term Boosting, some terms are more important (increaded relevance) than the others, by default, every term has a boost factor of 1, the decimal boost value goes in range 0 < x < y.y
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 981e2d97-e075-df74-7b2c-e6ed9d326276" -d '{
	"search": "pale^2 ale",
	"queryType": "full",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 3375099f-6006-f840-8bc9-3bab9cd4bc6b" -d '{
	"search": "\"pale ale\"^2",
	"queryType": "full",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

#### Regular Expressions
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 0530c25f-7e5f-0845-0945-7873ef185046" -d '{
	"search": "name:/.*col.*/",
	"queryType": "full",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

### Query statistics

#### Total number of results, the count is an approximation as it is not updated in realtime
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 5d2579df-972f-b8d5-2195-cba5439acc1b" -d '{
	"search": "name:/.*col.*/",
	"queryType": "full",
	"select": "id, name",
	"count": true
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`

### Filtering, this is applied after matching docs are found
- `curl -X POST -H "api-key: 0E6B95048C237F5E8849DE99C6E9C904" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 07602fa9-dbbd-6ff1-a7d0-e17002991705" -d '{
	"search": "*",
	"filter": "ibu lt 30.0",
	"select": "id, name"
}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/search?api-version=2015-02-28"`