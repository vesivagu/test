import { Rule, SchematicContext, Tree, SchematicsException } from '@angular-devkit/schematics';
import { parseTemplate } from '@angular/compiler';
import { findNodes } from '@angular/compiler/src/utils';

export function updateClasses(): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    // Find all HTML files in the project
    const htmlFiles = tree.actions.filter(action => action.path.endsWith('.html'));

    htmlFiles.forEach(action => {
      const htmlContent = tree.read(action.path);
      if (!htmlContent) {
        throw new SchematicsException(`File ${action.path} not found.`);
      }

      const sourceText = htmlContent.toString('utf-8');
      const htmlAst = parseTemplate(sourceText, action.path);
      const elements = findNodes(htmlAst, t => t instanceof Element);

      elements.forEach(element => {
        if (element.name === 'div' && element.attrs.find(attr => attr.name === 'class' && attr.value.includes('old-class'))) {
          // Update existing class or add new class
          const classAttr = element.attrs.find(attr => attr.name === 'class');
          if (classAttr) {
            classAttr.value += ' new-class';
          } else {
            element.attrs.push({ name: 'class', value: 'new-class' });
          }
        }
      });

      const updatedHtml = htmlAst.source;

      // Write back the changes to the file
      tree.overwrite(action.path, updatedHtml);
    });

    return tree;
  };
}
