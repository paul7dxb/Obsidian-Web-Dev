# Functions & Types

- Functions have places where types can be defined:
	- Parameters


Hovering over functions will show returned types which may be infered
![[TypeScript_Function_Inferred.png]]

- Declaring returned type
```TS
function add(a: number, b: number): number | string {
  return a + b;
}
```

```TS
function printOutput(value: any): void {
    console.log(value)
}
```