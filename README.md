import { Rule, SchematicContext, Tree, apply, mergeWith, url } from '@angular-devkit/schematics';
import { strings } from '@angular-devkit/core';

export function checkAttributes(options: any): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    // Read the JSON file
    const jsonFileContent = tree.read(options.jsonFilePath);
    if (!jsonFileContent) {
      throw new Error(`JSON file '${options.jsonFilePath}' not found.`);
    }

    const jsonContent = JSON.parse(jsonFileContent.toString());

    // Traverse through the Angular app files
    tree.visit((filePath) => {
      if (filePath.endsWith('.ts') || filePath.endsWith('.html')) {
        const fileContent = tree.read(filePath)?.toString('utf-8');
        if (fileContent) {
          Object.keys(jsonContent).forEach((attribute) => {
            if (fileContent.includes(attribute)) {
              _context.logger.info(`Attribute '${attribute}' found in file '${filePath}'.`);
            } else {
              _context.logger.warn(`Attribute '${attribute}' not found in file '${filePath}'.`);
            }
          });
        }
      }
    });

    return tree;
  };
}

export function attributeCheck(options: any): Rule {
  return (_tree: Tree, _context: SchematicContext) => {
    const templateSource = apply(url('./files'), [
      // other manipulations...
    ]);
    return mergeWith(templateSource);
  };
}
