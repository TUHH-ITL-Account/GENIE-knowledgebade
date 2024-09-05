# Authoring Knowledge Models

Course-based knowledge models are not part of the FDL-dsl per se, but build upon its concept 
to provide the generator with a formal representation of the course's contents.

Knowledge models are essentially tree structures with different types of nodes: topic nodes and
FDL nodes. They are stored as two lists in a `.yaml` file, which leads to the basic structure:

Node definition (- $NAME:), in fdlnodes and wmnodes section can be set arbitrary. In fdlnodes section they should contain the fdl type, see example.
Name of file (filename: $NAME.fdl) must be equal to the file name in your OS.
Make sure that in the wmnodes part of the .yaml file only the node definition names are used to attach FDLs!

#### Important notes
- RESPECT YAML SPACING AS SHOWN IN THE Example
- nodes have 2 (two) indents!
- attributes of nodes need 6 (six) spaces in total!
- there must be no random spaces at random lines anywhere in the file!

Example TechnischeLogistikSS22.yaml:
```
---
fdlnodes:
  - Stetigförderer_Def:
      id: fdl3
      filename: Stetigförderer_Def.fdl
      prereq: []
  - Gesamtwiderstand_Eq2:
      id: fdl4
      filename: Gesamtwiderstand_Eq2.fdl
      prereq: [Multiplikation, Addition]
  --other fdl nodes--
wmnodes:
  - Fördermaschinen:
      name: "Fördermaschinen"
      id: wm4
      children: [Fördersysteme]
      fdls: [Funktionen_von_Fördermaschinen_Ex]
  - Fördersysteme:
      name: "Fördersysteme"
      id: wm5
      children: [Stetigförderer, Unstetigförderer]
      fdls: [Unterscheidung_Stetigförderer_und_Unstetigförderer_TO, Häufige_Fördermittel_für_Fördergüter_Ex]
  --other wm nodes--
```

FDL nodes are an extra encapsulation layer for FDLs, allowing the addition of relevant attributes.

WM nodes (wm (ger): 'Wissensmodel') represent topics. Each topic can have an arbitrary number of FDLs 
attached to it.

The `children` relation of wm-nodes defines a rough 'is part of' relation between the specific course's
topics, spanning the tree. Note that this means cycles being forbidden.

A topic node having multiple parents is forbidden and a FDL node being part of different topics is
to be used with caution.
