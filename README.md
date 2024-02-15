## **Правила именования**

- используем БЭМ
```block__element--modifier```
```block-name__element-name--modifier-name```
- для переменных локализации используем для первого слова в названии тот же регистр, что и в переводимом тексте, далее camelCase/PascalCase. Для небольшого объёма текста используем весь текст при переводе. При переводе длинного текста - первые несколько слов или основной смысл

```html
    <div i18n="@@ConfirmPassword">Confirm password</div>
    <div i18n="@@copyText">copy text</div>
```

- при использовании структуры шаблона (<ng-template>) в разметке (*.html) называть с использованием camelCase

```html
    <ng-container *ngIf="isLoading$ | async; else mainScreen">
    ...........
    </ng-container>
    <ng-template #mainScreen>
    ...........
    </ng-template>
```


- для экспортируемых констант используем UPPER_CASE
```ts
  export const MAX_FILES_SIZE_MB = 10
```
- для enum используем UPPER_CASE
```ts
    enum RUNS_TYPE {
        CHECKLIST = 'checklist',
        CASE = 'case',
    }
```


- для интерфейсов используем PascalCase
```ts
    export interface StepObject {
        id: number;
        data: string;
    }
```

- для интерфейсов, работающих объектами, получаемыми с сервера использовать суффикс DTO
```ts
    export interface PermissionsDTO {
        access: boolean;
        users: number[];
        isAll?: boolean;
    }
```
- type использовать для создания псевдонимов более сложного типа в PascalCase

```ts
    export type GeneralizedStructure = Case | Checklist | Run;
    
    export type CreateRun = Partial<Run>;
```

- в названиях типов и интерфейсов суффиксы "Type" или "Interface" или префикс "I" не используется

- при создании кастомных директивы или пайпа используется префикс "myApp" и camelCase, суффикс "Pipe" или "Directive" не добавляется
```ts
    @Pipe({
      name: 'myAppNameInList',
    })
    
    
    @Directive({
      selector: '[myAppInputTrim]',
    })
```
- при создании кастомного валидатора для функции использовать суффикс Validate
```ts
  export const mustMatchValidate = (formGroup: UntypedFormGroup) =>  {
      ..........
      ..........
      return null;
  };
  ```
  - при создании кастомного валидатора для директивы использовать суффикс Validator
```ts
    @Directive({
        selector: '[mustMatchValidator]',
        providers: [{ provide: NG_VALIDATORS, useExisting: MustMatchDirective, multi: true }],
    })
```

- при создании директив использовать функцию валидатора (для дальнейшей возможности переиспользования и в реактивных формах)
- для приватных членов класса использовать префикс Underscore ( _ )
```ts
    private _project: Project;
    
    private _dialog: MatDialog
    
    private _usersService: UsersService,
    
    private readonly _MAX_SIZE = 10
    
    private _checkFormat(item: BaseStructure) {
    .............
    .............
    }
```


- при создании потоков использовать суффикс Dollar sign ( $ )
```ts
    name$: Observable<string>;
    
    private readonly _projects$ = new BehaviorSubject<Project[]>([]);
```


- избегать написания логики в subscribe
