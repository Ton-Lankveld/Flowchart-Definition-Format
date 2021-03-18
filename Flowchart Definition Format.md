# Flowchart Definition Format

## Author
Ton van Lankveld

## Version
2021 March 18

## Description
A XML file format to define the structure of a flowchart.
The data or process flows in one direction.

## Scope
This definition only describes the structure of the flowchart and **not** the lay-out or graphic rendering.
Not only for the classic software development, but also for work or process flows.

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
  <condition></condition>
  <true></true>
  <false></false>
</decision>
```
A conditional operation, that determines which one of the two paths the program will take. The operation is a true/false test.

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
  <next></next>
</subprogram>
```
Named subprogram or process, which is defined elsewhere.

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
- Terminal (Start/End)
- On-page connector
- Off-page connector
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
Path to a flowchart file. Not only is this tag optional for `<subprogram>`, but can also be used in an other object.

`<reference></reference>`
Unique identification of document or other entity.

`<role></role>`
In a process flowchart, parts of the process are dedicated to a department or role. Every object can have an optional "role" tag.

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
Title or name for this list. Optional.

`<select></select>`
Defines the number of option which must be selected. Requisted.
Values: 0+ | 1+ | 1.
  0+ = Zero or more options can be selected.
  1+ = One or more options can be selected.
  1 = Only one option can be selected.

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
  selected = One or more `<option>` in the `<optionslist>` can have the attribute `status="selected"`.

`<true></true>`
Id of the next object, if the correct number of options is selected. Or the text "end".

`<false></false>`
Id of the next object, if the correct number of options is not selected. Or the text "end".

`<next></next>`
Id of the next object or the text "end".

`<name></name>`
Name of the option.

`<id></id>`
Unique identification of the option.

## References
- [Wikipedia: Flowchart]https://en.wikipedia.org/wiki/Flowchart
- [W3C: Extensible Markup Language]https://www.w3.org/XML/
- [ISO 639-1 - Natural language Codes]https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
- [ISO 3166 - Country Codes]https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes

