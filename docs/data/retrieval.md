Before you use the following snippets, please make sure, that you read the [terms of use](../../about/licenses) of our data.


## Retrieving all resources from a group

This snippet is useful to retrieve all resources belonging to one of four groups of the ckan instance: 

* `data`
* `service`
* `app`
* `guideline`

```javascript
//var uri = "YOUR CKAN URI"
var uri = "http://giv-oct.uni-muenster.de:5000";
//var id = "YOUR GROUP ID"
var id = "apps";

$.ajax({
  url: uri+"/api/3/action/package_search?q=groups:"+id+"&rows=3000",
  dataType:"json",
  async:true,
  success: function(json){
    console.log(json);
    //PARSE JSON    
  }
});
```

## Retrieving a specific resource

This snippet is useful to retrieve a specific resource from our ckan instance.

```javascript
//var uri = "YOUR CKAN URI"
var uri = "http://giv-oct.uni-muenster.de:5000";
//var id = "YOUR RESOURCE ID"
var id = "abc-ancientwoods";

$.ajax({
  url: uri+"/api/3/action/package_show?id="+id,
  dataType:"json",
  async:true,
  success: function(json){
    console.log(json);
    //PARSE JSON    
  }
});
```
