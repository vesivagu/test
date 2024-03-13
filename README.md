import { Rule, SchematicContext, Tree, chain } from '@angular-devkit/schematics';
import * as parse5 from 'parse5';

function updateHtmlClasses(): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    tree.visit(filePath => {
      if (filePath.endsWith('.html')) {
        const content = tree.read(filePath)?.toString('utf-8');
        if (content) {
          const document = parse5.parse(content);
          traverse(document);
          const modifiedContent = parse5.serialize(document);
          tree.overwrite(filePath, modifiedContent);
        }
      }
    });
    return tree;
  };
}

function traverse(node: any) {
  if (node.attrs) {
    const classAttr = node.attrs.find((attr: any) => attr.name === 'class');
    if (classAttr) {
      // Update existing classes
      // e.g., classAttr.value += ' new-class';
    } else {
      // Add new class
      // e.g., node.attrs.push({ name: 'class', value: 'new-class' });
    }
  }

  if (node.childNodes) {
    node.childNodes.forEach((child: any) => traverse(child));
  }
}

export function mySchematic(options: any): Rule {
  return chain([
    updateHtmlClasses()
  ]);
}
