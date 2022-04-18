# Node Reading from STDIN and Writing to STDOUT

```TypeScript
// Begin reading from stdin so the process does not exit.
process.stdin.resume();

process.stdin.setEncoding('utf-8');
let inputString: string = '';
let inputLines: string[] = [];
let currentLine: number = 0;
process.stdin.on('data', function(inputStdin: string): void {
    inputString += inputStdin;
});

process.stdin.on('end', function(): void {
    inputLines = inputString.split('\n');
    inputString = '';
    main();
});

function readLine(): string {
    return inputLines[currentLine++];
}

function writeLine(text): void {
    process.stdout.write(`${text}\n`);
}
```


```TypeScript
import { WriteStream, createWriteStream } from "fs";

const ws: WriteStream = createWriteStream(process.env['OUTPUT_PATH']);
ws.write(text + '\n');
ws.end();
```





