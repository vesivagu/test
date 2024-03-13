import { Rule, Tree, SchematicContext, SchematicsException, apply, url, applyToUpdateRecorder, chain } from '@angular-devkit/schematics';
import { findElementWithTagAndAttribute, findElementWithTag } from '@schematics/angular/utility/html-utils';
import { getWorkspace } from '@schematics/angular/utility/config';
import { parse as parseHtml } from 'parse5';
import { strings } from '@angular-devkit/core';

export function updateHtml(): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    const workspace = getWorkspace(tree);
    const projectName = Object.keys(workspace.projects)[0];
    const project = workspace.projects[projectName];

    if (project.projectType !== 'application') {
      throw new SchematicsException(`Update requires a project type of "application".`);
    }

    const sourcePath = `${project.sourceRoot}/app`;
    const htmlFiles = tree.getDir(sourcePath).visit((filePath) => filePath.endsWith('.html'));
    
    // Example classes
    const existingClass = 'old-class';
    const newClass = 'new-class';

    htmlFiles.forEach((filePath) => {
      const fileContent = tree.read(filePath);
      if (!fileContent) {
        return;
      }

      const contentString = fileContent.toString('utf-8');
      const document = parseHtml(contentString);

      // Find elements with the existing class
      const elementsWithExistingClass = findElementWithTagAndAttribute(document, 'div', 'class', existingClass);

      // Update existing elements
      elementsWithExistingClass.forEach((element) => {
        const classes = element.attrs.find(attr => attr.name === 'class');
        if (classes) {
          classes.value += ` ${newClass}`;
        }
      });

      // Add new class to elements without the existing class
      const elementsWithoutExistingClass = findElementWithTag(document, 'p');
      elementsWithoutExistingClass.forEach((element) => {
        const classes = element.attrs.find(attr => attr.name === 'class');
        if (classes) {
          classes.value += ` ${newClass}`;
        } else {
          element.attrs.push({ name: 'class', value: newClass });
        }
      });

      const updatedContentString = strings.serialize(document);
      tree.overwrite(filePath, updatedContentString);
    });

    return tree;
  };
}

export default function(): Rule {
  return chain([
    updateHtml()
  ]);
}
