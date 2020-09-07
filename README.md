# NativeScript Charts Tips

> nativescript-ui-chart: ^7.1.1

## Pie Chart

```
<RadPieChart>
  <DonutSeries ... valueProperty="usage"></DonutSeries>
</RadPieChart>
```
  - It only draws and shows when there are **2 or more elements**
  ex:
    ```js
    [
      {
        color: "red",
        usage: 10000
      }
    ]
    ```
  - At least 2 elements are valid (not: null, 0, empty ... )
  ex:
    ```js
    [
      {
        color: "red",
        usage: 10000
      },
      {
        color: "blue",
        usage: 0
      }
    ]
    ```
  - The percentage between the biggest element and the smallest element must greater than the accepted point (~0.0001, ~ 0.01%)
  ex: `biggest/smallest = 1/1000000 (< 0.0001)`
    ```js
    [
      {
        color: "red",
        usage: 1000000
      },
      {
        color: "blue",
        usage: 50000
      },
      {
        color: "green",
        usage: 1
      }
    ]
    ```

So to solve the above cases. What should we do? In fact I'm not sure is that the best solution? But in the short term, it solved my proplem:
```js
let data = [
  {
    color: "red",
    usage: xx.xx
  },
  {
    color: "blue",
    usage: yy.yy
  }
]

const
    item1 = data[0].usage,
    item2 = data[1].usage,
    onlyItem1 = (!item2 && item1) || (item2 / item1 < 0.0001),
    onlyItem2 = (!item1 && item2) || (item1 / item2 < 0.0001);

data = [
  {
    color: onlyItem2 ? "blue" : "red",
    usage: onlyItem2 ? 0.0001 * item2 : item1
  },
  {
    color: onlyItem1 ? "red" : "blue",
    usage: onlyItem1 ? 0.0001 * item1 : item2
  }
];
```
> It's easy to know What i'm doing, right? =]]]]


## Bar Chart
....
