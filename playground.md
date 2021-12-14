# Code Institute Playground

The Playground is designed using Google Blockly. It allows students to build code in HTML, JavaScript and Python.

## Usage Instructions

The Playground should be placed in an `iframe` in the LMS. It is configured using URL parameters.

### The Language Parameter

To select which language the Playground displays, use the `lang` parameter. Available options are:

| Value | Meaning      |
|:------|:-------------|
| js    | JavaScript   |
| py    | Python       |
| both  | JavaScript and Python simultaneously |
| html  | HTML         |
| sql   | SQL (under development)

**Sample URL Call:**
`https://code-institute-org.github.io/playground.html?lang=js`

### The Kits Parameter

The `kits` parameter allows you to specify which categories of blocks should appear in the toolbox. You can specify multiple kits, each should be separated by a dollar sign (`$`). Do not use the `kits` parameter in conjunction with the `blocks` parameter. The `blocks` parameter will override `kits`.

| Value  | Notes |
|:-------|:------|
| all    | All categories for JavaScript and Python |
| html   | All categories for HTML |
| sql    | All categories for SQL (under development) |
| funcs  | JavaScript and/or Python |
| lists  | JavaScript and/or Python |
| logic  | JavaScript and/or Python |
| loops | JavaScript and/or Python |
| math   | JavaScript and/or Python |
| text   | JavaScript and/or Python |
| vars   | JavaScript and/or Python |
| htmlbase | HTML only |
| htmlformat  | HTML only |
| htmlforms  | HTML only |
| htmllist  | HTML only |
| htmlscripts | HTML only |
| htmlstyle  | HTML only |
| htmltables | HTML only |
| htmltext | HTML only |

**Sample URL Call:**
`https://code-institute-org.github.io/playground.html?lang=js&kits=text$math$logic`

### The Blocks Parameter

The `blocks` parameter allows you to pre-populate the toolbox with specific blocks, rather than categories. Multiple blocks can be specified, each one should be separated by a dollar sign (`$`).  Do not use the `kits` parameter in conjunction with the `blocks` parameter. The `blocks` parameter will override `kits`.

| Value  | Notes |
|:-------|:------|
| controls_if | JavaScript and/or Python only |
| logic_compare | JavaScript and/or Python only |
| logic_operation | JavaScript and/or Python only |
| logic_negate | JavaScript and/or Python only |
| logic_boolean | JavaScript and/or Python only |
| logic_null | JavaScript and/or Python only |
| logic_ternary | JavaScript and/or Python only |
| controls_repeat_ext | JavaScript and/or Python only |
| controls_whileUntil | JavaScript and/or Python only |
| controls_for | JavaScript and/or Python only |
| controls_forEach | JavaScript and/or Python only |
| controls_flow_statements | JavaScript and/or Python only |
| text | JavaScript and/or Python only |
| text_join | JavaScript and/or Python only |
| text_append | JavaScript and/or Python only |
| text_length | JavaScript and/or Python only |
| text_isEmpty | JavaScript and/or Python only |
| text_indexOf | JavaScript and/or Python only |
| text_charAt | JavaScript and/or Python only |
| text_getSubstring | JavaScript and/or Python only |
| text_changeCase | JavaScript and/or Python only |
| text_trim | JavaScript and/or Python only |
| text_print | JavaScript and/or Python only |
| text_prompt_ext | JavaScript and/or Python only |
| lists_create_with | JavaScript and/or Python only |
| lists_create_with | JavaScript and/or Python only |
| lists_repeat | JavaScript and/or Python only |
| lists_length | JavaScript and/or Python only |
| lists_isEmpty | JavaScript and/or Python only |
| lists_indexOf | JavaScript and/or Python only |
| lists_getIndex | JavaScript and/or Python only |
| lists_setIndex | JavaScript and/or Python only |
| lists_getSublist | JavaScript and/or Python only |
| lists_split | JavaScript and/or Python only |
| lists_sort | JavaScript and/or Python only |
| html | HTML only |
| head | HTML only |
| title | HTML only |
| body | HTML only |
| internal_style | HTML only |
| id_class | HTML only |
| generic_attribute | HTML only |
| body_attributes | HTML only |
| footer | HTML |
| plaintext | HTML only |
| horizontalbreak | HTML only |
| linebreak | HTML only |
| paragraph | HTML only |
| heading | HTML only |
| link | HTML only |
| image | HTML only |
| generictag | HTML only |
| emphasise | HTML only |
| inserted | HTML only |
| strong | HTML only |
| deleted | HTML only |
| super | HTML only |
| sub | HTML only |
| code | HTML only |
| quote | HTML only |
| blockquote | HTML only |
| sample | HTML only |
| keyboard | HTML only |
| variable | HTML only |
| division | HTML only |
| span | HTML only |
| style | HTML only |
| color | HTML only |
| bgcolour | HTML only |
| genericstyle | HTML only |
| span | HTML only |
| division | HTML only |
| generictag | HTML only |
| newlist | HTML only |
| listelement | HTML only |
| description_term | HTML only |
| description_definition | HTML only |
| table | HTML only |
| tablerow | HTML only |
| table | HTML only |
| tablerow | HTML only |
| tablecell | HTML only |
| form | HTML only |
| input_text | HTML only |
| button | HTML only |
| input | HTML only |
| select | HTML only |
| option | HTML only |
| fieldset | HTML only |
| legend | HTML only |
| script | HTML only |
| onclick | HTML only |
| select | SQL (under development) |
| tables_and_columns | SQL (under development) |
| where | SQL (under development) |

**Sample URL Call:**
`https://code-institute-org.github.io/playground.html?lang=js&blocks=text_print$text`

### The Workspace Parameter

The `workspace` parameter allows you to pre-populate the workspace with selected blocks and configurations. Only one workspace configuration can be loaded at a time.

The configuration files need to be individually created and stored in the templates directory.

**Sample URL Call:**
`https://code-institute-org.github.io/playground.html?lang=js&blocks=text_print$text&workspace=unit1`

