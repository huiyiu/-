# 堆排序

    public static void main(String[] args) {
        int[] A = {4, 5, 3, 2, 6, 1};
        heapSort(A, 6);
        System.out.println(A);
    }

    public static int leftChild(int i) {
        return 2 * i + 1;
    }

    /**
     * 元素下沉
     * 给定一个完全二叉树，除了根节点以外，此二叉树满足“堆序性”，“元素下沉”的目的是在此二叉树中将根节点的元素放至合适的坑位，相应地调整其他元素，最终使得包括根节点在内的整棵二叉树都满足“堆序性”。

     “元素下沉”的实施方案说来也很简单：当父节点的元素值小于左子节点的元素值或者右子节点的元素值时，将父节点的元素值与左右子节点较大的元素值进行交换，针对交换后的父节点，循环执行“元素下沉”操作，“元素下沉”的终止条件就是父节点的元素值不小于其任意左右子节点的元素值，或者当前父节点无子节点（即当前节点为叶子节点）。

     * @param A
     * @param i
     * @param N
     */
    public static void percDown(int[] A, int i, int N) {
        //子节点的索引号
        int child;
        //存储当前父节点元素的临时变量
        //(注：每一个节点都可以看作是其子树的根节点)
        int tmp;

        for (tmp = A[i]; leftChild(i) < N; i = child) {
            child = leftChild(i);
            //挑选出左、右子节点中较大者
            if (child != N - 1 && A[child + 1] > A[child]) {
                child++;
            }
            //比较当前父节点与较大子节点
            if (A[i] < A[child]) {
                //交换当前父节点处的元素值与较大子节点的元素值
                swap(A, i, child);
            } else {
                break;
            }

        }
    }

    /**
     * 堆排序
     * @param A
     * @param N
     */
    public static void heapSort(int[] A, int N) {
        int i;
        //步骤一：创建大根堆
        for (i = N / 2; i >= 0; i--) {
            percDown(A, i, N);

        }
        //步骤二：调整大根堆
        for (i = N - 1; i > 0; i--) {
            //首尾交换
            swap(A, 0, i);
            //元素下沉
            percDown(A, 0, i);
        }
    }

    //交换两个元素的位置
    public static void swap(int[] A, int start, int pos) {
        int tmp = A[start];
        A[start] = A[pos];
        A[pos] = tmp;
    }

#快速排序
static class QuickSort {
	 
		public static  void  quickSort(int[] a) {
			if(a.length>0) {
				quickSort(a, 0 , a.length-1);
			}
		}
	 
		private static void quickSort(int[] a, int low, int high) {
			//1,找到递归算法的出口
			if( low > high) {
				return;
			}
			//2, 存
			int i = low;
			int j = high;
			//3,key
			int key = a[ low ];
			//4，完成一趟排序
			while( i< j) {
				//4.1 ，从右往左找到第一个小于key的数
				while(i<j && a[j] > key){
					j--;
				}
				// 4.2 从左往右找到第一个大于key的数
				while(i<j && a[i] <= key) {
					i++;
				}
				//4.3 交换
				if(i<j) {
					int p = a[i];
					a[i] = a[j];
					a[j] = p;
				}
			}
			// 4.4，调整key的位置
			if(a[i]<a[low]) {
				int p = a[i];
				a[i] = a[low];
				a[low] = p;
			}
			//5, 对key左边的数快排
			quickSort(a, low, i-1 );
			//6, 对key右边的数快排
			quickSort(a, i+1, high);
		}
	}
