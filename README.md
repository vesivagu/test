import { Rule, SchematicContext, Tree, chain, template, url } from '@angular-devkit/schematics';

export function addCssClass(options: any): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    return chain([
      updateHtmlFiles(options)
    ])(tree, _context);
  };
}

function updateHtmlFiles(options: any): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    tree.getDir('/src/app').visit((filePath) => {
      if (filePath.endsWith('.html')) {
        let content = tree.read(filePath)!.toString('utf-8');
        // Modify content to add the CSS class
        content = content.replace('<div', '<div class="your-css-class"');
        tree.overwrite(filePath, content);
      }
    });
    return tree;
  };
}
