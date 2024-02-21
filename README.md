import { Rule, Tree, SchematicContext, SchematicsException, apply, url, template, mergeWith } from '@angular-devkit/schematics';
import { strings } from '@angular-devkit/core';

export function addCssClass(options: any): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    // Logic to modify HTML files
    // Example: find all <input> elements with a specific attribute and add a class
    const projectDir = '/path/to/your/angular/app';
    const htmlFiles = tree.getDir(projectDir).visit((filePath) => filePath.endsWith('.html'));

    htmlFiles.forEach((htmlFile) => {
      const content = tree.read(htmlFile)!.toString('utf-8');
      // Use a library like `cheerio` to parse HTML and manipulate DOM elements
      // Example:
      // const $ = cheerio.load(content);
      // $('input[data-special]').addClass('special-class');
      // tree.overwrite(htmlFile, $.html());
    });

    return tree;
  };
}

export function mySchematic(options: any): Rule {
  return (_tree: Tree, _context: SchematicContext) => {
    // Apply changes to HTML files
    return mergeWith(apply(url('./files'), [
      template({...options, ...strings}),
      addCssClass(options)
    ]));
  };
}
