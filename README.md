# Angular Training examples

[Training videos](https://udemy.com/course/the-complete-guide-to-angular-2/learn/lecture/6655886#overview) 

## Create 
    
    ng new prj-name
    ng generate component 
    ng g c --skipTests
## Section 2 - The basics

- Data Bindings

    - Event Binding => listen to the click
    - Property binding => enable/disable a button
    - 2 way binding  => fetch our input data
    - String interpolation => output the data

    <button [disabled]="!allowNewServer">...</button>           PB
    <input (input)="onUpdateServerName($event)">                EB
    <input [(ngModel)]="serverName">                            2Way
    <p>{{ serverCreationStatus }}</p>                           SI

- Directives
  Instructions in the DOM.
  Components are directive, but directive with a template.

    <div *ngFor="let logItem of log; let i = index"
        [ngStyle]="{backgroundColor: 'blue' : 'transparent'}"
        [ngClass]="{'white-text': i >= 4}">                        {'class' : ifconditionsatisifed}
    </div>

### Section 5

    <app-cockpit
      (serverCreated)="onServerAdded($event)"
      (bpCreated)="onBlueprintAdded($event)"
    ></app-cockpit>

    <app-server-element *ngFor="let serverElement of serverElements"
      [srvElement]="serverElement"
      [name]="serverElement.name">
      <p #contentParagraph>   </p>
    </app-server-element>
    

Access to template . Local references

    <input #serverNameInput>
    <input #serverContentInput>
    
    <button (click)="onAddServer(serverNameInput)">Add Server</button>
    <button (click)="onAddBlueprint(serverNameInput)">Add Server Blueprint</button>

    class CockpitComponent implements OnInit {
      @ViewChild('serverContentInput', { static: false }) serverContentInput: ElementRef;

      onAddServer(nameInput: HTMLInputElement) {
        this.serverCreated.emit({
          serverName: nameInput.value,                                    //local reerence passed through methods
          serverContent: this.serverContentInput.nativeElement.value      //local reerence fetched through viewchild
        });
      }
    }

ng-content 
  Add content into a component

## Section 6

    <p appBetterHighlight2 [highlightColor]="'red'">...</p>
    <p appBetterHighlight2 highlightColor="red">...</p>                  //equivalent
    <p [appBetterHighlight]="'cyan'" [defaultColor]="'yellow'">...</p>   // or , if   @Input('appBetterHighlight') 

    @HostBinding('style.backgroundColor') backgroundColor: string= 'red';    // bind to property like: {style = "background-color: red"}
    @HostListener('mouseenter') mouseover(eventData: Event)                  // bind to Listener

    or
    constructor(private elRef: ElementRef, private renderer: Renderer2) { }
    this.renderer.setStyle(this.elRef.nativeElement, 'background-color', 'red');
