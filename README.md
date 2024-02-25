import { Rule, SchematicContext, Tree, chain, externalSchematic } from '@angular-devkit/schematics';

export function checkAttributes(options: any): Rule {
  return (tree: Tree, context: SchematicContext) => {
    // Read JSON file
    const jsonContent = JSON.parse(tree.read('path/to/your/json/file.json')!.toString());

    // Traverse Angular app
    const angularAppPath = 'path/to/your/angular/app';
    const files = tree.getDir(angularAppPath).visit((filePath) => {
      // Check attributes in each file
      const content = tree.read(filePath)!.toString();
      if (content.includes(jsonContent.attribute)) {
        context.logger.info(`Attribute ${jsonContent.attribute} found in ${filePath}`);
      } else {
        context.logger.warn(`Attribute ${jsonContent.attribute} not found in ${filePath}`);
      }
    });

    return tree;
  };
}
