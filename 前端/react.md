1. hooks为什么不能放在if里
2. useContext
3. useMemo
4. 自定义hook
5. 数字精度问题
6. 检测数据类型
7. Promise链式调用，以下分别输出什么

```
Promise.reject(1)
        .then((num) => {
            console.log(num);
        }).catch((num) => {
            return num + 1;
        }).then((num) => {
            console.log(num);
        });
// 2
Promise.resolve(1)
        .then((num) => {
            console.log(num);
        }).catch((num) => {
            return num + 1;
        }).then((num) => {
            console.log(num);
        });
        
// 1
// undefined
```

1. 输入框获取焦点边框高亮
2. 列表表头吸顶
3. 一个父级div，有两个子div，一个固定高度，另一个高度填充满
4. 手写算法

> [{ price: 1, size: 2 }, { price: 2, size: 2 }, { price: 1, size: 1 }]] 依次按照price、size降序排序

```
function sort(arr) {
    for (let i = 0; i < arr.length; i++) {
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[i].price === arr[j].price && arr[i].size < arr[j].size) {
                [arr[i], arr[j]] = [arr[j], arr[i]];
            } else if (arr[i].price < arr[j].price) {
                [arr[i], arr[j]] = [arr[j], arr[i]];
            }
        }
    }
    return arr;
}
```

