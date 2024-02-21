import { Rule, SchematicContext, Tree, chain, apply, url, forEach, MergeStrategy, MergeWithConflictResolution } from '@angular-devkit/schematics';
import { parse as parseHtml, HTMLElement } from 'node-html-parser';

export default function (options: any): Rule {
  return (tree: Tree, context: SchematicContext) => {
    return chain([
      addCssClass(options),
    ])(tree, context);
  };
}

function addCssClass(options: any): Rule {
  return (tree: Tree, context: SchematicContext) => {
    return forEach((fileEntry) => {
      if (fileEntry.path.endsWith('.html') || fileEntry.path.endsWith('.css')) {
        const content = fileEntry.content.toString('utf-8');

        if (fileEntry.path.endsWith('.html')) {
          const parsedHtml = parseHtml(content);
          // Find elements in HTML and add CSS class
          parsedHtml.querySelectorAll(options.selector).forEach((element: HTMLElement) => {
            if (!element.classNames.includes(options.className)) {
              element.classNames.add(options.className);
            }
          });
          tree.overwrite(fileEntry.path, parsedHtml.toString());
        }

        if (fileEntry.path.endsWith('.css')) {
          // Add CSS rule for the specified class
          const newCssRule = `.${options.className} { /* Your CSS styles here */ }`;
          tree.create(fileEntry.path, content + '\n\n' + newCssRule);
        }
      }
    });
  };
}
