import { Rule, SchematicContext, Tree, apply, chain, url, mergeWith } from '@angular-devkit/schematics';
import { parse as parseJson } from 'jsonc-parser';

// Define options interface
export interface AddCssClassOptions {
  className: string;
}

// Add CSS class rule to component template
function addCssClass(options: AddCssClassOptions): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    tree.visit((filePath) => {
      if (filePath.endsWith('.component.html')) {
        const fileContent = tree.read(filePath)?.toString('utf-8');
        if (fileContent) {
          const updatedContent = fileContent.replace('</div>', `<div class="${options.className}"></div>`);
          tree.overwrite(filePath, updatedContent);
        }
      }
    });
    return tree;
  };
}

// Main schematic function
export function addCssClassSchematic(options: AddCssClassOptions): Rule {
  return chain([
    addCssClass(options),
    mergeWith(url('./files')),
  ]);
}
