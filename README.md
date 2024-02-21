import { Rule, SchematicContext, Tree } from '@angular-devkit/schematics';
import { parse as parseHtml, serialize } from 'parse5';

export function addCssClass(options: any): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    tree.visit((filePath) => {
      if (filePath.endsWith('.html')) {
        let content = tree.read(filePath)?.toString('utf-8');
        if (content) {
          const document = parseHtml(content);
          // Implement logic to traverse the HTML document, identify specific input elements, and add the CSS class
          // For example:
          document.childNodes.forEach((node) => {
            if (node.nodeName === 'input') {
              // Check if this input matches your criteria and add the CSS class
              // For example:
              node.attrs.push({ name: 'class', value: options.className });
            }
          });

          // Serialize the updated document back to HTML
          const updatedContent = serialize(document);
          tree.overwrite(filePath, updatedContent);
        }
      }
    });

    return tree;
  };
}
