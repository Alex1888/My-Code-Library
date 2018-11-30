* 从大到小排序, 每次: 找到第一个大于pivot的high放在前面, 第一个小于pivot的low放在pivot的后面
* 注意的是qsort里要有一个if来判断终止条件

```C++
int partition(vector<int>& v, int low, int high) {
	int pivot = v[low];
	int tmp = v[low];
	while (low < high) {
		while (low < high && v[high] >= pivot) high--;
		v[low] = v[high];
		while (low < high && v[low] <= pivot) low++;
		v[high] = v[low];
	}

	v[low] = tmp;
	return low;
}

void qsort(vector<int>& v, int low, int high) {
	if (low < high) {
		int pivotloc = partition(v, low, high);
		qsort(v, low, pivotloc-1);
		qsort(v, pivotloc+1, high);
	}
}

```

* 从小往大排, 每次: 找到第一个小于pivot的high放在前面, 找到第一个大于pivot的low放在后面

```c++
int partition2(vector<int>& nums, int low, int high){
    int pivot = nums[low];
    int tmp = nums[low];

    while(low < high){
        while(low < high && pivot <= nums[high]) high--; //这里不一样
        nums[low] = nums[high];

        while(low < high && pivot >= nums[low]) low++; //这里不一样
        nums[high] = nums[low];
    }

    nums[low] = tmp;
    return low;

}

void quickSort(vector<int>& nums, int low, int high){
    if(low < high){
        int pivot = partition2(nums, low, high);

        quickSort(nums, low, pivot-1);
        quickSort(nums, pivot+1, high);
    }
}
```
