```js
// 冒泡排序
function bubbleSort(arr) {
    var i = 0,
        j = 0;
    for (i = 1; i < arr.length; i++) {
        for (j = 0; j <= arr.length - i; j++) {
            var temp = 0;
            // ">" 从小到大排序
            // "<" 从大到小排序
            if (arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    return arr;
}

// 快速排序

function quickSort(arr, l, r) {
    if (l < r) {
        var i = l,
            j = r,
            x = arr[i];
        while (i < j) {
            while (i < j && arr[j] > x)
                j--;

            if (i < j)
            //这里用i++，被换过来的必然比x小，赋值后直接让i自加，不用再比较，可以提高效率
                arr[i++] = arr[j];

            while (i < j && arr[i] < x)
                i++;

            if (i < j)
            //这里用j--，被换过来的必然比x大，赋值后直接让j自减，不用再比较，可以提高效率
                arr[j--] = arr[i];
        }
        arr[i] = x;

        quickSort(arr, l, i - 1);
        quickSort(arr, i + 1, r);
    }
}

let quickSort = function(arr) {
    if (arr.length < 1) {
        return arr;
    }
    //  通过使用splice使数组长度不断减小　　
    //  let pivotIndex = Math.floor(arr.length / 2);
    //  let pivot = arr.splice(pivotIndex,1)[0];　　
    let pivot = arr[0];
    console.log(pivot);
    let left = [];　　
    let right = [];　　
    arr.forEach((value, index, array) => {
        if (index == 0) {
            return;
        }
        value < pivot ? left.push(value) : right.push(value);
    });
    return quickSort(left).concat(pivot, quickSort(right));
};

let quickSort2 = (arr, left, right) => {
    let i, j, pivot;
    //如果 left（左边索引值）大于right(右边索引值)说明一遍比较结束
    if (left >= right) {
        return;
    }
    i = left;
    j = right;
    //将基准值设置为要遍历的子数组的第一个值
    pivot = arr[left];
    //在遍历未相遇时继续遍历
    while (i < j) {
        // 从后往前遍历，直到找到小于基准的值
        while (i < j && arr[j] >= pivot) {
            j--;
        }
        arr[i] = arr[j];
        // 从前往后遍历，直到找到大于基准的值
        while (i < j && arr[i] <= pivot) {
            i++;
        }
        arr[j] = arr[i];
    }
    // 将基准值放回比较结束的起始位置
    arr[i] = pivot;
    // 递归对左部分数组进行比较，直至只剩一个元素
    quickSort2(arr, left, i - 1);
    // 递归比较右部分数组元素，直至只剩一个元素
    quickSort2(arr, i + 1, right);
    return arr;
}


// 二路归并

function merge(left, right) {
    var result = [],
        il = 0,
        ir = 0;

    while (il < left.length && ir < right.length) {
        if (left[il] < right[ir]) {
            result.push(left[il++]);
        } else {
            result.push(right[ir++]);
        }
    }
    while (left[il]) {
        result.push(left[il++]);
    }
    while (right[ir]) {
        result.push(right[ir++]);
    }
    return result;
}

// 交换函数
function swap(array, p1, p2) {
    var temp = array[p1];
    array[p1] = array[p2];
    array[p2] = temp;
}
// 冒泡排序
function bubbleSort(myArray) {
    var len = myArray.length;
    var i;
    var j;
    var stop;

    for (i = 0; i < len - 1; i++) {
        for (j = 0, stop = len - 1 - i; j < stop; j++) {
            if (myArray[j] > myArray[j + 1]) {
                swap(myArray, j, j + 1);
            }
        }
    }

    return myArray;
}

// 选择排序
function selectionSort(myArray) {

    var len = myArray.length,
        min;

    for (i = 0; i < len; i++) {

        // 将当前位置设为最小值
        min = i;

        // 检查数组其余部分是否更小
        for (j = i + 1; j < len; j++) {
            if (myArray[j] < myArray[min]) {
                min = j;
            }
        }

        // 如果当前位置不是最小值，将其换为最小值
        if (i != min) {
            swap(myArray, i, min);
        }
    }

    return myArray;
}

// 插入排序
function insertionSort(myArray) {

    var len = myArray.length, // 数组的长度
        value, // 当前比较的值
        i, // 未排序部分的当前位置
        j; // 已排序部分的当前位置

    for (i = 0; i < len; i++) {

        // 储存当前位置的值
        value = myArray[i];

        /*
         * 当已排序部分的当前元素大于value，
         * 就将当前元素向后移一位，再将前一位与value比较
         */
        for (j = i - 1; j > -1 && myArray[j] > value; j--) {
            myArray[j + 1] = myArray[j];
        }

        myArray[j + 1] = value;
    }

    return myArray;
}

// 合并排序

function merge(left, right) {
    var result = [],
        il = 0,
        ir = 0;

    while (il < left.length && ir < right.length) {
        if (left[il] < right[ir]) {
            result.push(left[il++]);
        } else {
            result.push(right[ir++]);
        }
    }

    return result.concat(left.slice(il)).concat(right.slice(ir));
}
// 1
function mergeSort1(myArray) {

    if (myArray.length < 2) {
        return myArray;
    }

    var middle = Math.floor(myArray.length / 2),
        left = myArray.slice(0, middle),
        right = myArray.slice(middle);

    return merge(mergeSort(left), mergeSort(right));
}
// 2.
function mergeSort2(myArray) {

    if (myArray.length < 2) {
        return myArray;
    }

    var middle = Math.floor(myArray.length / 2),
        left = myArray.slice(0, middle),
        right = myArray.slice(middle),
        params = merge(mergeSort(left), mergeSort(right));

    // 在返回的数组头部，添加两个元素，第一个是0，第二个是返回的数组长度
    params.unshift(0, myArray.length);

    // splice用来替换数组元素，它接受多个参数，
    // 第一个是开始替换的位置，第二个是需要替换的个数，后面就是所有新加入的元素。
    // 因为splice不接受数组作为参数，所以采用apply的写法。
    // 这一句的意思就是原来的myArray数组替换成排序后的myArray
    myArray.splice.apply(myArray, params);

    // 返回排序后的数组
    return myArray;
}

// 快速排序

function swap(myArray, firstIndex, secondIndex) {
    var temp = myArray[firstIndex];
    myArray[firstIndex] = myArray[secondIndex];
    myArray[secondIndex] = temp;
}

function partition(myArray, left, right) {

    var pivot = myArray[Math.floor((right + left) / 2)],
        i = left,
        j = right;


    while (i <= j) {

        while (myArray[i] < pivot) {
            i++;
        }

        while (myArray[j] > pivot) {
            j--;
        }

        if (i <= j) {
            swap(myArray, i, j);
            i++;
            j--;
        }
    }

    return i;
}

function quickSort(myArray, left, right) {

    if (myArray.length < 2) return myArray;

    left = (typeof left !== "number" ? 0 : left);

    right = (typeof right !== "number" ? myArray.length - 1 : right);

    var index = partition(myArray, left, right);

    if (left < index - 1) {
        quickSort(myArray, left, index - 1);
    }

    if (index < right) {
        quickSort(myArray, index, right);
    }

    return myArray;

}



var sorting = {
    //利用sort方法进行排序
    systemSort: function(arr) {
        return arr.sort(function(a, b) {
            return a - b;
        });
    },

    //冒泡排序
    bubbleSort: function(arr) {
        var len = arr.length,
            tmp;
        for (var i = 0; i < len - 1; i++) {
            for (var j = 0; j < len - 1 - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    tmp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = tmp;
                }
            }
        }
        return arr;
    },

    //快速排序
    quickSort: function(arr) {
        var low = 0,
            high = arr.length - 1;
        sort(low, high);

        function sort(low, high) {
            if (low < high) {
                var mid = (function(low, high) {
                    var tmp = arr[low];
                    while (low < high) {
                        while (low < high && arr[high] >= tmp) {
                            high--;
                        }
                        arr[low] = arr[high];
                        while (low < high && arr[low] <= tmp) {
                            low++;
                        }
                        arr[high] = arr[low];
                    }
                    arr[low] = tmp;
                    return low;
                })(low, high);
                sort(low, mid - 1);
                sort(mid + 1, high);
            }
        }
        return arr;
    },

    //插入排序
    insertSort: function(arr) {
        var len = arr.length;
        for (var i = 1; i < len; i++) {
            var tmp = arr[i];
            for (var j = i - 1; j >= 0; j--) {
                if (tmp < arr[j]) {
                    arr[j + 1] = arr[j];
                } else {
                    arr[j + 1] = tmp;
                    break;
                }
            }
        }
        return arr;
    },

    //希尔排序
    shellSort: function(arr) {
        var h = 1;
        while (h <= arr.length / 3) {
            h = h * 3 + 1; //O(n^(3/2))by Knuth,1973
        }
        for (; h >= 1; h = Math.floor(h / 3)) {
            for (var k = 0; k < h; k++) {
                for (var i = h + k; i < arr.length; i += h) {
                    for (var j = i; j >= h && arr[j] < arr[j - h]; j -= h) {
                        var tmp = arr[j];
                        arr[j] = arr[j - h];
                        arr[j - h] = tmp;
                    }
                }
            }
        }
        return arr;
    }
}
```