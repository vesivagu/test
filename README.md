import { Rule, SchematicContext, Tree } from '@angular-devkit/schematics';

export function addProvider(): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    const filePath = 'src/app/app.module.ts';

    // Check if app.module.ts exists
    if (!tree.exists(filePath)) {
      throw new Error(`${filePath} not found!`);
    }

    // Read the file content
    const fileContent = tree.read(filePath)?.toString('utf-8');
    if (!fileContent) {
      throw new Error(`Failed to read ${filePath}`);
    }

    // Add the provider
    const updatedContent = fileContent.replace(
      /providers:\s*\[\s*([^\]]*)\]/,
      (match, providers) => {
        // Ensure there's a comma if the providers list is not empty
        const prefix = providers.trim() ? `${providers.trim()}, ` : '';
        return `providers: [${prefix}MyNewService]`;
      }
    );

    // Write the updated content back to the file
    tree.overwrite(filePath, updatedContent);

    return tree;
  };
}
