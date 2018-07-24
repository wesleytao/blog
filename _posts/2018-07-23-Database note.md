
# 01-01-introduction
## key concepts
* Data model
	* set of records, XML,graph
* Schema versus data
* Data definition language
	set up schema
* Data manipulation or query language 
  for querying and modifying 

<iframe src="https://onedrive.live.com/embed?cid=7A4009AE5855F5B2&amp;resid=7A4009AE5855F5B2%2110980&amp;authkey=ABln01F7kWm1la0&amp;em=2&amp;wdAr=1.7777777777777777" width="1186px" height="691px" frameborder="0">this is embeded <a target="_blank" href="https://office.com">Microsoft Office</a> ppt<a target="_blank" href="https://office.com/webapps">Office Online</a> supported</iframe>

## key people
* DBMS implementer
 builds system
* Database desinger
establishes schema
* Database application developer
programs that operate on database: sales database insert/delete
* Database administrator
loads the data,keep running smoothly 
tunning paramer to get better performance
highly paid

# 02-02-relational-model
used by all major commercial database systems
very simple model 
query with high-level-languages: simple yet expensive
efficient implementations

# relation database
* NULL - special value for 'unknown" or "undefined"
* key -attribute whose value is unique in each tuple

# Querying Relational Database
steps:
1.Design schema;create using DDL
2.'Bulk load' initial data
3. Repeat: execute queries and modifications

# ad-hoc queries in high-level language
# Query languages
* relational algebra - formal
* SQL - actual/implemented

# XML Data 
* Introduction,well-informed XML(extensible markup language)
* well-formed XML
adheres to basic structural requirements
* single root element
* matched tags, proper nesting
* unique attributes within elements
XML parser(not well-formed)

Document Type Descriptor(DTD)
* grammar-like lauguage 
* special attributes types ID and IDREF(S)  pointer untyped

DTD/XSD 
pros: 
* Programs can assume structure
* CSS/XSL
* specification - data exchange 
* documentation 
* benefits of "typing"

cons:
* flexibility, ease of change
* DTDs can be messy -- irregular 
* XSDs 
* benefits of "no typing"

