# Flowchart Definition Format

## Description
As I could not find a good (XML) file format to define a flowchart, I scratched my brain itch and designed my own. Feel free to ignore it.

## Scope
The definition only describes the structure of the flowchart and **not** the graphic rendering. Not only for the classic software development, but also for work or process flows.

## To-Do
- Define Document Type Definition (DTD) or XML Schema Definition (XSD).
- Create tools/applications to analyze DTD's.

## Discussions
### Start Object
As long as there is just one start point of a flowchart, the first object in the file is the start of the chart.
If a chart has more the one start points, a "start" object is required.
For example:
```
<start id="">
  <next></next>
</start>
```

### Style Sheet
How a flowchart is rendered is not a part of the definition, but I like to offer my ideas for a graphical render application.
To define the grafical symbols, a Scalable Vector Graphic (SVG) file with the required symbols will provide the drawing data and the default style.
The style of the symbols, or deviations to the default style, can be captured in a Cascading Style Sheet (CSS) file.
The user of the render application can edit the SVG and CSS files to change the graphics.

### Rendering
For JavaScript [obfc.js]https://github.com/erdincuzun/obfc.js can be used to render the flowchart.

## Contribution
If you got suggestions, comments or remarks, please mail them to []mailto:lankveal@xs4all.nl?subject:Flowchart-Definition-Format .
