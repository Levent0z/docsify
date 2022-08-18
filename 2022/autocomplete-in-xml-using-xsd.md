# Autocomplete in XML using XSD

To get Intellisense (aka autocomplete) in VSCode, you need to:

1. Install the [XML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml) extension by Red Hat
2. Have an XSD file for the XML
3. Reference the XSD from the XML, or configure the extension with a mapping.

## Generate an XSD from an XML

If you don't have the XSD (or it doesn't exist)

1. Use an online tool such as [FreeFormatter](https://www.freeformatter.com/xsd-generator.html) to use an example XML as basis for the XSD.
2. Save the XSD content in a `.xsd` file in the same folder as the XML (preferably), e.g. **example.xsd**.

What happens next is dependent on the content of the XML file. What I'm about to describe below is based on a single XML file I experimented with. **YMMV**.

In the example XML file I looked at, the XML elements did not have a namespace prefix. The root element had an `xmlns` attribute that contained a URI to some metadata, but that URI didn't exist. The presence of the `xmlns` attribute in the XML manifests as a `targetNamespace` attribute in the root element of the generated XSD. This may cause the following warning by the XML VSCode extension:

```
Expecting no namespace, but the schema document has a target namespace ...
```

To avoid this (temporarily at least), remove the `targetNamespace` attribute from the XSD and the `xmlns` attribute from the top element.

## Activating Autocomplete

When you activate autocomplete for XML in VSCode (such as when you type `<` inside an element), you should get additional suggestions in the menu that pops up. There should be choices other than `<!--` and `<![CDATA[>`. For this to work, the XML file must be associated with the XSD file. There are several ways to do this:

### 1. Using `xml-model`

This is probably the easiest. Simply add a new line (below the top `<?xml`) like in this example:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<?xml-model href="example.xsd"?>
```

Remove any **xsi** attributes (see option 3) if you have them.

### 2. Using `XMLSchema-instance`

Configure your top XML element by adding the attributes shown in the example below:

```xml
<TopLevelElement xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  xsi:noNamespaceSchemaLocation="example.xsd">
    <!-- ... -->
</TopLevelElement>
```

Notice the use of the `noNamespaceSchemaLocation` attribute instead of the `schemaLocation` attribute.

### 3. Using a local configuration

In VSCode, while the XML file is the active tab, bring up the command palette and select `XML: Bind to grammar/schema file`. If you're using a local file for the XSD, select `File Association` next. Select the XSD file in the file dialog. You may need to massage the filename a little bit before it accepts it. (Decode URL-encoded characters and remove the double asterisk.) The extension will save this configuration into your Workspace Settings under `xml.fileAssociations`, which you can later edit.

If you're trying this option first, make sure to clear those settings before you try other options.

## Relaxing the XSD

The generated XSD may assume that the elements may have to come in a certain order, so it describes child elements using `<xs:sequence>`. You can replace this with `<xs:choice minOccurs="0" maxOccurs="unbounded">`.
