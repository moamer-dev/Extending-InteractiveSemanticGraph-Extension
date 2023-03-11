# Extending-InteractiveSemanticGraph-Extension

The main objective of the extension is to facilitate the visualization of SemanticMediawiki data using VisNetwork.js, which creates a relational network based on the properties. The extension resource can be accessed through its [GitHub Page](https://github.com/OpenSemanticLab/mediawiki-extensions-InteractiveSemanticGraph).

**The extension comprises two main JavaScript files that include the primary functions of the program:**

* The first file, InteractiveSemanticGraphUtils.js, serves two distinct functions:
  - Firstly, it creates the primary API URL that is utilized in the ASK API call.
  - This is achieved using the getSmwQuery(root, properties) function, which relies on two critical components: the ROOT node and the properties list defined on the embedded widget.
* The second file, InteractiveSemanticGraph.js, comprises the most frequently used functionalities of the program. These include:
  - loading the [MWJSOn](https://github.com/ofrohn/d3-celestial/blob/master/data/mw.json) module.
  - Initiating the [ASK API](https://www.semantic-mediawiki.org/wiki/Help:API:ask) call.
  - Creating the network.
  - And visualizing the API response.

In certain instances, labels associated with properties may be incomprehensible for typical users. To address this issue, the extension employs the special property [{{DISPLAYTITLE}}](https://www.semantic-mediawiki.org/wiki/Help:Special_property_Display_title_of) which can be specified on the Semantic MediaWiki (SMW) entity template to modify the assigned entity's title, such as a page or project title. Upon testing {{DISPLAYTITLE}} functionality, it was observed that the special property worked well with all entities except for property labels. When {{DISPLAYTITLE}} was utilized with properties, the ASK API response, which serves as the primary call of the extension, returned the default property labels rather than the assigned title. Therefore, it was crucial to extend the functionality to substitute the default labels with other preferred labels to enhance human readability for users.

To accomplish this, another special property that includes a Preferred label can be utilized to modify the default label of properties. When assigned to a property, the label is also altered in the ASK API response. Although it is possible to obtain the preferred label easily using the [Browse API](https://www.semantic-mediawiki.org/wiki/Help:API:smwbrowse), the extension heavily relies on the ASK API call method; thus, it was deemed preferable not to alter the API call method.

## The extension's functionalities were extended to include the following functionalities:

* Replace node default labels with the prefered labels.
* Replace properties default labels with the prefered labels.
* Replace legend box default labels with the prefered labels.
* Replace node connection labels with the prefered labels.
* Manage the properties displayes on the right click menu.

***In order to manage the right click menu included properties, you have to define the discarded properties in InteractiveSemanticGraph shortcode.***

An example
```
<div style="width: 100%;" class="InteractiveSemanticGraph">{ "root":"TestPage", "properties":["HasProperty1", "HasProperty2"], , "cus_properties":["HasProperty3", "HasProperty4"], "permalink": false, "autoexpand": false, "depth": 3 }</div>
```

These changes can be applied to any project and not solely specific to a certain project.
