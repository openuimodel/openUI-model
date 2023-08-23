# OpenUIModel

OpenUIModel is a description format for describing the content of CRUD user interfaces.

It is designed to give a implementation neutral description of the entities and attributes that can be created and changed over a User Interface.

Draft v0.0.1-SNAPSHOT:

```properties EBNF
model = [name], entities

entities = entity, {entity}

entity = name, id, attributes, attributes, relationOnly, [overviewComponent], [detailViewComponent];

attributes = (attribute | attributeGroup | attributes), {attribute}, {attributeGroup};

# name of an entity, attribute, attributeGroup
# Must be unique among it's group (entity, attribute, attributeGroup)
name = String

# id of an entity, attribute, attributeGroup
# Must be unique among it's group (entity, attribute, attributeGroup)
id = String

relationOnly = Boolean

# name of the component to be rendered for the overview
overviewComponent = String

# name of the component to be rendered for the detail view
detailViewComponent = String

attribute = name, id, type, optional, multiple, rendering, [validation], [relatedEntity]

type = "String" | "Numeric" | "Boolean" | customAttributeType

# any type supported by the rendering implementation
customAttributeType = String

optional = Boolean

multiple = Boolean

rendering = (overview, detail | overview | detail), [component]

attributeGroup = name, id, attributes

validation = (min | max | min, max) | regex | enum | length

min = Numeric

max = Numeric

enum = String, {String}

length = Integer

relatedEntity = id (used in an entity), displayAttribute, assignmentAttribute

displayAttribute = name (used in the related entity attributes)

assignmentAttribute = name (used in the related entity attributes)
 
```
