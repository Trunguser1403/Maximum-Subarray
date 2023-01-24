# Maximum-Subarray
#include<stdio.h>

struct subarrVa{
	int sum;
	int left;
	int right;
	int code;
};

int totalSituation(int n){
	int situation=0;
	for (int i=0; i<n; i++){
		for (int j=i; j<n; j++){
			situation++;
		}
	}
	return situation;
}

int storeArrSum(int array[], int n, subarrVa arr[]){
	int arrCode = 0;
	for (int i=0; i<n; i++){
		int tempSum = 0;
		for (int j=i; j<n; j++){
			tempSum += array[j];
			
			arr[arrCode].sum += tempSum;
			arr[arrCode].left = i;
			arr[arrCode].right = j;
			arr[arrCode].code = arrCode;
			arrCode++;
		}
	}
	return arrCode;
}

int findSubarrayMax(int array[], int n, subarrVa arr[]){
	int code = storeArrSum(array, n, arr);
	int maxSum= arr[0].sum;
	int i_Max;
	
	for (int i=0; i<code; i++){
		if (arr[i].sum> maxSum){
			maxSum=arr[i].sum;
			i_Max=arr[i].code;
		}
	}
	return i_Max;
}

int main()
{
	int array[] = {12,7,-9,0,5,1,8,4,-23,-12,-99,100,34,-21};
	int n = sizeof(array)/sizeof(int);
	subarrVa arr[100000];
	int infor = findSubarrayMax(array, n, arr);
	
	printf("Maximum array: %d\n" );
	for (int i= arr[infor].left; i<= arr[infor].right; i++){
		printf("array[%d]= %d\n", i, array[i]);
	}
}
