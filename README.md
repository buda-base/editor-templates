# SHACL Shapes Templates for the BUDA editor

The shacl shapes express validation and UI information for the various Entities that are the focus of the BUDA platform:

- Bibliographic items - bdo:Works, bdo:Instances, bdo:Items
- bdo:Persons
- bdo:Places
- bdo:Topics
- bdo:Roles
- bdo:Lineages
- bdo:Corporations

These are the resources that are subjects of editing. The shapes information for these Entities are organized into shapes graphs for each class of Entity, and for each class there are three graphs: 

- the _top_ graph validates references from the focus Entity graph to other Entities, e.g., where a `bdo:Work` was published or the father of a `bdo:Person`. The _top_ graph includes the _local_ graph.
- the _ui_ graph contains information that supports the UI for the editing client, e.g., the order in which names, gender, birth/death events, student/teacher relationships should be presented on the UI and names and descriptions and so on. The _ui_ graph includes the _top_ and _local_ graphs

The naming convention for the two sorts of shape graphs is _classname_**Shapes**, and _classname_**UIShapes**. _Top_ is not used in the naming and is understood in the _classname_**Shapes** form, that contains the full set of constraints for validating instances of classname.

There are a variety of supporting resources that may be associated with all, many, or some Entity classes:

- bdo:Note
- bdo:Label
- bdo:ContentLocation
- bdo:Event

The shapes associated with these are organized as above and imported as needed by the three types of shapes graphs for each Entity. The shapes for resources common to most or all Entities are contained in RootShapes, and RootUIShapes.

There is a `BaseShapes` graph that contains definitions of shapes and ancillary properties and classes that support the definitions used in shapes for Entites and other resources. Among the properties defined in `BaseShapes` are `bds:topShapeGraph`, and `bds:uiShapeGraph`. These connect an Entity class to the corresponding shapes graphs for the class:
```
bdo:Person 
    bds:topShapeGraph   bdg:PersonShapes ;
    bds:uiShapeGraph    bdg:PersonUIShapes .
```

The various shapes modules (shacl ontologies) are indicated in the `ont-policy.rdf` and the pattern of importing is illustrated below for the `bdo:Person` Entity:
```
PersonUIShapes
    PersonShapes
    EventUIShapes
    
PersonShapes    
    EventShapes

PersonLocalShapes
    EventLocalShapes

EventUIShapes
    EventShapes
    RootUIShapes

EventShapes
    RootShapes

RootUIShapes
    RootShapes

RootShapes
    BaseShapes

BaseShapes
```

## Prior work

- https://www.w3.org/TR/shacl/
- http://datashapes.org/
- http://datashapes.org/forms.html
- http://datashapes.org/constraints.html
- http://datashapes.org/dash.html
- http://datashapes.org/reification.html
- http://datashapes.org/templates.html#references
- https://uispin.org/index.html
- https://uispin.org/ui.html
- https://spinrdf.org/
- https://spinrdf.org/shacl-and-owl.html
- https://spinrdf.org/spin-shacl.html
- https://www.topquadrant.com/technology/shacl/
- [VitroLib templates](https://wiki.lyrasis.org/display/ld4lLABS/Lessons+learned%3A+VitroLib+and+SHACL)
- [Sinopia templates](https://raw.githubusercontent.com/LD4P/sinopia_sample_profiles/master/resourceTemplates/v1/all_resource_templates.json)
- [QA API](https://github.com/samvera/questioning_authority), caveat: [#170](https://github.com/samvera/questioning_authority/issues/170)
