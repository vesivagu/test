import {
  Rule,
  SchematicContext,
  Tree,
  apply,
  chain,
  mergeWith,
  template,
  url
} from '@angular-devkit/schematics';
import { strings } from '@angular-devkit/core';

export function addCssClass(options: any): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    const projectDir = '/path/to/your/angular/app';
    const htmlFiles = tree.getDir(projectDir).visit((filePath) => filePath.endsWith('.html'));

    htmlFiles.forEach((htmlFile) => {
      const content = tree.read(htmlFile)!.toString('utf-8');
      const updatedContent = content.replace('<input', '<input class="' + options.className + '"');

      tree.overwrite(htmlFile, updatedContent);
    });

    return tree;
  };
}

export function mySchematic(options: any): Rule {
  return (_tree: Tree, _context: SchematicContext) => {
    return chain([
      mergeWith(apply(url('./files'), [template({...options, ...strings})])),
      addCssClass(options)
    ]);
  };
}
