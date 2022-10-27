# TODO

## 参考

🗄
* `sql.md`
* `system.md` distributed
🔍 
* https://dba.stackexchange.com
* https://roadmap.sh/postgresql-dba
📚
* Connolly database systems
* Kleppmann data intensive applications
* Takahashi manga databases
* Winand sql perf https://use-the-index-luke.com/

## current

## next

Mongo aggregations
* 📙 Bradshaw guide
* https://github.com/tommyboytech/t3/pull/9998/files
* https://github.com/tommyboytech/t3/pull/10084/files
* https://github.com/tommyboytech/t3/pull/10146/files
* repl - add functions to map all full paths user-track and track-user

BYO database 📙 Dibernardo, Kleppmann
* https://architecturenotes.co/things-you-should-know-about-databases/
* https://www.hytradboi.com/
* https://cstack.github.io/db_tutorial/
* https://github.com/eatonphil/gosql
* https://notes.eatonphil.com/database-basics.html
* https://notes.eatonphil.com/database-basics-expressions-and-where.html
* https://notes.eatonphil.com/database-basics-indexes.html
* https://notes.eatonphil.com/database-basics-a-database-sql-driver.html

## done

* _22_: 📙 Bradshaw ch. 1/4/7/10/14/18
* _21_: data eng
* _20_: Postgres with Django (psycopg, Docker) 📙 Kleppmann section 1

# DATA ENG

🗄 `system.md` Kafka
📻 Macey https://softwareengineeringdaily.com/2019/07/23/data-engineering-with-tobias-macey/

https://benn.substack.com/p/work-like-an-analyst

access patterns
> Take data access patterns very seriously!...it's easy to turn something that should be logarithmic time into polynomial time https://calpaterson.com/activerecord.html
* _access pattern_: how you have to query based on schema https://calpaterson.com/non-relational-beartraps.html
* what you're prioritizing e.g. read/write vs. aggregations 📻 Macey 6:10
* _upsert_: insert or update 📙 Bradshaw [46]
* _get-or-create_: `get_or_create()` in Django
* aka find-create-find

business intelligence 🗄 `ml.md` data science
* _business intelligence (BI)_: exploration (for non-devs), reports 🗄 utils/exploration, `python.md` visualization
* ChartIO https://news.ycombinator.com/item?id=22548217
* Looker: more legacy? https://www.youtube.com/watch?v=M8oi7nSaWps 0:30 OSS version https://github.com/lightdash/lightdash
* Lux https://softwareengineeringdaily.com/2021/05/27/data-exploration-with-a-new-python-library-with-doris-lee/ https://github.com/lux-org/lux
* Tableau
* https://news.ycombinator.com/item?id=30323131
* OSS: Redash https://github.com/getredash/redash Poli https://github.com/shzlw/poli

industry
* _data engineer_: shepard (ETL) librarian (catalog) https://www.youtube.com/watch?v=qqlbYDfqeI4 1:45
> But if data analytics usually means extracting insights from existing data, data engineering means the process of building infrastructure to deliver, store and process the data. https://khashtamov.com/en/how-to-become-a-data-engineer/
* vs. web dev https://tech.marksblogg.com/is-hadoop-dead.html
> The above projects often aren't advertised in a way that web developers would be exposed to them. This is why someone could spend years working on new projects that are at the bottom of their S-curve in terms of both growth and data accumulated and largely never see a need for data processing outside of what could fit in RAM on a single machine.
> Web Development was a big driver in the population growth of coders over the past 25 years. Most people that call themselves a coder are most often building web applications. I think a lot of the skillsets they possess overlap well with those needed in data engineering but often distributed computing, statistics and storytelling are lacking.
> Websites often don't produce much load with any one user and often the aim is to keep the load on servers supporting a large number of users below the maximum hardware thresholds. The data world is made up of workloads where a single query is trying its best to maximize a large number of machines in order to finish as quickly as possible while keeping the infrastructure costs down.
> Companies producing PBs of data often have a queue of experienced consultants and solutions providers at their door. I've rarely seen anyone plucked out of web development by their employer and brought into the data platform engineering space; it's almost always a lengthy, self-retraining exercise.

## big data

📙 Kleppmann ch. 10

tools
* _Hadoop_: n computers coordinate processing for petabytes of data 🗄 `infra.md` EMR
* no one uses anymore? https://news.ycombinator.com/item?id=30595026
> Whereas Hadoop and big data targeted analytics appli‐ cations, often in the data warehousing space, the low latency nature of Kafka makes it applicable for the kind of core applications that directly power a business 📙 Narkhede kafka 
* setup https://tech.marksblogg.com/hadoop-up-and-running.html
* you probably don't need it https://www.benkuhn.net/hard/
* relationship to other projects like Presto, Clickhouse https://tech.marksblogg.com/is-hadoop-dead.html
* _MapReduce_: map (split query into chunks, execute in parallel) reduce (merge results) 📙 Kleppmann 46
* map (match) reduce (group) https://www.practical-mongodb-aggregations.com/intro/history.html
* also a query language 📙 Kleppmann 46
* PRQL = alternative query language https://news.ycombinator.com/item?id=30060784
* _HDFS_: distributed file system http://aosabook.org/en/hdfs.html
* pools all disks from cluster
* files replicated across nodes (not all nodes; two additional copies)
* _pyspark_: Python API to Spark https://www.youtube.com/watch?v=XrpSRCwISdk
* _Spark_: Pandas + distributed
* used for ML https://tech.marksblogg.com/is-hadoop-dead.html
* kinda part of Hadoop, kinda not https://tech.marksblogg.com/is-hadoop-dead.html
> At some point, the Spark community tried to distance itself from the Hadoop ecosystem. They didn't want to be seen as built on legacy software nor as some sort of "add-on" for Hadoop. Given the level of integration, Spark has with the rest of the Hadoop ecosystem and given the 100s of libraries from other Hadoop projects being used by Spark I don't subscribe to the belief that Spark is its own thing.

factors
* size: can't fit into normal dbms
* velocity: challenges processor to keep up
* variety: polyglot https://www.youtube.com/watch?v=KRcecxdGxvQ 📙 Kleppmann 18

size
* MB = Excel, nGB-1TB = Postgres, >5TB = Hadoop https://www.chrisstucchio.com/blog/2013/hadoop_hatred.html
* _small data_: can fit on a phone (so, half a terabyte) https://simonwillison.net/2021/Jul/22/small-data/
* complete works of Shakespeare only 5.5 MB 📙 Conery 345
* ways of thinking about data sizes: 1MB vs. 1M seconds (12 days) 1GB vs. 1B seconds (31 years) 1TB vs. 1T seconds (317 centuries) 📙 Conery 345
> the term Big Data is so over-used and under-defined that it is not useful in a serious engineering discussion. 📙 Kleppmann 1.9
> There are diminishing returns to the amount of information you can extract from data. The tenth gigabyte is worth much less than the second gigabyte. https://www.evanmiller.org/small-data.html

## ETL

🗄 logging

* _ETL_: mv fact tables to dimensionsal 📙 Conery 323
* _ELT_: cp facts tables, then mv to dimensionsal https://www.youtube.com/watch?v=voC0ewDeltA 4:00
* allows analysts to do the transformations they need vs. having to figure it out up front https://www.youtube.com/watch?v=qqlbYDfqeI4 7:00
* _transform_: 名 step that remodels data to dimensionsal https://www.youtube.com/watch?v=M8oi7nSaWps 3:30
* e.g. head/tail, add/rm col, type conversion, join https://www.youtube.com/watch?v=llRLh8cM7QI 15:50
* testing: validate integrity https://github.com/great-expectations/great_expectations https://softwareengineeringdaily.com/2020/02/17/great-expectations-data-pipeline-testing-with-abe-gong/ https://github.com/socialpoint-labs/sqlbucket
* syncing datastores https://sirupsen.com/napkin/problem-14-using-checksums-to-verify https://sirupsen.com/napkin/problem-8 🗄 backup

tools
* _Airbyte_: pull from data source https://www.youtube.com/watch?v=l48zwwRSGeA
* workflow https://www.youtube.com/watch?v=qqlbYDfqeI4 11:00-11:15
* plain text vs. crappy GUI tools for analysts https://www.youtube.com/watch?v=M8oi7nSaWps 5:45 https://www.youtube.com/watch?v=qqlbYDfqeI4 9:40
* _DBT_: tool for transforms https://www.youtube.com/watch?v=l48zwwRSGeA 6:15
* create views via ETL in Snowflake (at UM)
* data ingestion from Snowflake using Snowpipe https://docs.snowflake.com/en/user-guide/data-load-snowpipe-intro.html
* metrics https://news.ycombinator.com/item?id=30938109
* why does everyone love it so much? https://highgrowthengineering.substack.com/p/why-is-dbt-so-important-
> Fivetran as the best-in-class E and L, and dbt as the corresponding T. https://luttig.substack.com/p/dont-forget-microsoft
* _petl_: transforms https://petl.readthedocs.io/en/stable/
* if petl can only handle thousands of records, why not just use Pandas? https://www.youtube.com/watch?v=llRLh8cM7QI 9:30 25:00 https://petl.readthedocs.io/en/stable/

* visidata https://www.visidata.org/blog/2020/ten/

schemas
* _star schema_: fact table at center
* _snowflake schema_: like star schema but more normalized
* less popular bc harder to query 📙 Kleppmann 95
* _fact table_: transactions 📙 Kleppmann 93
* w/ many FK to other dimensions 📙 Kleppmann 95
* _dimension_: non-transactional tables 📙 Kleppmann 94 https://tech.marksblogg.com/data-fluent-for-postgresql.html

## OLAP

🗄 `sql.md` tables/views

taxonomy 📙 Kleppmann 90-95
* _data source_: where you're getting the data https://dataschool.com/data-governance
* _lake_: 类似 file system https://www.youtube.com/watch?v=V0GvZ_KAI70
* table format = structure of files (Parquet) that make up lake https://medium.com/expedia-group-tech/a-short-introduction-to-apache-iceberg-d34f628b6799
* Iceberg = SQL for table formats https://iceberg.apache.org/ https://www.thoughtworks.com/radar/platforms?blipid=202203012
* slower to access, has metadata (when was it produced, who owns it), batch writes, most reads will be humans doing analysis or exploration
* less expensive bc optimizing for large volume i.e. can use slower object storage 📻 Macey 31:30
* _warehouse_: DBaaS
> interesting at UM that they had an insights db, essentially a db for warehouse workloads but for the product vs. analysis
* typically different dbms from OLAP e.g. Redshift, BigQuery, Hive, Presto 📙 Kleppmann 93
* keeps more data in memory 📻 Macey 24:30
* more expensive bc optimizing for large volume and speed of access 📻 Macey 31:30
* streaming https://www.thoughtworks.com/radar/techniques?blipid=202203008
* _mart_: subset of warehouse
* uses star schema 📙 Conery 324
* _catalog_: manifest (desc, location) 📻 Macey 5:15 https://data.world/solutions/product-overview/
* Collibra https://www.thoughtworks.com/radar/platforms?blipid=202203049

warehouse dbms
* cloud: petabytes in single query and comes back in seconds/minutes e.g. Snowflake 📻 Macey 32:20
> I hear people arguing "a dataset can fit in memory". RAM capacity, even on the Cloud, has grown a lot recently. There are EC2 instances with 2 TB of RAM. RAM can typically be used at 12-25 GB/s depending on the architecture of your setup. Using RAM alone won't provide any failure recovery if the machine suffers a power failure. To add to this, the cost per GB will is tremendous compared to using disks. https://tech.marksblogg.com/is-hadoop-dead.html
* can always use Postgres https://brandur.org/warehouse https://tech.marksblogg.com/billion-nyc-taxi-rides-postgresql.html https://news.ycombinator.com/item?id=27109960
> I've also heard arguments that row-oriented systems like MySQL and PostgreSQL can fit the needs of analytical workloads as well as their traditional transactional workloads. Both of these offerings can do analytics and if you're looking at less than 20 GB of data it's probably not worth the effort of having multiple pieces of software running your data platform. https://tech.marksblogg.com/is-hadoop-dead.html
* _DuckDB_: embedded https://duckdb.org/ https://softwareengineeringdaily.com/2022/03/18/duckdb-with-hannes-muleisen/
* _Presto_: distributed query engine https://tech.marksblogg.com/presto-parquet-airpal.html https://tech.marksblogg.com/billion-nyc-taxi-rides-hive-presto.html
* _BigQuery_: really fast https://tech.marksblogg.com/billion-nyc-taxi-rides-bigquery.html https://dataschool.com/sql-optimization/bigquery-optimization
* _Snowflake_: users/investors like them https://news.ycombinator.com/item?id=24265041 https://dataschool.com/sql-optimization/snowflake/ https://www.youtube.com/watch?v=xojAXXRo_S0
* apparently a lot faster and easier to manage than a Hadoop installation https://news.ycombinator.com/item?id=24641481 
* can build dashboards off queries
* _Redshift_: https://tech.marksblogg.com/billion-nyc-taxi-rides-redshift.html https://dataschool.com/sql-optimization/optimizing-data-queries-with-redshift/

OLTP
> If you have a transactional need for your dataset it's best to keep this workload isolated with a transactional data store. This is why I expect MySQL, PostgreSQL, Oracle and MSSQL to be around for a very long time to come. https://tech.marksblogg.com/is-hadoop-dead.html
* data: application
* model: relational
* schema: DIY
* interface: SQL 📙 Kleppmann 93
* access pattern: writes 📙 Kleppmann 90
* consumers: users

OLAP
> But would you like to see a 4-hour outage at Uber because one of their Presto queries produced unexpected behaviour? Would you like to be told your company needs to produce invoices for the month so the website will need to be switched off for a week so there are enough resources available for the task? Analytical workloads don't need to be coupled with transactional workloads. You can lower operational risks and pick better-suited hardware by running them on separate infrastructure. https://tech.marksblogg.com/is-hadoop-dead.html
* data: from n data sources (application, analytics) 📙 Kleppmann 92
* model: non-relational 📙 Kleppmann 93, 101
* schema: star
* interface: SQL 📙 Kleppmann 93
* access pattern: reads (aggregates) 📙 Kleppmann 90-92
* consumers: DBA, BI, ML https://softwareengineeringdaily.com/2021/07/14/data-science-on-aws-implementing-ai-and-ml-pipelines-on-aws-with-chris-fregly/

# MONGO

📙 Bradshaw guide
🎓 https://university.mongodb.com/dashboard
📜
* Mongo https://www.mongodb.com/docs/manual
* PyMongo https://pymongo.readthedocs.io/en/stable/tutorial.html

lookups
> workaround for $$ notation just eliminate aliasing?
* dot nota
```js
// dot notation: reference subdocument key 📙 Bradshaw [63] https://www.mongodb.com/docs/manual/core/document/#dot-notation
db.people.find({"name.first": "bob"})

// field path ($) = dot notation for stage's input documents 📙 Bradshaw [173]
{$project: {amount: "$funding_rounds.amount"}}

// variable notation ($$) = reference variable in expression 📙 Bradshaw [174]
{
    $project: {
        rounds: {$filter: {
            input: "$funding_rounds",
            as: "round",  // variable definition
            cond: {$gte: ["$$round.raised_amount", "$1M"]}  // reference
        }}
    }
}
```
queries
* _query document_: arg to `find()`, `aggregate()` 📙 Bradshaw [53]
* _cursor_: return from aggregation
* iterator, also a connection object 📙 Bradshaw [66]
* lazy evaluation i.e. cursor doesn't query db until all operators evaluated 📙 Bradshaw [66]
* only fetches 100 results or 4 MB on evaluation
* `hasNext()`: bool on whether next el to fetch 📙 Bradshaw [66]
* `next()`: fetches next el
* _immortal_: cursor that you explicitly need to iterate fully through or kill 📙 Bradshaw [71]
* _projection_: specify keys to return per document i.e. select 📙 Bradshaw [196]
* via dict keys in PyMongo
* do last bc expensive operation and want to run on as few documents as possible 📙 Bradshaw [166]

semantics
* _field_: key
* _normal collection_: size dynamic 📙 Bradshaw [151]
* _capped collection_: size static 📙 Bradshaw [151]
* _natural order_: order of documents on disk https://www.mongodb.com/docs/v4.4/reference/method/db.collection.findOne/

monitoring
* `db.currentOp()` connection id, operation id, seconds running 📙 Bradshaw [371]
* stats: `db.stats()` and `db.col.stats()`
* some long-running ops are not normal queries but for replication 📙 Bradshaw [375]
* profiler will slow down db, can set it to only observe queries that take long than 100ms 📙 Bradshaw [376,378]
* _acknowledged write_: waits until previous write completed vs. just sitting in an os buffer 📙 Bradshaw [376]
* _phantom writes_: write waiting in the os buffer after you've already stopped client from sending further writes 📙 Bradshaw [376]

za
* implementation http://aosabook.org/en/nosql.html
* certification https://university.mongodb.com/certification/developer/about exam https://university.mongodb.com/certification/exam-prep
* indexes 📙 Bradshaw [384]
* _mongod_: server daemon; port 27107 📙 Bradshaw [227,290]
* _MongoEngine_: ODM i.e. doesn't return dicts like PyMongo https://stackoverflow.com/a/41323384
* _Mongo tools_: https://github.com/mongodb/homebrew-brew `brew install mongodb-database-tools`
* _Beanie_: ODM https://talkpython.fm/episodes/show/349/meet-beanie-a-mongodb-odm-pydantic
* _Atlas_: managed Mongo
* _Charts_: Atlas + visualization

replication 🗄 `system.md` data
* _replica set_: cluster 📙 Bradshaw [227]
* changing normal mongod server to replica set involves downtime so just config as 1-server set from start 📙 Bradshaw [231]
* connection config comes from primary 📙 Bradshaw [230]
* 1 primary (writes) n secondaries (replication)
* if primary unavailable secondaries elect new primary 📙 Bradshaw [227,235,243,244]
* secondaries become primary due to priority + election algorithm 📙 Bradshaw [244]
* need majority to elect primary bc don't want two primary in event of network partition 📙 Bradshaw [241]
* _data node_: node that holds data 📙 Bradshaw [247]
* _arbiter_: secondary holding no data whose only point is to participate in elections for 2-member replica sets 📙 Bradshaw [246]
* generally shouldn't be used [247]
* _passive_: secondaries w/ priority of 0 i.e. can never become primary 📙 Bradshaw [244]
* _hidden member_: secondary that doesn't get requests routed to it and won't get replicated to often 📙 Bradshaw [245]
* for low-powered servers

partition 🗄 `system.md` data
* _mongos_: routing process in front of sharding cluster 📙 Bradshaw [290,293]
* can shard on single machine 📙 Bradshaw [291]
* _shard key_: field used to chuck data e.g. if `username` then alice-candace, david-fred, etc. 📙 Bradshaw [294]

## aggregation

📜
* https://docs.mongodb.com/manual/aggregation/
* https://www.practical-mongodb-aggregations.com

grouping https://www.mongodb.com/docs/upcoming/reference/operator/aggregation/group/
* output document per group by `_id` 📙 Bradshaw [189] https://www.mongodb.com/docs/upcoming/reference/operator/aggregation/group/#group-title-by-author
```js
// regular syntax
$group : { 
    _id : "$author",  // group
    books: { $push: "$title" }  // accumulator
}

// label syntax; neither Bradshaw [193] nor the docs explain https://www.mongodb.com/docs/upcoming/reference/operator/aggregation/group/#optimization-to-return-the-first-document-of-each-group
$group : { 
    _id : { author: "$author"},
    books: { $push: "$title" }
}
```
* _accumulator_: mostly SQL aggregates (min/mix/avg) + misc functionality (push) https://www.mongodb.com/docs/upcoming/reference/operator/aggregation/group/#std-label-accumulators-group
* can run w/out grouping e.g. count https://www.mongodb.com/docs/upcoming/reference/operator/aggregation/group/#count-the-number-of-documents-in-a-collection
* _push_: add el to list as obj added to group 📙 Bradshaw [194]
* only works in group stage 📙 Bradshaw [196]
* _addToSet_: push + no dupes 📙 Bradshaw [186]

operations
* array expressions: filter, slice, `$arrayElemAt` 📙 Bradshaw [181,184,186]
* _filter_: comparison operator for projection stage of aggregation 📙 Bradshaw [181]
```js
$project: {
    items: {
        $filter: {
            input: "$items",
            as: "item",
            cond: { $gte: [ "$$item.price", 100 ] }
        }
    }
}
db.sales.aggregate([
   {
   }
])
```
* find doesn't require projection for this so idky aggregation does
* _match_: predicate; earlier the better 📙 Bradshaw [165,180]
* _unwind_: create output document for each el in array field 📙 Bradshaw [174]
```diff
- {
-    k: v,
-    k: [1,2]
- }
+ {
+    k: v,
+    k: [1]
+ }
+ {
+    k: v,
+    k: [2]
+ }
```
* _lookup_: left outer join https://www.mongodb.com/docs/manual/reference/operator/aggregation/lookup/
```js
db.orders.aggregate([             // FROM orders
    {
        $lookup: {
            from: "inventory",    // JOIN inventory
            localField: "item",   // ON orders.item
            foreignField: "sku",  // = inventory.sku
            as: "inventory_docs"  // stdout alias
        }
    }
])
```

semantics
* _aggregation_: operation on a pipeline 📙 Bradshaw [166]
* _pipeline_: array of stages 📙 Bradshaw [166]
* same idea as UNIX pipes 📙 Bradshaw [162]
* introduced w/ version 3.2 📙 Bradshaw [5]
* preceded by MapReduce https://www.practical-mongodb-aggregations.com/intro/history.html
* no SSoT for how to do things btw `find()` and `aggregate()`
* _stage_: input document + operator = output document 📙 Bradshaw [162,166]
* can have multiple of the same type 📙 Bradshaw [180]
* each stage takes input from previous stage 📙 Bradshaw [161]
* input and output of each stage also a document 📙 Bradshaw [161]

## find

📜 Mongo https://www.mongodb.com/docs/manual/crud/

* syntax: `db.col.find(query)`
* get collections `sorted(db.collection_names())`

basic
* can't refer to another key in document e.g. `find({"balance": "this.profit - this.loss})` 📙 Bradshaw [55]
* null 📙 Bradshaw [57]
* regex 📙 Bradshaw [58]
```sh
# SELECT * FROM TAB
db.col.find()

# SELECT * FROM TAB LIMIT 1
db.col.findOne()  # for n, returns 1 according to natural order https://www.mongodb.com/docs/v4.4/reference/method/db.collection.findOne/
db.col.find_one() # same as mongosh? https://github.com/mongodb/mongo-python-driver/blob/6e99bf451503825577213ef148ec6b519a41257b/pymongo/collection.py#L1388

# SELECT * FROM TAB LIMIT N
db.col.find().limit(n)  # for pagination 📙 Bradshaw [69] can also use slice() or skip() 📙 Bradshaw [60,67]

# COUNT https://stackoverflow.com/a/4415593
db.col.find().count()

# SORT
db.col.find().sort({age: 1})  # asc
db.col.find().sort({age: -1}) # desc
```

predicates
* can use `$where` queries but shouldn't bc slower, use `$expr` instead 📙 Bradshaw [65]
```sh
# SELECT * FROM TAB WHERE COL = VAL 📙 Bradshaw [54]
{f:v}
# NESTED
{f1.f2: v}

# MEMBERSHIP 📙 Bradshaw [56]
{f: {$in: [a, b]}}
# EXACT MATCH ON N 📙 Bradshaw [59]
{f: { $all: [a, b]}}

# LOGICAL OPERATORS 
{f1: v, f2: v}
# `[]` for empty list https://stackoverflow.com/a/25142571
{$and: [{f1: {$eq: null}}, {f2: {$ne: null}}]}  # 📙 Bradshaw [56] https://stackoverflow.com/a/69314784

# EQUALITY
db.col.find({likes: 0})
# INEQUALITY
db.col.find({likes: {$ne: 1}})

# COMPARISON 📙 Bradshaw [55]
db.post.find({likes: {$gt: 1}})
```

## shell

🗄 utils/GUIs

workflows
* _iPython_: write in driver language (PyMongo), run in REPL
* ✅ good at reuse
* ❌ slow for sketching
* need for work bc can only access some collections via corpus obj
* _RoboMongo_: https://github.com/Studio3T/robomongo https://www.practical-mongodb-aggregations.com/intro/getting-started.html
* _Compass_: write in GUI query editor, run in GUI https://www.mongodb.com/products/compass
* ❌ doesn't work with server versions before 3.6
* ✅ good at sketching simple queries
* ❌ bad at sketching complex queries bc bad editing (no Vim or syntax highlighting)
* ❌ bad at reuse
* ✅ good at aggregations https://www.practical-mongodb-aggregations.com/intro/getting-started.html#mongodb-compass-gui
* _DbGate_: queryless via GUI, run in GUI
* ✅ good at sketching
* ❌ bad at reuse
* _mongosh_: write in text editor, run in terminal
* ❌ slow at sketching bc vim mode in readline never seems to work
* ✅ text editor = Vim, syntax highlighting but 1) slow 2) ephemeral
* ✅ text editor = Vim, syntax highlighting but 1) slow 2) ephemeral

REPL
* mongorc
```js
function foo(value){return [{$match: {"key": `${value}`}}]}
db.col.aggregate(foo(arg))
```
* `edit`: for writing more complex queries/aggregations https://stackoverflow.com/a/28074078
* not actually a good solution bc will fail silently if parsing error
```js
// edit q
{
    $and: [
        { "id": "foo" },
        { "other_col_id": { $ne: "bar"} } 
    ]
},
// edit p
{"thing1": 1, "thing2":1, "_id":0}
// run
db.col.find(q, p)
```

mongo
* warning https://docs.mongodb.com/v4.4/mongo/#start-the-mongo-shell-and-connect-to-mongodb
* install as standalone https://github.com/mongodb/homebrew-brew#installing-only-the-shell-or-the-database-tools
```sh
$ brew tap mongodb/brew
$ brew install mongodb-community-shell
```
* prompt: display host/user https://www.mongodb.com/docs/manual/tutorial/configure-mongo-shell/#customize-prompt-to-display-database-and-hostname https://stackoverflow.com/a/21417240

mongosh https://docs.mongodb.com/mongodb-shell 
* methods https://docs.mongodb.com/mongodb-shell/reference/methods/
* config: if you're connecting to remote, mongo will still use config on local https://docs.mongodb.com/mongodb-shell/run-commands/#.mongoshrc.js-file https://stackoverflow.com/a/11397470
* enhanced https://github.com/TylerBrock/mongo-hacker
```sh
# shell history https://docs.mongodb.com/mongodb-shell/logs/#view-mdb-shell-command-history
~/.mongodb/mongosh/.mongosh_repl_history
# shell logs https://docs.mongodb.com/mongodb-shell/logs/#view-the-log-for-the-session
~/.mongodb/mongosh/
# clear console
cls

# connect https://docs.mongodb.com/mongodb-shell/connect/
mongo -u user -p pw 127.0.0.1:6017/db
mongosh --port 27017

# view connection info https://docs.mongodb.com/mongodb-shell/connect/#verify-current-connection
db.getMongo()          # Mongo shell
db.collection_names()  # PyMongo REPL https://stackoverflow.com/a/9805506

db  # view current db
show dbs  # view all dbs
use <db>  # switch/create db
show collections  # view collections
```

# NON-RELATIONAL

> There are data stores that are also used as message queues (Redis), and there are message queues with database-like durability guarantees (Kafka), so the boundaries between the categories are becoming blurred 📙 Kleppmann 12

* modeling from different angles https://www.openmymind.net/2011/7/5/Rethink-your-Data-Model/

* _EdgeDB_: graph-relational = no impedance mismatch but still relational https://news.ycombinator.com/item?id=30290225
* written in Python on top of Postgres https://talkpython.fm/episodes/show/355/edgedb-building-a-database-in-python

---

* Datomic (Hickey), datalog/prolog https://news.ycombinator.com/item?id=21742222 https://kevinlynagh.com/newsletter/2022_04_on_datalog_application_databases/ https://news.ycombinator.com/item?id=31154039
* can be a problem is you need to change the PK https://calpaterson.com/non-relational-beartraps.html
> Changing the primary key of a table is a surprisingly common activity. In truth, it's pretty easy to pick something that initially looks like it will be unique but which later turns out to not be unique...Unfortunately, in many non-relational database systems the primary key is "special". For example, Dynamo-style systems will use the primary key to decide which of the partitions the record will go on.
* _polyglot persistence_: using multiple types of data stores 📙 Kleppmann 2.29 because choosing just one is no fun :) https://old.reddit.com/r/learnpython/comments/glbuog/whats_is_your_decision_process_between_csv_json/
* _CRDT_: https://blog.acolyer.org/2019/11/20/local-first-software/ https://martin.Kleppmann.com/2020/07/06/crdt-hard-parts-hydra.html https://caolan.uk/articles/inside-a-collaborative-text-editor/ vs OT (operational transformations) https://news.ycombinator.com/item?id=24176455 https://news.ycombinator.com/item?id=24617542 https://news.ycombinator.com/item?id=24790170
* _block_: https://news.ycombinator.com/item?id=27200177
* immutable https://github.com/codenotary/immudb

## column

📙 Kleppmann chapter 3
🗄 `computers.md` encoding/CSV, Parquet

* _column store_: not row-oriented (like OLTP)
* e.g. instead of looking for all `price` values by iterating over every sale record, just grab `price` column 📙 Kleppmann 96
* ❓ stores data differently on disk https://nchammas.com/writing/database-access-patterns
* in order to reconstruct a row, everything in row must be stored as nth in column 📙 Kleppmann 100
> Neither Parquet nor ORC files existed prior to 2012. These file formats were instrumental in making analytics fast on Hadoop. Prior to these formats, workloads were largely row-oriented. If you needed to transform TBs of data and could do so in a parallel fashion then Hadoop did a good job of that. MapReduce was a framework often used for this purpose. What columnar storage offered was a way to analyse TBs of data in seconds. This proved to be a more valuable proposition to more businesses. Data Scientists may only need a small amount of data to produce insights but they'll need to look over a data lake with potentially PBs of data to pick out what they need first. Columnar analytics is key for them to build the data fluency needed to know what to cherry-pick. https://tech.marksblogg.com/is-hadoop-dead.html
* _wide column store_: ❓

dbms https://en.wikipedia.org/wiki/List_of_column-oriented_DBMSes
* Cassandra https://stackoverflow.com/q/13010225 📙 Kleppmann 99 https://news.ycombinator.com/item?id=28292369 https://simonwillison.net/2021/Aug/24/how-discord-stores-billions-of-messages/
* _Bigtable_: wide table = document store in SQL https://en.wikipedia.org/wiki/Wide-column_store
* _HBase_: Hadoop db

## document

📙 Kleppmann 2.28-42

document store
* _document_: JSON "obj"
* replaces row as paradigm 📙 Bradshaw [3]
* _schema_: structure of document https://docs.mongodb.com/realm/schemas/
* not fixed i.e. inconsistent intra-collection 📙 Bradshaw [3]
* _document reference_: UUID 📙 Kleppmann 3.38
* _field_: key
* _subdocument_: document key whose value is itself a document https://youtu.be/SM9gJv08dm0 1:20
* aka embedded 📙 Bradshaw [174]
* _collection_: group of documents

design
* 1-M w/in document itself
* M-M via document reference 📙 Kleppmann 3.38
* joins https://news.ycombinator.com/item?id=22834036
* good for 1-M or no relationships 📙 Kleppmann 2.49
* flexiblity: schema per doc aka schemaless/schema-on-read, obviates need for migrations 📙 Kleppmann 2.63, 4.111
* easier to scale/shard apparently, locality 📙 Kleppmann 2.32
* transactions only at level of single document https://docs.mongodb.com/v3.4/core/write-operations-atomicity/
* easy to have dupes 📙 Kleppmann 2.33
* hands off processing to application, so it's both slower in dev time and execution time 📙 Bradshaw [8]

dbms
* BYO https://notes.eatonphil.com/documentdb.html
* _CouchDB_: good at replication https://www.dataengineeringpodcast.com/couchdb-document-database-episode-124/ 7:15 
* Mongo
* _Postgres_: JSON
* _TinyDB_: embedded https://github.com/msiemens/tinydb
* alternatives https://github.com/256dpi/lungo https://github.com/vincentdchan/PoloDB
* not atomic but potential workaround https://tinydb.readthedocs.io/en/latest/extensions.html#tinyrecord
```python
from tinydb import TinyDB, Query
db = TinyDB("/path/to/db.json")
q = Query()
```

hierarchical
* _hierarchical database_: document store + tree structure i.e. child only has one parent 📙 Takahashi 2.39
* too rigid for a data store https://stratechery.com/2016/oracles-cloudy-future/ https://twobithistory.org/2017/12/29/codd-relational-model.html
* e.g. file system, DNS https://www.postgresql.org/docs/12/tutorial-concepts.html 📙 Kleppmann 2.36-38
* used in Zookeeper https://www.youtube.com/watch?v=Vv4HpLfqAz4 8:50
* can be done in relational as well https://hoverbear.org/blog/postgresql-hierarchical-structures/
* _IMS_: https://twobithistory.org/2017/10/07/the-most-important-database.html

## graph

* _network database_: similar to graph https://stackoverflow.com/a/52325525 📙 Takahashi 2.39 anything that would have ever been network is now SQL https://www.prisma.io/blog/comparison-of-database-models-1iz9u29nwn37 📙 Kleppmann 2.36

dbms
* Mongo offers as well https://www.mongodb.com/databases/mongodb-graph-database
* _Janus_: distributed, OSS https://github.com/JanusGraph/janusgraph
* _Tao_: distributed https://news.ycombinator.com/item?id=29045443 https://www.micahlerner.com/2021/10/13/tao-facebooks-distributed-data-store-for-the-social-graph.html

query languages
* _Cypher_: declarative
* _GQL_: emerging standard https://stackoverflow.com/q/13824962 https://www.youtube.com/watch?v=h8cyPIEfxQY 11:30
* _Gremlin_: wrapper over Neo4J Java API

---

* https://www.kaseyklimes.com/notes/2019/10/16/an-augmented-mind-designing-a-personal-knowledge-base-with-notion
* _use cases_: good at relationships btw heterogenous data ("does Alice follow Bob?") w/out a million joins  📙 Kleppmann 2.49, 2.63 bad at aggregates or anything that deals w/ a few attr over many records; used for networks (IAM, knowledge mgmt, Git, recommendation engine) https://www.youtube.com/watch?v=h8cyPIEfxQY 14:30
* _dbms_: Tiger Graph, Dgraph https://softwareengineeringdaily.com/2021/01/19/dgraph-native-graphql-database-with-manish-jain/ Memgraph, Terminus db, Neo4J https://media.pragprog.com/titles/pwrdata/neo4j.pdf embedded https://github.com/CodyKochmann/graphdb https://github.com/dpapathanasiou/simple-graph cache for dgraph https://github.com/dgraph-io/ristretto
* _OGM_: ORM for graphs https://www.youtube.com/watch?v=h8cyPIEfxQY 12:30

* _property graph_: vertex (id, dict of properties, and list of incoming/outgoing edges) edge (id, dict of properties, start/end vertices and descriptive label) 📙 Kleppmann 2.50
* _triple-store_: subject (vertex) predicate, object (value or another vertex) 📙 Kleppmann 2.55 used by Datomic (Datalog query language) 📙 ibid 2.50, 60, 63
* _RDF (resource description framework)_: triple store for semantic web 📙 Kleppmann 2.57 SPARQL query language 📙 ibid 59 https://twobithistory.org/2020/01/05/foaf.html
* _types_: https://stackoverflow.com/a/59532041/6813490
* visualization https://github.com/shahinrostami/chord https://github.com/plotly/falcon
* _sink_: https://github.com/brettkromkamp/contextualise https://www.youtube.com/watch?v=GekQqFZm7mA https://www.denizcemonduygu.com/philo/ http://aosabook.org/en/500L/dagoba-an-in-memory-graph-database.html https://pragprog.com/book/pwrdata/seven-databases-in-seven-weeks-second-edition

## key

🗄 `system.md` distributed/consensus

* _KV store_: hash map + persistence 📙 Kleppmann [72]
* options: Redis, Bitcask
* distributed KV store used for service discovery (etcd) ()
* used for metadata, counters
> ZippyDB serves a number of use cases, ranging from metadata for a distributed filesystem, counting events for both internal and external purposes, to product data that’s used for various app features https://engineering.fb.com/2021/08/06/core-data/zippydb/
* impl: hash index; faster not bc they don't have to go to disk but bc don't have to translate in-mem data structure to something that can be written to disk 📙 Kleppmann [89]
* typed values allow for in/decrement, push/pop from list
* used for caching db result set e.g. memcached 📙 Kleppmann [89] https://github.com/akrylysov/pogreb
* dbms: embedded https://github.com/patx/pickledb https://github.com/spacejam/sled https://github.com/charmbracelet/skate https://github.com/dgraph-io/badger disk for storage https://github.com/peterbourgon/diskv
* RocksDB, memcached used as storage for distributed KV https://github.com/bitleak/kvrocks https://engineering.fb.com/2021/08/06/core-data/zippydb/ https://www.micahlerner.com/2021/05/31/scaling-memcache-at-facebook.html
* BYO: https://aosabook.org/en/500L/dbdb-dog-bed-database.html Bitcask https://github.com/avinassh/py-caskdb
> In short, keys are stored in a hash table in RAM, k/v pairs are written to log files. Dead simple, but powerful enough. https://news.ycombinator.com/item?id=31306678

za
* _object store_: KV in which K is ID and V is blob (file, binary) 🗄 `infra.md` AWS/S3
* can only create/update, not append https://stackoverflow.com/a/47524241
* sink https://ceph.io/ceph-storage/ https://github.com/minio/minio https://stackoverflow.com/questions/56627446/docker-compose-how-to-use-minio-in-and-outside-of-the-docker-network https://alexwlchan.net/2020/08/s3-keys-are-not-file-paths
* _flat file_: meant for config, no way to represent relationships or handle concurrency (e.g. prevent dirty read); some structure via delimiters, new lines https://www.prisma.io/blog/comparison-of-database-models-1iz9u29nwn37

## time series

todo
* https://www.youtube.com/watch?v=nT6UsVgJ0xw
* https://www.youtube.com/watch?v=Z6pghPlZ1vQ
* time-weighted average https://blog.timescale.com/blog/what-time-weighted-averages-are-and-why-you-should-care/?
* https://www.honeycomb.io/blog/time-series-database/
* https://news.ycombinator.com/item?id=28901063
* https://www.influxdata.com/blog/start-python-influxdb

basics
* _time series_: KV in which K is time https://en.wikipedia.org/wiki/Time_series_database
* used for monitoring 🗄 `system.md`
* _panel data_: timeseries for individuals https://en.wikipedia.org/wiki/Panel_data

libs
* _darts_: https://github.com/unit8co/darts/
* _kats_: https://github.com/facebookresearch/kats
* _sktime_: https://github.com/alan-turing-institute/sktime

dbms
* _Influx_: https://softwareengineeringdaily.com/2019/08/21/time-series-databases-with-rob-skillington/ https://softwareengineeringdaily.com/2021/08/19/influxdata-time-series-data-with-russ-savage/
* _Timescale_: built on Postgres https://blog.timescale.com/blog/how-postgresql-aggregation-works-and-how-it-inspired-our-hyperfunctions-design-2/ https://softwareengineeringdaily.com/2021/06/28/timescale-time-series-databases-with-mike-freedman/
* _tstorage_: embedded https://github.com/nakabonne/tstorage BYO https://nakabonne.dev/posts/write-tsdb-from-scratch/ https://news.ycombinator.com/item?id=27730854
* _Whisper_: embedded db for Graphite https://github.com/graphite-project/whisper

# PLUMBING

📹 CMU https://www.youtube.com/playlist?list=PLSE8ODhjZXjbohkNBWQs_otTrBTrjyohi https://www.youtube.com/playlist?list=PLSE8ODhjZXjasmrEd2_Yi1deeE360zv5O
📙 https://www.interdb.jp/pg/

* _correlation_: correlation btw storage on disk and order of rows https://hakibenita.com/sql-tricks-application-dba#always-load-sorted-data

optimization
* queries: avoid `distinct`, `having`, subqueries, `*` https://dataschool.com/sql-optimization/optimize-your-sql-query/
* query plan
* use indexes

## connections

* _wire protocol_: protocol for db client-server https://datastation.multiprocess.io/blog/2022-02-08-the-world-of-postgresql-wire-compatibility.html
* e.g. can translate Mongo protocol to SQL and store in Postgres https://github.com/FerretDB/FerretDB

order
* 1 auth 📙 Beaulieu 3.41
* 2 assigned connection ID 📙 Beaulieu 3.41

---

* how rows are stored https://ketansingh.me/posts/how-postgres-stores-rows/
* _connection pool_: cache for connections https://en.wikipedia.org/wiki/Connection_pool
* _pool_: group of open connections we keep around for when the app needs them (vs. opening a new one w/ each request or using a single one for each req) 📙 Conery IH 252 https://brettwooldridge.github.io/HikariCP/ https://brandur.org/postgres-connections
* uses TCP/IP as connection protocol
* _at dbms level_: process per connection (Postgres) coroutine per connection (RethinkDB) https://news.ycombinator.com/item?id=12649712
> The PostgreSQL server can handle multiple concurrent connections from clients. To achieve this it starts (“forks”) a new process for each connection. From that point on, the client and the new server process communicate without intervention by the original postgres process. Thus, the master server process is always running, waiting for client connections, whereas client and associated server processes come and go. - https://www.postgresql.org/docs/12/tutorial-arch.html
* _serialization_: query responses typically in binary and parsed by language specific API 📙 Kleppmann 4.128
* _sink_: https://www.usegolang.com/ in Flask https://stackoverflow.com/questions/16311974/connect-to-a-database-in-flask-which-approach-is-better https://flask.palletsprojects.com/en/1.1.x/tutorial/database/ https://github.com/questionlp/api.wwdt.me https://brandur.org/postgres-connections

## indexing

📚
* Bradshaw ch. 5
* Winand
🗄
* internals/explain
* `algos.md` search engine
* `vim.md` ctags

start here
* Postgres has partial indexes
* notes for Karwin chapter 13
> mention of caching? https://hakibenita.com/sql-tricks-application-dba#always-load-sorted-data
* https://calpaterson.com/how-a-sql-database-works.html
* https://dataschool.com/sql-optimization/how-indexing-works/
* BRIN https://hakibenita.com/sql-tricks-application-dba#index-columns-with-high-correlation-using-brin https://www.highgo.ca/2020/06/22/types-of-indexes-in-postgresql/
* https://www.youtube.com/watch?v=HubezKbFL7E
* Beaulieu chapter 13, 15
* Faroult 3
* https://github.com/BurntSushi/xsv
* https://news.ycombinator.com/item?id=32250426

basics
* _index_: binning vs. full table scan 📙 Evans 24
```sql
CREATE INDEX idx_fk_country_id ON city(country_id) -- https://github.com/jOOQ/sakila/blob/main/sqlite-sakila-db/sqlite-sakila-schema.sql
```
* impl: metadata as tree
* subset of data (vs. concordance)
* why: faster reads but slower writes 📙 Kleppmann 71, Karwin 6
> If you need to access data quickly, you index it...that's 90% of what you need to know https://www.bennadel.com/blog/3467-the-not-so-dark-art-of-designing-database-indexes-reflections-from-an-average-software-engineer.htm
* _vacuum_: 📍 https://news.ycombinator.com/item?id=29858083
* _reindex_: 📍 https://news.ycombinator.com/item?id=29858083

types https://www.highgo.ca/2020/06/22/types-of-indexes-in-postgresql/
* _covering_: store additional columns in index https://hakibenita.com/django-32-exciting-features#covering-indexes
> A covering index is when you have an index and it has multiple columns in the index and you’re doing a query on just the first couple of columns in the index and the answer you want is in the remaining columns in the index. When that happens, the database engine can use just the index. It never has to refer to the original table, and that makes things go faster if it only has to look up one thing. https://corecursive.com/066-sqlite-with-richard-hipp/
* _primary_: keeping track of order of entry i.e. having a primary key 📙 Kleppmann 85
* _partial_: normal index + `WHERE` clause https://heap.io/blog/engineering/basic-performance-analysis-saved-us-millions https://hakibenita.com/sql-tricks-application-dba https://dataschool.com/sql-optimization/partial-indexes/ 📙 Bradshaw [5]
* _secondary_: https://calpaterson.com/non-relational-beartraps.html 📙 Kleppmann [85] Bradshaw [5]
* _multicolumn_: aka concatenated 📙 Kleppmann 87 https://dataschool.com/sql-optimization/multicolumn-indexes/

data structures
* _b-tree_: most popular 📙 Kleppmann 83 Winand vii
* sorted keys, pointers to range of keys on disk 📙 Kleppmann 80
* bad for filtering? https://sirupsen.com/napkin/problem-13-filtering-with-inverted-indexes
* diff than hash index bc in memory and updates in place (vs. append-only) 📙 Kleppmann 80
> Several data structures, such as B+Trees, help NoSQL systems quickly retrieve data from disk. Updates to those structures result in updates in random locations in the data structures' files, resulting in several random writes per update if you fsync after each update. http://aosabook.org/en/nosql.html
* _bitmap index_: used for low-cardinality columns https://en.wikipedia.org/wiki/Bitmap_index https://www.youtube.com/watch?v=5imhr4ye3Tw 📙 Kleppmann 97, 561
* semantic confusion? https://en.wikipedia.org/wiki/Bitmap https://github.com/RoaringBitmap/roaring
* bitmap scan https://hakibenita.com/sql-tricks-application-dba#always-load-sorted-data https://spacelift.io/blog/tricking-postgres-into-using-query-plan
* _hash index_: in-mem hash table
* V location in physical storage e.g. append-only log as in Riak Bitcask 📙 Kleppmann 72
* hash table must fit in memory 📙 Kleppmann 75 https://hakibenita.com/postgresql-hash-index
* _SSTable (sorted string)_: hash index but sorted keys 📙 Kleppmann 76
* doesn't need to have all keys in memory 📙 Kleppmann 77
* impl w/ LSM tree 📙 Kleppmann 78
* _LSM tree_: faster for writes 📙 Kleppmann 83
* compress more easily 📙 Kleppmann 84
* used in Cassandra, LevelDB 📙 Kleppmann 79, 85 https://nakabonne.dev/posts/write-tsdb-from-scratch/ 🗄 `algos.md` trees
* _BRIN_: https://hakibenita.com/sql-tricks-application-dba#index-columns-with-high-correlation-using-brin

## internals

parse -> plans -> engine https://pganalyze.com/blog/how-postgres-chooses-index
* _database engine_: container for components https://www.sqlite.org/draft/queryplanner.html https://www.practical-mongodb-aggregations.com/intro/introducing-aggregations.html
* lexer: lex, yac https://news.ycombinator.com/item?id=30086374 https://www.interdb.jp/pg/index.html
* _parser_: https://github.com/reata/sqllineage 🗄 `language.md` compiler
* https://tokern.io/blog/open-source-sql-parsers/
* transpile btw Presto, Hive Spark https://github.com/tobymao/sqlglot
* _query optimizer_: generates query plans, picks execution plan 📙 Beaulieu 3.41 https://news.ycombinator.com/item?id=30855639
* aka querry planner 📙 Bradshaw [167]
> decides which parts of the query to execute in which order and which indexes to use 📙 Kleppmann 37
* cost-based 📙 Kleppmann 427 https://blog.jooq.org/10-cool-sql-optimisations-that-do-not-depend-on-the-cost-model/ https://pghintplan.osdn.jp/pg_hint_plan.html
* ❓ virtual machine https://news.ycombinator.com/item?id=32750676
* _query plan_: output from query optimizer imperative steps to impl declarative SQL https://www.youtube.com/watch?v=IwahVdNboc8 https://dataschool.com/sql-optimization/what-is-a-query-plan/
* _execution plan_: query plan chosen by optimizer 📙 Beaulieu 3.41
> There is a trade-off between the amount of time spent figuring out the best query plan and the quality of the choice https://en.wikipedia.org/wiki/Query_optimization
* _query hint_: explicitly tell optimizer what to do 📙 Beaulieu 3.42 https://en.wikipedia.org/wiki/Hint_(SQL)
* Postgres doesn't support https://wiki.postgresql.org/wiki/Todo
* _query engine_: executes query plan https://en.wikipedia.org/wiki/Presto_(SQL_query_engine) https://news.ycombinator.com/item?id=27006476

explain 🗄 indexing
> In some circumstances, you have knowledge of your data that the optimizer does not have, or cannot have. You might be able to improve the performance of a query by providing additional information to the optimizer https://hakibenita.com/sql-dos-and-donts#add-faux-predicates
* `explain`: view preflight execution plan  https://thoughtbot.com/blog/reading-an-explain-analyze-query-plan https://dataschool.com/sql-optimization/optimization-using-explain/
* adds overhead caused by the Volcano model https://www.ongres.com/blog/explain_analyze_may_be_lying_to_you/
* `explain analyze`: view postflight analysis 📙 Evans 25
* `seq scan`:  query plan doesn't use an index 📙 Evans 25
* aka full table scan https://hakibenita.com/sql-tricks-application-dba#always-load-sorted-data
* making sense of Postgres output https://www.pgmustard.com/docs/explain https://explain.depesz.com/
* more precision yields faster query plan
> The query fetches sales that were modified before 2019. There is no index on this field, so the optimizer generates an execution plan to scan the entire table. Let's say you have another field in this table with the time the sale was created. Since it's not possible for a sale to be modified before it was created, adding a similar condition on the created field won't change the result of the query. However, the optimizer might use this information to generate a better execution plan https://hakibenita.com/sql-dos-and-donts#add-faux-predicates
```diff
FROM sale
WHERE modified < '2019-01-01 asia/tel_aviv'
+ AND created < '2019-01-01 asia/tel_aviv'
```

storage engines
* _journal_: https://fly.io/blog/sqlite-internals-rollback-journal/
* _storage engine_: handle transactions, maintain index https://stackoverflow.com/a/39204302
* row-oriented vs. column-oriented 📙 Kleppmann 586
* log-structured (Riak Bitcask) 📙 Kleppmann 72
* page-oriented 📙 Kleppmann 70 https://sirupsen.com/napkin/problem-6 https://news.ycombinator.com/item?id=32250426
* _Berkeley DB_: https://corecursive.com/066-sqlite-with-richard-hipp/
* _InnoDB_: MySQL; locks table row during transaction
* _MyISAM_: locks whole table https://stackoverflow.com/a/5414622/6813490 
* _WiredTiger_: Mongo 📙 Bradshaw [6]

## logging

* _log_: append-only data file; used to deal w/ concurrency 📙 Kleppmann 71
* _segment_: chunk of log; immutable 📙 Kleppmann 73
* _compaction_: rm dupe keys from log; done by plucking most recent update for key and writing to new, smaller segment file; done in background while continuing to use existing segments for read/write 📙 Kleppmann 73
* fsync log instead of fsyncing data itself to increase throughput? http://aosabook.org/en/nosql.html
> Several data structures, such as B+Trees, help NoSQL systems quickly retrieve data from disk. Updates to those structures result in updates in random locations in the data structures' files, resulting in several random writes per update if you fsync after each update. To reduce random writes, systems such as Cassandra, HBase, Redis, and Riak append update operations to a sequentially-written file called a log. While other data structures used by the system are only periodically fsynced, the log is frequently fsynced. By treating the log as the ground-truth state of the database after a crash, these storage engines are able to turn random updates into sequential ones. While NoSQL systems such as MongoDB perform writes in-place in their data structures, others take logging even further. Cassandra and HBase use a technique borrowed from BigTable of combining their logs and lookup data structures into one log-structured merge tree. Riak provides similar functionality with a log-structured hash table. CouchDB has modified the traditional B+Tree so that all changes to the data structure are appended to the structure on physical storage. These techniques result in improved write throughput, but require a periodic log compaction to keep the log from growing unbounded.

types
* _command log_: log commands to change state but not incremental changes
* _append-only log_: immutability at the db level; conflict w/ GDPR https://www.bloorresearch.com/2018/02/append-databases-gdpr-conundrum/
* _write-ahead log (WAL)_: log changes in state before update so you can recover if failure (power, OS, hw) https://softwareengineeringdaily.com/wp-content/uploads/2018/06/SED613-Database-Reliability-Engineering.pdf
* used in b-tree 📙 Kleppmann 84
* individual entries known as frames https://news.ycombinator.com/item?id=26583558
* turn off if you're just doing a transformation https://hakibenita.com/sql-tricks-application-dba#use-unlogged-tables-for-intermediate-data

# POSTGRES

📜
* general https://www.postgresql.org/docs/current/index.html
* guide http://postgresguide.com/
* wiki https://wiki.postgresql.org/wiki/Main_Page

misc
* local dev https://jamey.thesharps.us/2019/05/29/per-project-postgres/
* chaos https://github.com/lesovsky/noisia
* config https://news.ycombinator.com/item?id=25024224
* cron https://github.com/citusdata/pg_cron
* debug https://iamsafts.com/posts/postgres-gin-performance/
* functions https://blog.jonudell.net/2021/08/05/the-tao-of-unicode-sparklines/
* gotchas https://wiki.postgresql.org/wiki/Don%27t_Do_This https://news.ycombinator.com/item?id=26709019
* internals http://www.interdb.jp/pg/
* typing https://www.postgresql.org/docs/current/datatype.html 🗄 `sql.md` typing
* stored procedures https://www.postgresql.org/docs/current/xplang.html https://dev.nextthought.com/blog/2018/09/getting-started-with-pgsql-plpythonu.html 

semantics
* _cluster_: server instance managing n databases https://www.postgresql.org/docs/12/tutorial-concepts.html
* _foreign data wrapper_: access data from another data store e.g. document store for a relational db
* `json`: text field; slow to search
* JSON schema https://github.com/supabase/pg_jsonschema
* `jsonb`: binary; slower writes, faster reads https://pganalyze.com/blog/postgres-jsonb-django-python
```sql
-- all keys for json obj
select jsonb_object_keys(json_col) from table
-- nested key
select json_col -> 'top_level_key' ->> 'nested_key' from table
```

utils
* generate harmful workloads https://github.com/lesovsky/noisia
* generate test data https://news.ycombinator.com/item?id=26564168 https://hakibenita.com/sql-for-data-analysis#generating-data
* tmp db for testing: https://eradman.com/posts/schema-definition.html https://github.com/eradman/ephemeralpg/ https://stackoverflow.com/questions/14314026/embedded-postgresql-for-java-junit-tests 🗄 `testing.md`
* show view's underlying query `select pg_get_viewdef('my_vw')` https://stackoverflow.com/a/25738887/6813490

---

* _anonymize_: https://postgresql-anonymizer.readthedocs.io/en/latest/
* _audit_: https://github.com/pgaudit/pgaudit https://supabase.com/blog/2022/03/08/audit https://news.ycombinator.com/item?id=30615470
* _backup_: https://github.com/2ndquadrant-it/barman/ https://github.com/ankane/pgsync https://github.com/postgrespro/pg_probackup https://pgbackrest.org/index.html https://github.com/aiven/pghoard https://github.com/orgrim/pg_back https://www.youtube.com/watch?v=kbCytSYPh0E
* _benchmarking_: https://github.com/ankane/pghero https://blog.codeship.com/tuning-postgresql-with-pgbench/
* _diagram_: https://pgmodeler.io/ https://github.com/akarki15/dbdot
* _extensions_: https://news.ycombinator.com/item?id=23821112 https://github.com/zombodb/pgx https://tech.marksblogg.com/postgresql-extension-rust.html distributed https://github.com/citusdata/citus ydb https://news.ycombinator.com/item?id=31081272
* _GUI_: pgadmin https://retool.com/blog/best-postgresql-guis-in-2020/
* _GraphQL_: https://github.com/graphile/postgraphile
* _import_: pgloader https://www.twilio.com/blog/sqlite-postgresql-complicated https://github.com/dimitri/pgloader https://www.youtube.com/watch?v=DA1Trq51JZs https://www.youtube.com/watch?v=yDtgk_OLHUc http://www.postgresqltutorial.com/import-csv-file-into-posgresql-table/ https://stackoverflow.com/questions/2987433/how-to-import-csv-file-data-into-a-postgresql-table/2987451#2987451 https://mattsegal.dev/restore-django-local-database.html https://bigmachine.io/all/importing-a-csv-into-postgresql-like-a-pro/
* _logs_: https://github.com/darold/pgbadger
* _monitoring_: https://minervadb.xyz/postgresql-dba-daily-checklist/ https://pgstats.dev/ https://info.crunchydata.com/blog/postgresql-monitoring-for-application-developers-dba-stats https://klotzandrew.com/blog/quickly-debugging-postgres-problems https://github.com/lesovsky/pgcenter Vivid Cortex https://github.com/lob/pg_insights https://github.com/cybertec-postgresql/pgwatch2 https://github.com/cybertec-postgresql/pgwatch2 https://pganalyze.com/ https://github.com/dalibo/temboard
* _queries_: https://news.ycombinator.com/item?id=22432254 explain http://www.helenanderson.co.nz/sql-query-tweaks/ `pg_stat_statements` https://pgdash.io/blog/postgres-features.html https://github.com/mgartner/pg_flame
* _search_: https://czep.net/17/full-text-search.html https://www.imagescape.com/blog/2020/03/11/website-search-using-django-and-postgresql-trigrams 🗄 `algos.md` FTS
* _scheduling_: https://github.com/cybertec-postgresql/pg_timetable

how to
* get date from timestamp: `SELECT date(startime) FROM bookings` https://stackoverflow.com/a/6133147
* fuzzy match https://news.ycombinator.com/item?id=26236772

## auth

* _role_: Postgres equivalent of a user, necessary to connect 📙 Conery [4.5] https://www.postgresql.org/docs/8.1/user-manag.html
* _role creation_: PG will create role/db matching Linux user that installed PG; sometimes this doesn't happen w/ Homebrew 📙 Conery 4.4 0:15
* _list roles_: `\du`
* _connection string_: `postgresql://user:pass@host:port/db` https://testdriven.io/blog/dockerizing-flask-with-postgres-gunicorn-and-nginx/#docker https://flask-sqlalchemy.palletsprojects.com/en/2.x/config/#connection-uri-format
* _pure authentication_: Linux user matching PG role can log into that role 📙 Conery 4.3 2:30
* login
```sh
# same syntax for both pgcli and psql
# defaults to user/role and db matching Linux user name https://www.postgresql.org/docs/12/tutorial-accessdb.html
psql -d <db> -U <user>
$ whoami  # alice
$ pgcli  # role (alice) db (alice)
```

---

install
```sh
# as root
$ apt-get install postgresql postgresql-client postgresql-contrib

# shows that psql and CLI work, both should fail w/ error that Postgres doesn't have user named root
$ psql
$ createdb

# only role in db in `postgres`
# installing PG also creates os user of `postgres`
# idky switching to `postgres` also switches directory to `/root`
$ su postgres
$ createdb scifi
$ psql scifi
```

* macos installation and start https://www.postgresql.org/docs/12/installation-platform-notes.html#INSTALLATION-NOTES-MACOS https://postgresapp.com/ https://stackoverflow.com/a/18832331 🗄 `brew/postgres*.log`
```sh
# start manually
pg_ctl -D /usr/local/var/postgres start
# start on os startup w/ Homebrew
brew services start postgresql
```

* Docker image: roles only set during initializatio https://hub.docker.com/_/postgres if you update auth credentials `docker-compose down -v` might not be enough, may need to rm image as well https://stackoverflow.com/q/53820456 https://github.com/docker-library/postgres/issues/537
```sh
# debug cmd
docker-compose exec <service> env # env var ingested?
docker-compose exec <service> psql -U <user> # can you log in?
```
```yaml
services:
  db:
    image: "postgres:11"  # which image to use; unlike 'web', we're not building this one ourselves
    command: ["postgres", "-c", "log_statement=all", "-c", "log_destination=stderr"]  # logs https://stackoverflow.com/a/59313245
    environment:
      - POSTGRES_HOST  # defaults to service name i.e. 'db' https://www.youtube.com/watch?v=A9bA5HpOk30 6:50 can set manually as well https://stackoverflow.com/a/52543774
      - POSTGRES_DB=zjv_db
      - POSTGRES_USER=zjv_user  # creates role https://stackoverflow.com/q/46669759
      - POSTGRES_PASSWORD=zjv_pw  # cannot be empty or undefined
      - POSTGRES_HOST_AUTH_METHOD=trust  # allow connections w/out password https://learndjango.com/tutorials/django-docker-and-postgresql-tutorial
    volumes:  # create dir in WORKDIR (pg_data) and map to where PG stores data https://www.youtube.com/watch?v=A9bA5HpOk30 2:30
      - pg_data:/var/lib/postgresql/data/  # or does this create file in CWD on local machine? https://www.youtube.com/watch?v=A9bA5HpOk30 9:25

volumes:  # yj
  pg_data:
```

* app tier ingestion of env
```conf
# Flask
DB_USER=zjv_user
DB_PW=zjv_pw
DB_NAME=zjv_db
```
```python
# Django https://docs.djangoproject.com/en/3.1/ref/settings/#databases
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'HOST': 'db',
        'PORT': 5432,  # docker images defaults to 5432 so we don't need to specify in docker-compose.yml
        'NAME': 'postgres',
        'USER': 'postgres',
        'PASSWORD': 'postgres',
    }
}
# Flask
user = os.getenv("DB_USER")
pw = os.getenv("DB_PW")
name = os.getenv("DB_NAME")
app.config["SQLALCHEMY_DATABASE_URI"] = f"postgresql://{user}:{pw}@db:5432/{name}"
```

## CLI

cmd
* Postgres specific cmd: `\h`


---

* _change output_: `\pset`
* _set var_: `\set`

psql https://tomcam.github.io/postgres/ https://mydbanotebook.org/psql_tips_all.html
* conf: `.psqlrc` https://www.digitalocean.com/community/tutorials/how-to-customize-the-postgresql-prompt-with-psqlrc-on-ubuntu-14-04 https://robots.thoughtbot.com/improving-the-command-line-postgres-experience https://robots.thoughtbot.com/an-explained-psqlrc
* connect: `-d <db> -U <user> -h <host> -p <port>`; defaults (user=root, host=localhost, port=5432) https://startcodingnow.com/psql-in-docker-compose/
* connect after login: `\c <db>`
* connection info: `\conninfo`
* https://stackoverflow.com/questions/41591386/postgresql-column-does-not-exist-but-it-actually-does

CLI util (psql, postgres, pg_dump, createdb/dropdb) https://gist.github.com/apolloclark/ea5466d5929e63043dcf
* _postgresql-client_: CLI for backups
* create: `createdb <db>` (if 0 doesn't write to stdout) https://www.postgresql.org/docs/12/tutorial-createdb.html comes w/ PG installation https://www.postgresql.org/docs/12/tutorial-createdb.html
* rm: `dropdb <db>`
* dump: `pg_dump <db> > <file>` https://www.postgresql.org/docs/11/backup-dump.html
* load: `psql -f <file>`; https://www.postgresql.org/docs/11/backup-dump.html#BACKUP-DUMP-RESTORE might need to create db beforehand (idk if way to dump such that db automatically created on load, also don't know if safer to use `-d <db>` to ensure loaded to correct db but `verbos` db worked without it) https://raw.githubusercontent.com/ghidinelli/fred-jehle-spanish-verbs/master/jehle_verb_postgresql.sql
* start/status: `pg_ctl`
* version: `postgres -V`

## psycopg

* _driver_: lib for (db) connection https://stackoverflow.com/a/8588766 
* _psycopg_: Python driver for Posgres
* impl https://www.varrazzo.com/blog/2020/03/06/thinking-psycopg3/
* _psycopg2_: uninstallable w/ Poetry even w/ Brew install of Postgres https://realpython.com/flask-by-example-part-2-postgres-sqlalchemy-and-alembic/
* _psycopg2-binary_: installable w/ Poetry, problem with pipenv https://github.com/pypa/pipenv/issues/4073
* reasons for split https://github.com/psycopg/psycopg2/issues/674
* seems like people just use psycopg2-binary instead of psycopg2 http://www.dark-hamster.com/programming/how-to-solve-error-on-installing-psycopg2-using-pip-by-using-psycopg2-binary-instead/ https://gitlab.com/mailman/mailman/commit/3b2a3e199601961b8b195d4a7713e170ce6f9935
* erred out w/ `python:3-alpine` even with installing `psycopg2-binary` as separate dep https://stackoverflow.com/q/60461406
```log
Collecting psycopg2-binary==2.8.5
  Downloading psycopg2-binary-2.8.5.tar.gz (381 kB)
    Error: pg_config executable not found.
    pg_config is required to build psycopg2 from source.
    If you prefer to avoid building psycopg2 from source, please install the PyPI
    'psycopg2-binary' package instead.
```
* worked with new image and installing psycopg2-binary as separate dep in Dockerfile https://github.com/psycopg/psycopg2/issues/684#issuecomment-538423955
```diff
- FROM python:3-alpine
+ FROM python:3.6-slim
+ RUN pip install psycopg2-binary
```
* SQLAlchemy seems to have psycopg as sub dep, but still need to install as standalone https://learndjango.com/tutorials/django-docker-and-postgresql-tutorial
```ini
[[package]]
name = "sqlalchemy"

[package.extras]
postgresql = ["psycopg2"]
postgresql_psycopg2binary = ["psycopg2-binary"]
```
```log
web_1  | 172.18.0.1 - - [25/Jun/2020 18:54:01] "GET /healthcheck HTTP/1.1" 200 -
web_1  | [2020-06-25 18:54:13,597] ERROR in app: Exception on /get-things [GET]
web_1  | Traceback (most recent call last):
web_1  |   File "/usr/local/lib/python3.8/site-packages/sqlalchemy/util/_collections.py", line 1020, in __call__
web_1  | During handling of the above exception, another exception occurred:
web_1  | Traceback (most recent call last):
web_1  |     import psycopg2
web_1  | ModuleNotFoundError: No module named 'psycopg2'
```

# SQLITE

📜 https://sqlite.org/docs.html
🛠 https://github.com/simonw/sqlite-utils
🔗 https://tech.marksblogg.com/sqlite3-tutorial-and-guide.html

misc
* _APSW_: alternative to Python's sqlite3 https://github.com/litements/s3sqlite
* db file extension incl. `.db` and `.sqlite` https://www.visidata.org/ https://sqlite.org/fileformat.html
* can do blob https://stackoverflow.com/q/29008721/6813490 https://www.youtube.com/watch?v=TLgVEBuQURA
* GUI: https://sqlitebrowser.org/ https://github.com/pawelsalawa/sqlitestudio
* backups https://github.com/benbjohnson/litestream https://litestream.io/alternatives/cron/ https://news.ycombinator.com/item?id=31152490 https://news.ycombinator.com/item?id=31318708

howto
* config (journal, wal, timeout) https://unixsheikh.com/articles/sqlite-the-only-database-you-will-ever-need-in-most-cases.html https://avi.im/blag/2021/fast-sqlite-inserts/
* migrations: https://news.ycombinator.com/item?id=22367104
* perf https://news.ycombinator.com/item?id=26103776
* diff databases https://news.ycombinator.com/item?id=31256704
* corrupt a database https://news.ycombinator.com/item?id=31214131

## CLI

📜 https://sqlite.org/cli.html

commnands
```sh
# open /  close
sqlite3 / .quit
# create empty
sqlite3 <name.db>
# open / reload https://github.com/dbcli/litecli/issues/76
.open <file>

# show file
l
# list db
.da  # .databases (litecli)
# list tables
.tables
# describe schema
.schema <table>

# columns and headers https://sqlite.org/cli.html#changing_output_formats https://dba.stackexchange.com/a/40672
.mode column  # will override `.mode csv`
.headers on
.width  # https://dba.stackexchange.com/a/40672

# query CSV https://news.ycombinator.com/item?id=28299729
.mode csv
.import my.csv <alias>
select * from alias
```

za
* config location: `~/.sqliterc`
* cmd history: `~/.sqlite_history`
* archives https://unixsheikh.com/articles/sqlite-the-only-database-you-will-ever-need-in-most-cases.html
```sh
# dump
sqlite3 my_database .dump | gzip -c > my_database.dump.gz
# restore
cat my_database.dump.gz | sqlite3 my_database
```

---

config
* default file location: pgcli(`~/.config/litecli/config`) sqlite()
* specify config file: `litecli --liteclirc <conf> <db_file>` 🗄 `query-sandbox`

db files
* create db file from script: interactive `sqlite3; .read seed.sql` https://sqlite.org/cli.html#special_commands_to_sqlite3_dot_commands_ interactive `sqlite3 test.db < test_schema.sql` https://stackoverflow.com/q/42245816/6813490 http://flask.pocoo.org/docs/0.12/tutorial/dbinit/#tutorial-dbinit

## design

📜 https://sqlite.org/quirks.html

components
* _SQLite_: library https://tech.marksblogg.com/sqlite3-tutorial-and-guide.html
* Go port https://simonwillison.net/2022/Jan/30/a-cgo-free-port-of-sqlite/
* plumbing https://jvns.ca/blog/2014/09/27/how-does-sqlite-work-part-1-pages/ https://jvns.ca/blog/2014/10/02/how-does-sqlite-work-part-2-btrees/
* _sqlite3_: CLI
* sqlite3: Python driver https://github.com/zachvalenta/sqlite3-demo https://github.com/zachvalenta/bookcase-sjk https://sebastianraschka.com/Articles/2014_sqlite_in_python_tutorial.html

strong points https://unixsheikh.com/articles/sqlite-the-only-database-you-will-ever-need-in-most-cases.html
* dbms in a C library
* ACID-compliant
* multithreaded https://sqlite.org/threadsafe.html
* reads parallelized 
* writes concurrent
> This means that writers queue up. Each application does its database work quickly and moves on, and no lock lasts for more than a few milliseconds
* file-based/serverless = good for unreliable network (smartphone, airplane)
* db files can deal w/ TB https://news.ycombinator.com/item?id=24178013

limitations
* files https://news.ycombinator.com/item?id=32146245
* schema changes require downtime, PRAGMA https://news.ycombinator.com/item?id=31152490
* doesn't support right join or full outer join https://sqlite.org/omitted.html added for 3.9 https://sqlite.org/releaselog/3_39_0.html
* only support single user 📙 Osborn 6.33 https://news.ycombinator.com/item?id=31152490
* data types differ from other dbms, problem for porting?
* no perms, security 📙 Takahashi 1.19 no users 📙 ibid 1.20

extensions
* fewer functions than other dbms
* get more via extension https://github.com/nalgeon/sqleans
* _FTS4_: extension for search https://simonwillison.net/2019/Jan/7/exploring-search-relevance-algorithms-sqlite/ 🗄 `algos.md` FTS
* bundled https://github.com/nalgeon/sqlean
* JSON https://dba.stackexchange.com/questions/122198/is-it-possible-to-store-and-query-json-in-sqlite https://news.ycombinator.com/item?id=30486052

types
* types: text, blob, null, int (whole num) real (decimal)
* _class_: type for cell https://stackoverflow.com/a/3388158
* _affinity_: type for attr
> The type affinity of a column is the recommended type for data stored in that column. The important idea here is that the type is recommended, not required. Any column can still store any type of data. It is just that some columns, given the choice, will prefer to use one storage class over another. The preferred storage class for a column is called its "affinity". - https://www.sqlite.org/datatype3.html#type_affinity
* _manifest typing_: type information scoped to cell instead of column (as in most other dbms)
* dynamic vs. static https://www.sqlite.org/datatype3.html https://unixsheikh.com/articles/sqlite-the-only-database-you-will-ever-need-in-most-cases.html
* can ️lead to problems when porting to other DBMS
* avoid type conversion https://news.ycombinator.com/item?id=28259104
```sql
CREATE TABLE tIssue (
    id   INTEGER PRIMARY KEY NOT NULL CHECK (typeof(id) = 'integer'),
    col1 BLOB NOT NULL                CHECK (typeof(col1) = 'blob'),
    col2 TEXT                         CHECK (typeof(col2) = 'text' OR col2 IS NULL)
);
```

constraints
* _PK_: `integer primary key` will autoincrement https://stackoverflow.com/a/8519985/6813490
* just points to `rowid` https://stackoverflow.com/a/7906029/6813490
* typically don't need `autoincrement` https://sqlite.org/autoinc.html https://unixsheikh.com/articles/sqlite-the-only-database-you-will-ever-need-in-most-cases.html
* `rowid`: default attr on all tables https://www.sqlite.org/rowidtable.html https://sqlite.org/withoutrowid.html
* _FK_: `pragma foreign_keys = on;`; have to turn on each time you connect https://sqlite.org/foreignkeys.html https://stackoverflow.com/a/9937992/6813490 🗄 `bookcase`
* FK w/ SQLAlchemy: w/ Flask https://fastapi.tiangolo.com/tutorial/sql-databases/ https://www.youtube.com/watch?v=lnfrcHdE_HI https://stackoverflow.com/questions/38792722/flask-foreign-key-constraint https://stackoverflow.com/questions/2614984/sqlite-sqlalchemy-how-to-enforce-foreign-keys have access to engine http://flask-sqlalchemy.palletsprojects.com/en/2.x/quickstart/#road-to-enlightenment
> rn Flask-SQLA will happily violate FK or just leave null 
* `pragma`: cmd to set env var

# ZA

dbms taxnomy https://nchammas.com/writing/database-access-patterns
* data structures e.g. relational, document
* scale e.g. single node, distributed
* storage e.g. relational, column store
* consistency guarantee
* transaction isolation
* _temporality_: real-time vs. historical 📻 Macey 8:30

types of data
* _dataset_: actual data (vs. schema) https://pgexercises.com/gettingstarted.html
* _dummy data_: fake/seed data for development; https://github.com/zachvalenta/flask-CRUD/blob/master/db_seed.py https://github.com/joke2k/faker#providers https://mimesis.name/ https://mockaroo.com/ https://github.com/Qovery/replibyte
* _synthetic data_: real data but anonymized https://softwareengineeringdaily.com/2021/02/16/synthetic-data-with-ian-coe-andrew-colombi-and-adam-kamor/ https://gretel.ai/blog/what-is-synthetic-data

scaling
* _vertical_: get faster drives for db
> I am always puzzled about this "autoscale" thing on a cloud. If your task can be represented as something like calculate sum of some ginormous array then sure. Split array in parts and launch thousand instances each working on it's own slice and then combine. In way more common situation you have a service hitting database and doing something with it. Sure you can spin a thousand instances of said service. But they will all be hitting the same database. - https://news.ycombinator.com/item?id=21741870
* _horizontal_; shard; until recently you waited as long as you could on this 📙 Kleppmann 1.18
> horizontal-scaling is often based on the partitioning of the data i.e. each node contains only part of the data, in vertical-scaling the data resides on a single node and scaling is done through multi-core i.e. spreading the load between the CPU and RAM resources of that machine. With horizontal-scaling it is often easier to scale dynamically by adding more machines into the existing pool - Vertical-scaling is often limited to the capacity of a single machine, scaling beyond that capacity often involves downtime and comes with an upper limit. - https://stackoverflow.com/a/11715598/6813490

security
* read-only access https://pgexercises.com/about.html
* `statement_timeout` to prevent long-running queries https://pgexercises.com/about.html https://www.postgresql.org/docs/13/runtime-config-client.html
* clear settings from connection after each statement https://pgexercises.com/about.html https://www.pgbouncer.org/
* _row-level_: limit user to specific rows https://pganalyze.com/blog/postgres-row-level-security-django-python https://news.ycombinator.com/item?id=30700899
* StrongDM records remote access sessions https://softwareengineeringdaily.com/2019/07/23/data-engineering-with-tobias-macey/

timezones
* client sould specify their timezone before querying https://hakibenita.com/sql-dos-and-donts#be-aware-of-timezones
* relational has problems w/ this https://increment.com/software-architecture/architecture-for-generations/ https://en.wikipedia.org/wiki/Temporal_database#Example https://retool.com/blog/formatting-and-dealing-with-dates-in-sql/

async
* Django: not yet supported https://docs.djangoproject.com/en/3.2/topics/async/
* Encode `databases`; adds async to SQLAlchemy https://www.encode.io/databases/database_queries/ https://fastapi.tiangolo.com/advanced/async-sql-databases/
* Postgres: can use async functions that underly synchronous `PQexec` https://www.postgresql.org/docs/9.5/libpq-async.html

## dbcli

📜
* https://litecli.com/
* https://www.pgcli.com

cmd
* help: `\?`
* clear screen: `ctrl l`
* autocomplete: `ctrl e`
* list tables: `\dt`
* set pager to bat: `pager = less -SRXF` https://www.pgcli.com/docs
* open with env var: `cli -h`
* autocomplete: `ctrl e`
* clear screen: `ctrl l`
* exit: `exit`, `\q`
* _metacommand_: preceded w/ backslash https://www.pgcli.com/commands

named queries
* 📍 open PR: print query on usage (less_chatty?)
* _named query_: snippet, saved query https://www.pgcli.com/named_queries.md
* syntax: `f` (litecli) `n` (pgcli)
* list: `\f` https://github.com/dbcli/pgcli/issues/1236
* save: `\fs <name> <query>` https://github.com/dbcli/pgcli/issues/938
* save w/ param: `\fs <name> <query where foo = $1>` https://github.com/dbcli/pgcli/issues/938
> broken in sandbox: could be pager, Python version, config (try default config installed in $HOME) https://github.com/dbcli/pgcli/search?q=codec&type=issues
* use: `\f <name>`
* use w/ param: `\f <name> "arg"`
* rm: `\fd <name>` https://litecli.com/favorites/

## DBMS

MySQL
* MariaDB is dead https://news.ycombinator.com/item?id=27922687
* _CLI_: https://www.mycli.net/docs flags https://dev.mysql.com/doc/refman/8.0/en/mysql-command-options.html
* _GUI_: https://sequelpro.com/
* _check constraint_: no suppport previously https://www.youtube.com/watch?v=lnfrcHdE_HI 4:45 https://dev.mysql.com/doc/refman/8.0/en/create-table-check-constraints.html
* _db - current_: `select database();`
* _db - list_: `show databases;`
* _db - use_: `use <name>;`
* _db - create_: common
* _table - list_: `show tables;`
* _table - rm_: common
* _table - update col_: common
* version: `mysql -V`
* login: `mysql -h <host> -u <user> -p`
* exit: `exit;`
* clear screen: `CMD k` (iTerm) `CMD ALT l` (Terminal)
* cmd from shell: `mysql -u <user> -e <cmd>`
* run script: ` mysql -u <user> <dbname> < script.sql`
* dump - local: `mysqldump -u <user> <db> > backup.sql` https://github.com/zachvalenta/flyway-tutorial/blob/master/db-backup.sh
* dump - remote: `mysqldump -h <host> -u <user> --single-transaction -p <db> > backup.sql` https://github.com/zachvalenta/flyway-tutorial/blob/master/db-restore.sh
* load: `mysql -u <user> -e "DROP DATABASE IF EXISTS <db>; CREATE DATABASE <db>;` -> `mysql -u <user> <db> < backup.sql`

Oracle
* apparently still much more feature rich than Postgres https://news.ycombinator.com/item?id=24582937
* _CLI_: seems like you need an account and the docs are shoddy https://dba.stackexchange.com/questions/65032/connect-to-sql-plus-from-command-line-using-connection-string but maybe this will work https://github.com/xo/usql
* _GUI_: SQL Developer; comment `CMD ALT /` exec `CTRL /`
* _account_: same as work / phone 123456789 / ABC Corp 100 Commerce Blvd Orlando FL 32801
* Oracle dev https://stackoverflow.com/users/146325/apc
* _Sybase_: SAP counterpart

za
* BYO https://github.com/weinberg/SQLToy https://news.ycombinator.com/item?id=26811279 https://github.com/joaoh82/rust_sqlite https://github.com/auxten/go-sqldb https://github.com/erikgrinaker/toydb/blob/master/docs/references.md?utm_source=pocket_mylist
* compare queries across different dbms https://github.com/rickbergfalk/sqlpad
* _embedded_: https://en.wikipedia.org/wiki/List_of_in-memory_databases https://www.openmymind.net/2011/2/10/Do-Relational-Database-Vendors-Care-About-Devs/
* _client-server_: when you have multiple clients (vs. multithreaded) or need thousands of writes/second https://unixsheikh.com/articles/sqlite-the-only-database-you-will-ever-need-in-most-cases.html

## utils

🗄
* `sql.md` pedagogy/dataclerk
* Mongo / workflows

workflows
* exploration: Visidata
* entry: dataclerk
* query: CLI (narrow rs) GUI (wide rs)

| GUIs       | type              | cost | OSS |  notes                                                                          |
|------------|-------------------|------|-----|---------------------------------------------------------------------------------|
| DBeaver    | relational        | 0    | y   | ERD https://stackoverflow.com/a/48397209                                        |
| UltOrg     | relational        | ?    | n   | https://www.hytradboi.com/2022/ultorg-a-user-interface-for-relational-databases |
| DbGate     | relational, NoSQL | 0    | y   | https://github.com/dbgate/dbgate                                                |
| pgAdmin    | Postgres          | 0    | y   |                                                                                 |
| DB4S       | SQLite            | 0    | y   | https://github.com/sqlitebrowser/sqlitebrowser                                  |
| Table Plus | relational, NoSQL | 100  | n   | https://news.ycombinator.com/item?id=22908224                                   |
| BeeKeeper  | relational        | 120  | n   |                                                                                 |

GUI features
* query editor
* ERD
* queryless joins https://www.hytradboi.com/2022/ultorg-a-user-interface-for-relational-databases
* follow FKs https://github.com/Wisser/Jailer

API / code generation
* Postgrest https://github.com/PostgREST/postgrest https://news.ycombinator.com/item?id=30132947
* query SQLite over HTTP https://news.ycombinator.com/item?id=30636796
* ROAPI https://github.com/roapi/roapi https://tech.marksblogg.com/roapi-rust-data-api.html
* Datasette https://www.youtube.com/watch?v=pTr1uLQTJNE
* DBCore https://github.com/eatonphil/dbcore https://notes.eatonphil.com/generating-a-rest-api-from-a-database.html
* Octo https://github.com/octoproject/octo-cli

backup
* _dump_: "create a script that would allow me to recreate this db"
* _load_: "use script to create db"
* data version control https://softwareengineeringdaily.com/2020/08/24/data-version-control-with-dmitry-petrov/ https://news.ycombinator.com/item?id=22731928 https://terminusdb.com/  https://news.ycombinator.com/item?id=24071955 https://realpython.com/python-data-version-control/ https://github.com/iterative/dvc https://github.com/dolthub/dolt
* https://serversforhackers.com/s/backup-and-recovery https://www.pgbarman.org/index.html Backblaze https://news.ycombinator.com/item?id=26426489

conversion / generation
* https://hakibenita.com/sql-for-data-analysis#generating-data
* import from 3rd party: Dogsheep https://datasette.substack.com/p/dogsheep-personal-analytics-with
* Visidata
* Posgres https://news.ycombinator.com/item?id=24189582
* https://github.com/simonw/sqlite-utils
```sh
# https://simonwillison.net/2020/Nov/14/personal-data-warehouses/ 20:25
curl www.api.com | jq foo | sqlite-utils insert foo.db bar_table
```

linting
* https://github.com/alanmcruickshank/sqlfluff https://www.thoughtworks.com/radar/tools?blipid=202203065
* https://www.eversql.com/sql-syntax-check-validator/
* https://github.com/purcell/sqlint
* https://github.com/darold/pgFormatter
* https://sqlfum.pt/

perf
* https://github.com/ankane/pghero
* https://klotzandrew.com/blog/quickly-debugging-postgres-problems
* QPS (queries per second) https://www.youtube.com/watch?v=kEShMV4VfWE
* https://stackoverflow.com/a/11275107/6813490/ 
* https://numeracy.co/blog/life-of-a-sql-query
* https://www.digitalocean.com/community/tutorials/how-to-use-mysql-query-profiling
