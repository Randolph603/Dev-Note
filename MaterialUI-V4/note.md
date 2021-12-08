## ISSUE: types of property 'textTransform' are incompatible.

* solution 1:
tyr textTransform: "uppercase" as const that works for me

* solution 2:
textTransform: "uppercase" as "uppercase",

* solution 3:
  ```
  const style = (theme: Theme) => createStyles({
        textTransform: "uppercase"
  })
  ```