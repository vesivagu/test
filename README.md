import { Rule, SchematicContext, SchematicsException, Tree } from '@angular-devkit/schematics';
import { Schema as MySchematicSchema } from './schema';
import { Schematics } from '@angular-devkit/schematics/tools';

export function mySchematic(options: MySchematicSchema): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    const workspaceConfigBuffer = tree.read('angular.json');
    if (!workspaceConfigBuffer) {
      throw new SchematicsException('Not an Angular CLI workspace');
    }

    const workspaceConfig = JSON.parse(workspaceConfigBuffer.toString());
    const projectName = options.project || workspaceConfig.defaultProject;

    // Prompting user for input
    const prompts: Schematics.PromptQuestionCollection = [
      {
        type: 'input',
        name: 'name',
        message: 'What is your name?'
      }
    ];

    return Schematics.prompt(prompts, (answers) => {
      // Use the user's input here
      const { name } = answers;
      _context.logger.info(`Hello, ${name}!`);

      // Perform other schematic tasks using the user's input
      // For example, generating files, modifying configuration, etc.

      return tree;
    });
  };
}
