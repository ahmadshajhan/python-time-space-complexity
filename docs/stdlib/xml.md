# xml Module

The `xml` module provides base functionality for parsing and manipulating XML documents, with submodules for DOM, SAX, and ElementTree.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Parse XML | O(n) | O(n) | n = document size; DOM loads entire tree |
| DOM traversal | O(n) | O(n) | n = nodes; consider SAX for large files |
| XPath query | O(n) | O(n) | n = nodes searched; result depends on query |

## XML Processing

### Using ElementTree

```python
import xml.etree.ElementTree as ET

# Parse XML - O(n)
tree = ET.parse('data.xml')
root = tree.getroot()

# Navigate tree - O(n)
for item in root.findall('item'):
    name = item.find('name').text
    price = item.find('price').text
    print(f"{name}: {price}")

# Modify and save - O(n)
root.attrib['updated'] = 'True'
tree.write('modified.xml')
```

### Creating XML

```python
import xml.etree.ElementTree as ET

# Create root - O(1)
root = ET.Element('catalog')

# Add children - O(1) each
item = ET.SubElement(root, 'item')
item.set('id', '1')

name = ET.SubElement(item, 'name')
name.text = 'Product'

price = ET.SubElement(item, 'price')
price.text = '29.99'

# Save - O(n)
tree = ET.ElementTree(root)
tree.write('output.xml')
```

## Related Documentation

- [html Module](html.md)
- [json Module](json.md)
