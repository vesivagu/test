import { Rule, Tree, SchematicContext, SchematicsException, chain } from '@angular-devkit/schematics';
import { getWorkspace } from '@schematics/angular/utility/config';
import { parse as parseHtml, serialize } from 'parse5';

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

      let contentString = fileContent.toString('utf-8');
      const document = parseHtml(contentString);

      // Update existing class and add new class
      updateClassAndAddNewClass(document, existingClass, newClass);

      // Serialize the updated document and overwrite the file
      const updatedContentString = serialize(document);
      tree.overwrite(filePath, updatedContentString);
    });

    return tree;
  };
}

function updateClassAndAddNewClass(document: any, existingClass: string, newClass: string) {
  function traverse(node: any) {
    if (node.attrs) {
      const classAttr = node.attrs.find((attr: any) => attr.name === 'class');
      if (classAttr && classAttr.value.includes(existingClass)) {
        // Update existing class
        classAttr.value = classAttr.value.replace(existingClass, newClass);
      } else if (!classAttr) {
        // Add new class if class attribute doesn't exist
        node.attrs.push({ name: 'class', value: newClass });
      }
    }

    if (node.childNodes) {
      node.childNodes.forEach((childNode: any) => {
        traverse(childNode);
      });
    }
  }

  traverse(document);
}

export default function(): Rule {
  return chain([
    updateHtml()
  ]);
}
