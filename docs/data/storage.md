## Storage

## Storage

### Package_create
##### Parameters
*	name (string) – the name of the new dataset, must be between 2 and 100 characters long and contain only lowercase alphanumeric characters, - and _, e.g. 'warandpeace'
*	title (string) – the title of the dataset (optional, default: same as name)
*	author (string) – the name of the dataset’s author (optional)
*	author_email (string) – the email address of the dataset’s author (optional)
*	maintainer (string) – the name of the dataset’s maintainer (optional)
*	maintainer_email (string) – the email address of the dataset’s maintainer (optional)
*	license_id (license id string) – the id of the dataset’s license, see license_list() for available values (optional)
*	notes (string) – a description of the dataset (optional)
*	url (string) – a URL for the dataset’s source (optional)
*	version (string, no longer than 100 characters) – (optional)
*	state (string) – the current state of the dataset, e.g. 'active' or 'deleted', only active datasets show up in search results and other lists of datasets, this parameter will be ignored if you are not authorized to change the state of the dataset (optional, default: 'active')
*	type (string) – the type of the dataset (optional), IDatasetForm plugins associate themselves with different dataset types and provide custom dataset handling behaviour for these types
*	resources (list of resource dictionaries) – the dataset’s resources, see resource_create() for the format of resource dictionaries (optional)
*	tags (list of tag dictionaries) – the dataset’s tags, see tag_create() for the format of tag dictionaries (optional)
*	extras (list of dataset extra dictionaries) – the dataset’s extras (optional), extras are arbitrary (key: value) metadata items that can be added to datasets, each extra dictionary should have keys 'key' (a string), 'value' (a string), and optionally 'deleted'
*	relationships_as_object (list of relationship dictionaries) – see package_relationship_create() for the format of relationship dictionaries (optional)
*	relationships_as_subject (list of relationship dictionaries) – see package_relationship_create() for the format of relationship dictionaries (optional)
*	groups (list of dictionaries) – the groups to which the dataset belongs (optional), each group dictionary should have one or more of the following keys which identify an existing group: 'id' (the id of the group, string), 'name' (the name of the group, string), 'title' (the title of the group, string), to see which groups exist call group_list()
*	owner_org (string) – the id of the dataset’s owning organization, see organization_list() or organization_list_for_user for available values (optional)

##### Javascript
```javascript
<script>
    var client = new CKAN.Client('http://giv-oct.uni-muenster.de:5000', '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39');
    client.action('package_create', {
                name:  'newtestsprova',
                owner_org: 'tests'
            },
            function(err) {
                if (err) console.log(err);
                console.log('All done');
            })
</script>
```

##### Python
```python
#!/usr/bin/env python2
import ckanapi

remote = 'http://giv-oct.uni-muenster.de:5000'
apikey = '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39'

ckan = ckanapi.RemoteCKAN(remote, apikey)

package = ckan.action.package_create(name='packagetest', owner_org='tests')
```
##### R
```r
library('ckanr')
ckanr_setup(url = "http://giv-oct.uni-muenster.de:5000", key = "5df62ec6-5fa7-4e2f-838a-a7d30c6aca39")
# create a package
(res <- package_create("newpackage", owner_org='tests'))
```

### Datastore_create
##### Parameters
*	resource_id (string) – resource id that the data is going to be stored against.
*	force (bool (optional, default: False)) – set to True to edit a read-only resource
*	resource (dictionary) – resource dictionary that is passed to resource_create(). Use instead of resource_id (optional)
*	aliases (list or comma separated string) – names for read only aliases of the resource. (optional)
*	fields (list of dictionaries) – fields/columns and their extra metadata. (optional)
*	records (list of dictionaries) – the data, eg: [{“dob”: “2005”, “some_stuff”: [“a”, “b”]}] (optional)
*	primary_key (list or comma separated string) – fields that represent a unique key (optional)
*	indexes (list or comma separated string) – indexes on table (optional)


##### Javascript
```javascript
<script>
    var client = new CKAN.Client('http://giv-oct.uni-muenster.de:5000', '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39');

    var nfields = [
        {'id': 'dataset_id', 'type': 'text'},
        {'id': 'indicator_id', 'type': 'text'},
        {'id': 'region', 'type': 'text'},
        {'id': 'period', 'type': 'int'},
        {'id': 'value', 'type': 'float'}
    ]

    var data = [
        {'indicator_id': ''Population',
            'dataset_id': 'acled',
            'region': 'ITA',
            'value': '5000000',
            'period': '2016'}
    ];

    var resource = {
        "package_id": "packagetest",
        "format": "CSV",
        "name": "NameExample2"
    }

    client.action('datastore_create', {
                resource:  resource,
                records: data,
                primary_key: 'dataset_id'
            },
            function(err) {
                if (err) console.log(err);
                console.log('All done');
            }
    )

</script>
```

##### Python
```python
#!/usr/bin/env python2
import ckanapi

remote = 'http://giv-oct.uni-muenster.de:5000'
apikey = '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39'

ckan = ckanapi.RemoteCKAN(remote, apikey)

package = ckan.action.package_show(id='packagetest')

resource = {"package_id": package['id'],"format": "CSV", "name": "NameExample"}

newfields = [
    {'id': 'dataset_id', 'type': 'text'},
    {'id': 'indicator_id', 'type': 'text'},
    {'id': 'region', 'type': 'text'},
    {'id': 'period', 'type': 'int'},
    {'id': 'value', 'type': 'float'}
]

newRecords = [
    {	'indicator_id': 'Population',
        'dataset_id': 'acled',
        'region': 'ITA',
        'value': '5000000',
        'period': '2016'}
]

ckan.action.datastore_create(resource=resource, fields=newfields, records=newRecords, primary_key='dataset_id')
```

### Datastore_upsert
##### Parameters
*	resource_id (string) – resource id that the data is going to be stored under.
*	force (bool (optional, default: False)) – set to True to edit a read-only resource
*	records (list of dictionaries) – the data, eg: [{“dob”: “2005”, “some_stuff”: [“a”,”b”]}] (optional)
*	method (string) – the method to use to put the data into the datastore. Possible options are: upsert, insert, update (optional, default: upsert)

##### Methods
*	upsert: Update if record with same key already exists, otherwise insert. Requires unique key.
*	insert: Insert only. This method is faster that upsert, but will fail if any inserted record matches an existing one. Does not require a unique key.
*	update: Update only. An exception will occur if the key that should be updated does not exist. Requires unique key.


##### Javascript
```javascript
<script>
    var client = new CKAN.Client('http://giv-oct.uni-muenster.de:5000', '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39');

    var data = [
        {'indicator_id': 'CHD.B.HUM.04.T6',
            'dataset_id': 'acled',
            'region': 'KEN',
            'value': '50000000',
            'period': '2016'}

    ];
    packageId = '450f2c55-425f-4797-8d70-33b5729d1f1d';

    client.action('datastore_upsert', {
                resource_id:  packageId,
                records: data,
                method: 'upsert',
                force: 'True'
            },
            function(err) {
                if (err) console.log(err);
                console.log('All done');
            })

</script>
```

##### Python
```python
import ckanapi

remote = 'http://giv-oct.uni-muenster.de:5000'
apikey = '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39'
resource_id = '450f2c55-425f-4797-8d70-33b5729d1f1d'

ckan = ckanapi.RemoteCKAN(remote, apikey)

newRecord = [
    {'indicator_id': 'CHD.B.HUM.04.T6',
     'dataset_id': 'acled',
     'region': 'KEN',
     'value': '50000000',
     'period': '2016'}
]

ckan.action.datastore_upsert(
            resource_id=resource_id,
            method='upsert',
            records=newRecord,
            force=True)
```


### Datastore_search
##### Parameters
*   resource_id (string) – id or alias of the resource to be searched against
*	filters (dictionary) – matching conditions to select, e.g {“key1”: “a”, “key2”: “b”} (optional)
*	q (string) – full text query (optional)
*	plain (bool) – treat as plain text query (optional, default: true)
*	language (string) – language of the full text query (optional, default: english)
*	limit (int) – maximum number of rows to return (optional, default: 100)
*	offset (int) – offset this number of rows (optional)
*	fields (list or comma separated string) – fields to return (optional, default: all fields in original order)
*	sort (string) – comma separated field names with ordering e.g.: “fieldname1, fieldname2 desc”



##### Javascript
```javascript
<script>
    var client = new CKAN.Client('http://giv-oct.uni-muenster.de:5000', '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39');
    var resourceId = '450f2c55-425f-4797-8d70-33b5729d1f1d';

    var nfilters = {"region": 'KEN'};

    var search = client.action('datastore_search', {
                resource_id:  resourceId,
                filters: nfilters
            },
            function(err) {
                if (err) console.log(err);
                console.log('All done');
            })
</script>
```

##### Python
```python
#!/usr/bin/env python2
import ckanapi

remote = 'http://giv-oct.uni-muenster.de:5000'
apikey = '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39'
resource_id = 'c123ba85-41f9-4a04-80f5-a26368ba9204'

ckan = ckanapi.RemoteCKAN(remote, apikey)

filters = {"region": "KEN"} 

data = ckan.action.datastore_search(resource_id=resource_id, filters=filters)
for record in data['records']:
    print 'region: {x}, value: {y}'.format(x=record['region'], y=record['value'])
```


### Datastore_delete
##### Parameters
*   resource_id (string) – resource id that the data will be deleted from. (optional)
*	force (bool (optional, default: False)) – set to True to edit a read-only resource
*	filters (dictionary) – filters to apply before deleting (eg {“name”: “fred”}). If missing delete whole table and all dependent views. (optional)




##### Javascript
```javascript
<script>
    var client = new CKAN.Client('http://giv-oct.uni-muenster.de:5000', '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39');
    var resourceId = '450f2c55-425f-4797-8d70-33b5729d1f1d';

    var nfilters = {"region": 'KEN'};

    var search = client.action('datastore_delete', {
                resource_id:  resourceId,
                filters: nfilters,
                force: 'True'
            },
            function(err) {
                if (err) console.log(err);
                console.log('All done');
            })
</script>
```

##### Python
```python
#!/usr/bin/env python2
import ckanapi

remote = 'http://giv-oct.uni-muenster.de:5000'
apikey = '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39'
resource_id = 'c123ba85-41f9-4a04-80f5-a26368ba9204'

ckan = ckanapi.RemoteCKAN(remote, apikey)

filters = {"region": "KEN"} 

data = ckan.action.datastore_delete(resource_id=resource_id, filters=filters, force= True)
```