# OpenUIModel

OpenUIModel is a description format for describing the content of CRUD user interfaces.

It is designed to give an implementation neutral description of the entities and attributes that can be created and changed over a User Interface.

Draft v0.0.1-SNAPSHOT:

```properties EBNF
model = [name], [version], entities

entities = entity, {entity}

entity = id, name, pluralName, attributes, relationOnly, [overviewComponent], [detailViewComponent]

attributes = (attribute | attributeGroup), {attributes}

# id of an entity, attribute, attributeGroup
# Must be unique among it's group (entity, attribute, attributeGroup)
id = String

# name of an entity, attribute, attributeGroup
# Must be unique among it's group (entity, attribute, attributeGroup)
name = String

# depending on name
# default is an 's' attached at the end or 'ies' when name ends with 'y' 
pluralName = String

relationOnly = Boolean

# name of the component to be rendered for the overview
overviewComponent = String

# name of the component to be rendered for the detail view
detailViewComponent = String

attribute = id, name, pluralName, type, optional, multiple, rendering, [validation], [relatedEntity]

type = "String" | "Numeric" | "Boolean" | customAttributeType

# any type supported by the rendering implementation
customAttributeType = String

optional = Boolean

multiple = Boolean

rendering = (overview, detail | overview | detail), [component]

attributeGroup = id, name, pluralName, optional, multiple, attributes

validation = (min | max | min, max) | regex | enum | length

min = Numeric

max = Numeric

enum = String, {String}

length = Integer

relatedEntity = id (used in an entity), displayAttribute, assignmentAttribute

displayAttribute = name (used in the related entity attributes)

assignmentAttribute = name (used in the related entity attributes)

```

JSON example:

```json 
{
  "name": "Shop",
  "version": "1.0",
  "entities": [
    {
      "id": "e1",
      "name": "Category",
      "attributes": [
        {
          "name": "Category Name",
          "id": "a1",
          "type": "String",
          "optional": false
        },
        {
          "name": "Tag",
          "id": "a2",
          "type": "String",
          "optional": true,
          "multiple": true
        }
      ]
    },
    {
      "id": "e2",
      "name": "Item",
      "attributes": [
        {
          "id": "a3",
          "name": "Attribute Name",
          "type": "String",
          "validation": {
            "length": 255
          },
          "optional": false
        },
        {
          "id": "a4",
          "name": "Description",
          "type": "String",
          "optional": false
        },
        {
          "id": "a5",
          "name": "Items in Stock",
          "type": "Integer",
          "validation": {
            "min": 0,
            "max": 999999
          },
          "optional": false
        },
        {
          "id": "a6",
          "name": "Price (netto)",
          "type": "Decimal",
          "optional": false
        },
        {
          // Attribute Group
          // Repeating pairs of Properties as Name-Value pairs
          "id": "ag1",
          "name": "Property",
          "multiple": true,
          "optional": true,
          "attributes": [
            {
              "id": "a7",
              "name": "Property Name",
              "type": "7String",
              "validation": {
                "length": 255
              },
              "optional": false
            },
            {
              "id": "a8",
              "name": "Property Value",
              "type": "String",
              "validation": {
                "length": 255
              },
              "optional": false
            }
          ]
        }
      ]
    }
  ]
}
```
