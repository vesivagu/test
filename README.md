import { Rule, SchematicContext, Tree, chain } from '@angular-devkit/schematics';
import { getProjectMainFile } from '@angular/cdk/schematics';
import { buildRelativePath } from '@schematics/angular/utility/find-module';

export function addCssClass(options: any): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    const workspaceConfigBuffer = tree.read('angular.json');
    if (!workspaceConfigBuffer) {
      throw new Error('Could not find angular.json');
    }

    const workspaceConfig = JSON.parse(workspaceConfigBuffer.toString());
    const projectName = options.project || workspaceConfig.defaultProject;
    const project = workspaceConfig.projects[projectName];

    if (project.projectType !== 'application') {
      throw new Error(`The ${projectName} is not an Angular application.`);
    }

    const mainPath = getProjectMainFile(project);

    const templatePath = `${project.sourceRoot}/${project.prefix}/app`;

    return chain([
      modifyTemplates(templatePath, options.className),
    ]);
  };
}

function modifyTemplates(templatePath: string, className: string): Rule {
  return (tree: Tree) => {
    tree.visit(filePath => {
      if (filePath.startsWith(templatePath) && filePath.endsWith('.html')) {
        const content = tree.read(filePath)?.toString('utf-8');
        if (content) {
          const updatedContent = content.replace(/<div/g, `<div class="${className}"`);
          tree.overwrite(filePath, updatedContent);
        }
      }
    });
    return tree;
  };
}
