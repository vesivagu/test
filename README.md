import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class HostBindingService {
  private activeClass = false;
  private color = 'black';

  // Methods to get and set class
  setActiveClass(isActive: boolean) {
    this.activeClass = isActive;
  }

  getActiveClass() {
    return this.activeClass;
  }

  // Methods to get and set color
  setColor(color: string) {
    this.color = color;
  }

  getColor() {
    return this.color;
  }
}






import { Component, HostBinding, OnInit } from '@angular/core';
import { HostBindingService } from './host-binding.service';

@Component({
  selector: 'app-example',
  template: `<p>Example component</p>`
})
export class ExampleComponent implements OnInit {
  @HostBinding('class.active') isActive!: boolean;
  @HostBinding('style.color') hostColor!: string;

  constructor(private hostBindingService: HostBindingService) {}

  ngOnInit(): void {
    // Initialize host properties based on service values
    this.isActive = this.hostBindingService.getActiveClass();
    this.hostColor = this.hostBindingService.getColor();

    // You could also add logic here to watch the service for changes, if needed.
  }
}




