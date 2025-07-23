# Angular: Best Practices - Button (Button Component)

## Goal
Create a reusable button component with support for:
- different types (primary, secondary, danger, etc.),
- states (disabled, loading),
- custom content (icons, text, ng-content),

## Component structure
- Component selector: `button[ui-button]`
- Standalone + Signals
- `ChangeDetectionStrategy.OnPush`
- Use `host` bindings for classes

## Example component

```ts
type ButtonType = 'primary' | 'secondary' | 'danger';

@Component({ 
  selector: 'button[ui-button]', 
  standalone: true, 
  imports: [], 
  changeDetection: ChangeDetectionStrategy.OnPush, 
  template: '<ng-content/>',
  host: {
    '[class.disabled]': 'disabled()',
    '[class]': 'type()',
    'role': 'button',
    'tabindex': '0',
  }
})
export class ButtonComponent { 
  readonly type = input<ButtonType>('primary');
  readonly disabled = input(false, { transform: booleanAttribute });
  readonly loading = input(false, { transform: booleanAttribute });
}
```

##usage

```ts
import { Component } from '@angular/core';
import { ButtonComponent } from './button.component';


@Component({
  selector: 'app-root',
  standalone: true,
  imports: [ButtonComponent],
  templateUrl: './app.component.html',
  styleUrl: './app.component.css'
})
export class AppComponent {
  handleClick() {
    console.log('clicked')
  }
}
```

```html
<button ui-button type="primary" (click)="handleClick()">Primary button</button>
<button ui-button type="secondary" (click)="handleClick()">Secondary button</button>
<button ui-button type="danger" (click)="handleClick()">Danger button</button>
<button ui-button type="primary" disabled (click)="handleClick()">Disabled button</button>
```
