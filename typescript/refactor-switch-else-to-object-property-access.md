## Refactor switch-else to object property access

See [this article](https://archive.vn/R74f7).

Example Code:

```ts
const Status = {
  Running: "running",
  Stop: "stop",
  Aborted: "aborted",
  Finished: "finished",
} as const;
// type StatusType = "running" | "stop" | "aborted" | "finished"
type StatusType = typeof Status[keyof typeof Status];

function getStatusCode2(value: string) {
  switch (value) {
    case Status.Running:
      return 1;
    case Status.Stop:
      return 2;
    case Status.Aborted:
      return 3;
    case Status.Finished:
      return 4;
    default:
      throw new Error(`Unexpected value [${value}]`);
  }
}
```

Example "Solution":

```ts
enum Status {
  Running = "running",
  Stop = "stop",
  Aborted = "aborted",
  Finished = "finished",
}

type StatusType = keyof typeof Status;

const statusCodes = {
  running: 1,
  stop: 2,
  aborted: 3,
  finished: 4,
} as const;

function getStatusCode(value: StatusType): number {
  const code = statusCodes[value];
  if (code === undefined) {
    throw new Error(`Unexpected value [${value}]`);
  }
  return code;
}
```
