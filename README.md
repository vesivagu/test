<div class="drop-zone" (dragover)="onDragOver($event)" (dragleave)="onDragLeave($event)" (drop)="onDrop($event)">
  <p>Drag and drop XML files here</p>
</div>

import { Component } from '@angular/core';

@Component({
  selector: 'app-file-upload',
  templateUrl: './file-upload.component.html',
  styleUrls: ['./file-upload.component.css']
})
export class FileUploadComponent {

  onDragOver(event: DragEvent) {
    event.preventDefault();
  }

  onDragLeave(event: DragEvent) {
    event.preventDefault();
  }

  onDrop(event: DragEvent) {
    event.preventDefault();
    const files = event.dataTransfer?.files;
    if (files && files.length > 0) {
      this.handleFiles(files);
    }
  }

  handleFiles(files: FileList) {
    for (let i = 0; i < files.length; i++) {
      const file = files[i];
      if (file.type === 'text/xml') {
        const reader = new FileReader();
        reader.onload = (e) => {
          const contents = e.target?.result as string;
          // Process the XML contents
          console.log(contents);
        };
        reader.readAsText(file);
      } else {
        console.log('Invalid file type. Please drop an XML file.');
      }
    }
  }
}


.drop-zone {
  border: 2px dashed #ccc;
  border-radius: 5px;
  width: 300px;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}
