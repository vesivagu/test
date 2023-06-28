<input type="text" [(ngModel)]="xmlUrl" placeholder="Enter XML URL" />
<button (click)="readXmlFromUrl(xmlUrl)">Read XML</button>


import { Component } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Component({
  selector: 'app-file-reader',
  templateUrl: './file-reader.component.html',
  styleUrls: ['./file-reader.component.css']
})
export class FileReaderComponent {
  constructor(private http: HttpClient) { }

  readXmlFromUrl(url: string) {
    this.http.get(url, { responseType: 'text' })
      .subscribe(
        (xmlContent: string) => {
          // Process the XML content here
          console.log(xmlContent);
        },
        (error) => {
          console.error('Error reading XML file:', error);
        }
      );
  }
}



import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { CommonModule } from '@angular/common';
import { FileReaderComponent } from './file-reader.component';

@NgModule({
  declarations: [FileReaderComponent],
  imports: [CommonModule, FormsModule],
})
export class FileReaderModule { }
