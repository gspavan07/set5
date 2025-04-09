## ✅ Set 10 

### 1. Load `CoursesListComponent` when a button is clicked

**Generate Component:**

**app.component.ts**
```ts
import { CommonModule } from '@angular/common';
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  imports: [CommonModule],
  templateUrl: './app.component.html',
  styleUrl: './app.component.css'
})
export class AppComponent {
  title = 'demo';
  showCourses = false;
  courses = ['Angular', 'React', 'Vue'];
}

```

**app.component.html**
```html
<button (click)="showCourses = !showCourses">View courses list</button>
<div *ngIf="showCourses">
  <ul>
    <li *ngFor="let course of courses">{{ course }}</li>
  </ul>
</div>
```

---

### 2. Apply multiple CSS classes using `ngClass`

**styles.css**
```css
.highlight {
  background-color: yellow;
  padding: 5px;
}

.bold {
  font-weight: bolder;
}
```

**app.component.html**
```html
<p [ngClass]="{ highlight: isHighlighted, bold: isBold }">
  Angular ngClass Directive Example
</p>

<button (click)="toggleHighlight()">Toggle Highlight</button>
<button (click)="toggleBold()">Toggle Bold</button>
```
**app.component.ts**
```ts
import { CommonModule } from '@angular/common';
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  imports: [CommonModule],
  templateUrl: './app.component.html',
  styleUrl: './app.component.css'
})
export class AppComponent {
  isHighlighted = false;
  isBold = false;
  toggleHighlight() {
    this.isHighlighted = !this.isHighlighted;
  }
  toggleBold() {
    this.isBold =!this.isBold;
  }
}

```

---

### 3. Create a component called `HelloComponent` and render "Hello Angular"

**Generate Component:**
```bash
ng generate component hello
```

**hello.component.html**
```html
<h2>Hello Angular</h2>
```

**app.component.html**
```html
<app-hello></app-hello>
```

---
