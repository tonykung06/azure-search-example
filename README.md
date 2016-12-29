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
- `curl -X POST -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: d33a759c-7230-b5ea-44a6-5933a84d1179" -d '{"value":[{"@search.action":"upload","id":"1","name":"FrozenBrews","slogen":"Redefiningcrispandcold","description":"LocatedattheSouthPole,thisistheonlybrewerySantaClausthinksofvisitingaftersniffingreindeerrearwhiletruckin'"'"'aoundtheglobe.","breweryType":"micro","location":{"type":"Point","coordinates":[90.000000,0.000000]}}]}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/breweries/docs/index?api-version=2015-02-28"`

### Delete documents from an index
`curl -X POST -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 99b20304-b1df-0102-feb9-cfed5a525d26" -d '{"value":[{"@search.action":"delete","id":"1"}]}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/breweries/docs/index?api-version=2015-02-28"`

### Mergin documents of an index
`curl -X POST -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 28eb5377-1416-211d-ab2b-23ff619aa59a" -d '{"value":[{"@search.action":"merge","id":"1","name":"mergedname"}]}' "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/breweries/docs/index?api-version=2015-02-28"`

### Retrieving a specific document from an index
`curl -X GET -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: ec5a8218-df2c-c502-a566-20d8b4223ab3" "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/1?select=*&api-version=2015-02-28"`

### Retrieving some fields of a specific document from an index
`curl -X GET -H "api-key: <API Key>" -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: ec5a8218-df2c-c502-a566-20d8b4223ab3" "https://tonykung-asdemo-hk-dev.search.windows.net/indexes/beers/docs/1?select=name,breweryName&api-version=2015-02-28"`