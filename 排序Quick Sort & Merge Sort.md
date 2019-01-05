## 快速排序
* 从大到小排序, 每次: 找到第一个大于pivot的high,放在前面, 第一个小于pivot的low,放在pivot的后面
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

* 从小往大排, 每次: 找到第一个小于pivot的high,放在前面, 找到第一个大于pivot的low,放在后面

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

## Merge Sort
* 分治算法的典型,先分成左右两边,然后再合并

```c++
void merge(vector<int>& nums, int low, int mid, int high){
    vector<int> tmp(high-low+1, 0);
    int i = low, j = mid+1, k = 0;

    while(i<= mid && j<= high){
        if(nums[i] <= nums[j])
            tmp[k++] = nums[i++];
        else
            tmp[k++] = nums[j++];
    }

    while(i<=mid){
        tmp[k++] = nums[i++];
    }

    while(j<=high){
        tmp[k++] = nums[j++];
    }

    // 这里注意: 是从low到high的copy,不是整组都copy
    for(k=0, i=low; i<=high; i++,k++)
        nums[i] = tmp[k];
}

void MergeSort(vector<int>& nums, int low, int high){
    if(low < high){
        int mid = (low + high) / 2;
        MergeSort(nums, low, mid);
        MergeSort(nums, mid+1, high);
        merge(nums, low, mid, high);
    }
}

```
