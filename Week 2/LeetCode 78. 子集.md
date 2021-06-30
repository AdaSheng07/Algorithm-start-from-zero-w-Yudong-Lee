```Java
// Java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {

        ans = new ArrayList<List<Integer>> ();
        set = new ArrayList<Integer> ();
        // 从index = 0开始寻找子集
        findSubsets(nums, 0);
        return ans;
    }
    
    private void findSubsets(int[] nums, int index) {
        // System.out.println("==start==");
        // System.out.println(index);
        // System.out.print("set:");
        // for (int num : set) System.out.print(num);
        // System.out.println("\n==end==");
        // 当index = n时，这一层递归结束，将set复制给ans
        if (index == nums.length){
            ans.add(new ArrayList<Integer> (set));
            return; // 返回上一层未执行完的代码，即index = 2，再执行set.add(nums[index = 2]); ...
        }
        // 在nums[index]不选，则index+1，看下一个元素
        findSubsets(nums, index + 1);
        // 在nums[index]选，则将nums[index]放入set中，再看下一个元素
        set.add(nums[index]);
        findSubsets(nums, index + 1);
        set.remove(set.size() - 1); // 全局变量重置，删除上一次执行的结果
    }
        

        // 两个全局变量，属于所有函数体
        private List<List<Integer>> ans;
        private List<Integer> set;

    
}
```
