* 从大到小排序, 注意的是qsort里要有一个if来判断终止条件

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
