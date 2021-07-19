# Flowchart Definition Format

## Author
Ton van Lankveld

## Version
2021 July 19

## Description
A XML file format to define the structure of a flowchart.

## Scope
This definition only describes the structure of the flowchart and **not** the lay-out or graphic rendering.
Not only for classic software development, but also for other work or process flows.

## License
[MIT Opensource]https://opensource.org/licenses/MIT

## General Comments
- First object in the file, is the start point of the chart.
- `<next>`, `<true>` and `<false>` contain the id of the next object.
- The tags `<next>`, `<true>` or `<false>` connect the objects.
- If `<next>`, `<true>` or `<false>` = end, then end of the flow.

## Objects
Every object **must** have an "id" attribute.
If the natural language in an object is an other then the default, as defined in the top-level "flowchart" tag, the "xml:lang" attribute **must** define the other language.

### Top Level
```
<flowchartstructure xml:lang="">
  <title></title>
  <description></description>
  <version></version>
  -
  -
</flowchartstructure>
```
Top tage of the chart definition.
Attributes:
`xml:lang` - Required - Natural language (ISO 639-1) of the text in the chart and the countery code (ISO 3166) if necessary. Example: xml:lang="en-US".
`id`       - Optional - Unique identification string. Can be helpful if there are more the one flowchart in a file. Example: id="p01".

### Process
```
<process id="">
  <text></text>
  <next></next>
</process>
```
Represents a set of operations that changes value, form, or location of data.

### Decision
```
<decision id="">
  <text></text>
  <condition></condition>
  <true></true>
  <false></false>
</decision>
```
A conditional operation, that determines which one of the two paths the program will take. The operation is a true/false test.
The text-tag is optional.

### In- and Output
```
<inoutput id="">
  <text></text>
  <next></next>
</inoutput>
```
Indicates the process of inputting data or outputting data, as in entering data or displaying results.

### Subprogram or Sub-procedure
```
<subprogram id="">
  <text></text>
  <link></link>
  <next></next>
</subprogram>
```
Named subprogram or process, which is defined elsewhere.
The link-tag points the an other FDF-file. Optional.

### Database or File
```
<database id="">
  <text></text>
  <next></next>
</database>
```
Data file or database.

### Document
```
<document id="">
  <title></title>
  <reference></reference>
  <next></next>
</document>
```
One document.

### Multi-document
```
<multidocument id="">
  <text></text>
  <next></next>
</multidocument>
```
More then one document.

### Annotation
```
<annotation id="">
  <text></text>
  <objectid></objectid>
  <objectid></objectid>
</annotation>
```
Additional information about a step in the program.

## Other ANSI/ISO Symbols
These flowchart symbols have no object representation in this definition:
- Terminal (Start/End). See: General Comments
- On-page connector. Not applicable
- Off-page connector. A FDF-file contance a compleet flowchart
- Manual operation/input
- Preparation or initialization


## Tags
`<version></version>`
Version/date of the chart or software/process release.

`<description></description>`
Description of the software or process.

`<next></next>`
Id of the next object or the text "end".

`<text></text>`
Short description.

`<title></title>`
Know title of document or process.

`<condition></condition>`
A test to compare 2 or more data values or conditions.

`<true></true>`
Id of the next object, if the test of the condition is true. Or the text "end".

`<false></false>`
Id of the next object, if the test of the condition is false. Or the text "end".

`<name></name>`
Name of the subprogram.
Optional: If name not found, then follow link to name of sub-flowchart.

`<link></link>`
Path to a FDF-file. Not only is this tag optional for `<subprogram>`, but can also be used in an other object.

`<reference></reference>`
Unique identification of document or other entity.

`<role></role>`
In a process flowchart, parts of the process are dedicated to a department or role. Every object can have an optional "role" tag.

`<...></...>`
Custom tag.  **Must** be valid XML.

## Extension
### Options List
In a work or process flow there are situations where options have to be considered. For example to analize a sales order. This can be done with a serie of Desicion objects, but that is not very effective. An Options List is shorter and more readable.
Defines an options list and the way the options are selected.

### Example Object
```
<optionslist id="">
  <title></title>
  <select></select>
  <option>
    <name></name>
    <id></id>
  </option>
  <option>
    <name></name>
    <id></id>
  </option>
  <option>
    <name></name>
    <id></id>
  </option>
  <next></next>
</optionslist>
```

### Tags
`<title></title>`
Title or name for this list. Required.

`<select></select>`
Defines the number of option which must be selected. Required.
Values: 0+ | 1+ | 1 | 0/1
- 0+ = Zero or more options can be selected.
- 1+ = One or more options can be selected.
- 1 = Only one option can be selected.
- 0/1 = Zero exclusive or 1 options can be selected.

```
<option>
  <name></name>
  <id></id>
</option>
  ```
`<option>` can have an optional `<next></next>` to point to the next object. If so, all the options in this `<optionslist>` **must** have a `<next></next>`.
`<option>` can have an optional attribute; status. Example: `status="default"`.
Values: "default" | "selected".
  default = Only one option in the `<optionslist>` can be the default selection.
  selected = One or more (depends on `<select>` value) `<option>` in the `<optionslist>` can have the attribute `status="selected"`.

`<next></next>`
Id of the next object or the text "end".

`<name></name>`
Name of the option.

`<id></id>`
Unique identification of the option.

`<next></next>`
Id of the next object or the text "end".

`<if-0></if-0>`
In case `<select>` = 0/1; Id of the next object, if no (0) option is selected.

`<if-1></if-1>`
In case `<select>` = 0/1; Id of the next object, if one (1) option is selected.

### Behaviour
- If value(s) of `<select>` is not met, generate an error message.
- In case of `<select>` value is 1 or 0/1; stop search in list if an option is found en go to object in `<next>`.

### Graphic Examples
![alt Three examples of the options-list object](./pictures/FDF-Options-List-Graphics-Examples.svg)


## References
- [Wikipedia: Flowchart]https://en.wikipedia.org/wiki/Flowchart
- [W3C: Extensible Markup Language]https://www.w3.org/XML/
- [ISO 639-1 - Natural language Codes]https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
- [ISO 3166 - Country Codes]https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes
